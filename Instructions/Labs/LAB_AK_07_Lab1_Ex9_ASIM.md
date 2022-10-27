---
lab:
  title: 연습 9 - ASIM 파서 만들기
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-9---create-asim-parsers"></a>모듈 7 - 랩 1 - 연습 9 - ASIM 파서 만들기

## <a name="lab-scenario"></a>랩 시나리오

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 특정 Windows 레지스트리 이벤트에 대한 ASIM 파서를 모델링해야 합니다.  이러한 간소화된 파서는 ASIM 파서 레지스트리 이벤트 정규화 표준(https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema) )에 따라 나중에 완료됩니다.

>**중요:** 이 랩에서는 긴 KQL ASIM 파서 스크립트를 Microsoft Sentinel에 입력합니다. 스크립트는 이 랩의 시작 부분에 있는 다운로드 파일을 통해 제공되었습니다. 스크립트를 다운로드할 대체 위치는 https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Allfiles 입니다.

### <a name="task-1-develop-kql-function-for-microsoft-365-defender-registry-event"></a>작업 1: Microsoft 365 Defender 레지스트리 이벤트에 대한 KQL 함수 개발 

이 작업에서는 DeviceRegistryEvents에 대한 작업 영역 파서인 함수를 만듭니다. 

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. **로그** 페이지를 선택합니다.

1. 다운로드한 **SC200_module7_ASIM_Parser_scripts.txt**를 열고 작업 1 스크립트 KQL 문을 복사하여 새 쿼리 탭에 붙여넣습니다.

    >**참고** 아래 표시된 스크립트는 참조용입니다.

    ```KQL
    let RegistryType = datatable (TypeCode: string, TypeName: string) [
    "None", "Reg_None",
    "String", "Reg_Sz",
    "ExpandString", "Reg_Expand_Sz",
    "Binary", "Reg_Binary",
    "Dword", "Reg_DWord",
    "MultiString", "Reg_Multi_Sz",
    "QWord", "Reg_QWord"
    ];
    let RegistryEvents_M365D=() {
    DeviceRegistryEvents
    | extend
        // Event
        EventOriginalUid = tostring(ReportId),
        EventCount = int(1), 
        EventProduct = 'M365 Defender for Endpoint',
        EventVendor = 'Microsoft', 
        EventSchemaVersion = '0.1.0', 
        EventStartTime = TimeGenerated, 
        EventEndTime = TimeGenerated, 
        EventType = ActionType,
        // Registry
        RegistryKey = iff (ActionType in ("RegistryKeyDeleted", "RegistryValueDeleted"), PreviousRegistryKey, RegistryKey),
        RegistryValue = iff (ActionType == "RegistryValueDeleted", PreviousRegistryValueName, RegistryValueName),
        // RegistryValueType -- original name is fine
        // RegistryValueData -- original name is fine
        RegistryKeyModified = iff (ActionType == "RegistryKeyRenamed", PreviousRegistryKey, ""),
        RegistryValueModified = iff (ActionType == "RegistryValueSet", PreviousRegistryValueName, ""),
        // RegistryValueTypeModified -- Not provided by Defender
        RegistryValueDataModified = PreviousRegistryValueData
    | lookup RegistryType on $left.RegistryValueType == $right.TypeCode
    | extend RegistryValueType = TypeName
    | project-away
        TypeName,
        PreviousRegistryKey,
        PreviousRegistryValueName,
        PreviousRegistryValueData
    // Device
    | extend
        DvcHostname = DeviceName,
        DvcId = DeviceId,
        Dvc = DeviceName
    // Users
    | extend
        ActorUsername = iff (InitiatingProcessAccountDomain == '', InitiatingProcessAccountName, strcat(InitiatingProcessAccountDomain, '\\', InitiatingProcessAccountName)), 
        ActorUsernameType = iff(InitiatingProcessAccountDomain == '', 'Simple', 'Windows'), 
        ActorUserIdType = 'SID'
    | project-away InitiatingProcessAccountDomain, InitiatingProcessAccountName
    | project-rename
    ActorUserId = InitiatingProcessAccountSid, 
    ActorUserAadId = InitiatingProcessAccountObjectId, 
    ActorUserUpn = InitiatingProcessAccountUpn
    // Processes
    | extend
    ActingProcessId = tostring(InitiatingProcessId), 
    ParentProcessId = tostring(InitiatingProcessParentId) 
    | project-away InitiatingProcessId, InitiatingProcessParentId
    | project-rename
    ParentProcessName = InitiatingProcessParentFileName, 
    ParentProcessCreationTime = InitiatingProcessParentCreationTime, 
    ActingProcessName = InitiatingProcessFolderPath, 
    ActingProcessFileName = InitiatingProcessFileName,
    ActingProcessCommandLine = InitiatingProcessCommandLine, 
    ActingProcessMD5 = InitiatingProcessMD5, 
    ActingProcessSHA1 = InitiatingProcessSHA1, //OK
    ActingProcessSHA256 = InitiatingProcessSHA256, 
    ActingProcessIntegrityLevel = InitiatingProcessIntegrityLevel, 
    ActingProcessTokenElevation = InitiatingProcessTokenElevation, 
    ActingProcessCreationTime = InitiatingProcessCreationTime 
    // -- aliases
    | extend 
    Username = ActorUsername,
    UserId = ActorUserId,
    UserIdType = ActorUserIdType,
    User = ActorUsername,
    CommandLine = ActingProcessCommandLine,
    Process = ActingProcessName
    };
    RegistryEvents_M365D
    ```

1. **참고:** 시간을 내어 KQL 줄을 한 줄씩 검토합니다.

1. **실행**을 선택하여 KQL이 유효한지 확인합니다.

1. **저장**을 선택한 다음, **함수로 저장**을 선택합니다.

    |아래로 스크롤하여 쿼리 예약에서 다음을 설정합니다.|설정|
    |---|---|
    |값|함수 이름|
    |vimRegEvtM365D|레거시 범주|

1. MyASIM

1. 그런 다음 **저장**을 선택합니다.


### <a name="task-2-develop-kql-function-for-securityevent-table"></a>새 쿼리 탭에서 **vimRegEvtM365D**를 입력하고 **실행**을 선택합니다. 

작업 2: SecurityEvent 테이블에 대한 KQL 함수를 개발합니다.

1. 이 작업에서는 SecurityEvent의 작업 영역 파서인 함수를 만듭니다.

1. 새 쿼리 탭을 만듭니다.

    >다운로드한 **SC200_module7_ASIM_Parser_scripts.txt**를 열고 작업 2 스크립트 KQL 문을 복사하여 새 쿼리 탭에 붙여넣습니다.

    ```KQL
    let RegistryType = datatable (TypeCode: string, TypeName: string) [
    "%%1872", "Reg_None",
    "%%1873", "Reg_Sz",
    "%%1874", "Reg_Expand_Sz",
    "%%1875", "Reg_Binary",
    "%%1876", "Reg_DWord",
    "%%1879", "Reg_Multi_Sz",
    "%%1883", "Reg_QWord"
    ];
    let RegistryAction = datatable (EventOriginalSubType: string, EventType: string) [
        "%%1904", "RegistryValueSet",
        "%%1905", "RegistryValueSet",      
        "%%1906", "RegistryValueDeleted"             
    ];
    let Hives = datatable (KeyPrefix: string, Hive: string) [
        "MACHINE", "HKEY_LOCAL_MACHINE",
        "USER", "HKEY_USERS",   
    ];
    let RegistryEvents=() {
        SecurityEvent
        // -- Filter
        | where EventID == 4657          
        // Event
        | extend
            EventCount = int(1), 
            EventVendor = 'Microsoft', 
            EventProduct = 'Security Events', 
            EventSchemaVersion = '0.1.0', 
            EventStartTime = todatetime(TimeGenerated), 
            EventEndTime = todatetime(TimeGenerated),
            EventOriginalType = tostring(EventID) 
        | project-rename
            EventOriginalSubType = OperationType,
            EventOriginalUid = EventOriginId
        | lookup RegistryAction on EventOriginalSubType
        // Registry
        // Normalize key hive
        | parse ObjectName with "\\REGISTRY\\" KeyPrefix "\\" Key
        | lookup Hives on KeyPrefix
        | extend RegistryKey = strcat (Hive, "\\", Key)
        | project-away Hive, Key, KeyPrefix, ObjectName
        | project-rename
            RegistryValue = ObjectValueName
        | extend
            RegistryValueData = iff (EventOriginalSubType == "%%1906", OldValue, NewValue), 
            RegistryKeyModified = iff (EventOriginalSubType == "%%1905", RegistryKey, ""),
            RegistryValueModified = iff (EventOriginalSubType == "%%1905", RegistryValue, ""),
            RegistryValueDataModified = iff (EventOriginalSubType == "%%1905", OldValue, "")
        | lookup RegistryType on $left.NewValueType == $right.TypeCode
        | project-rename RegistryValueType = TypeName
        | lookup RegistryType on $left.OldValueType == $right.TypeCode
        | project-rename RegistryValueTypeModified = TypeName
        | project-away OldValue, NewValue, OldValueType, NewValueType
        // Device
        | extend
            DvcId = SourceComputerId,
            DvcHostname = Computer,
            DvcOs = 'Windows'
        // User
        | project-rename
            ActorUserId = SubjectUserSid, 
            ActorSessionId = SubjectLogonId, 
            ActorDomainName = SubjectDomainName
        | extend
            ActorUserIdType = 'SID',
            ActorUsername = iff (ActorDomainName == '-', SubjectUserName, SubjectAccount), 
            ActorUsernameType = iff(ActorDomainName == '-', 'Simple', 'Windows'),
            ActingProcessId = tostring(toint(ProcessId)) 
        // Process 
        | project-rename
            ActingProcessName = ProcessName
        // -- Aliases
        | extend
            User = ActorUsername,
            UserId = ActorUserId,
            Dvc = DvcHostname,
            Process = ActingProcessName
        // -- Remove potentially confusing
        | project-away 
            SubjectUserName,
            SubjectAccount
    };
    RegistryEvents
    ```

1. **참고** 아래 표시된 스크립트는 참조용입니다.

1. **참고:** 시간을 내어 KQL 줄을 한 줄씩 검토합니다.

1. **실행**을 선택하여 KQL이 유효한지 확인합니다.

    |**저장**을 선택한 다음, **함수로 저장**을 선택합니다.|아래로 스크롤하여 쿼리 예약에서 다음을 설정합니다.|
    |---|---|
    |설정|값|
    |함수 이름|vimRegEvtSecurityEvent|

1. 레거시 범주

1. MyASIM


### <a name="task-3-create-a-unifying-workspace-parser"></a>그런 다음 **저장**을 선택합니다. 

새 쿼리 탭에서 **vimRegEvtSecurityEvent**를 입력하고 **실행**을 선택합니다.  

1. 작업 3: 통합 작업 영역 파서 만들기

1. 이 작업에서는 이전 두 함수를 결합하는 통합 파서 함수를 만듭니다.

    ```KQL
    union isfuzzy=true
    vimRegEvtM365D,
    vimRegEvtSecurityEvent
    ```

1. 새 쿼리 탭을 만듭니다.

1. 새 쿼리 탭에 다음 KQL 문을 입력합니다.

1. **실행**을 선택하여 KQL이 유효한지 확인합니다.

    |**저장**을 선택한 다음, **함수로 저장**을 선택합니다.|아래로 스크롤하여 쿼리 예약에서 다음을 설정합니다.|
    |---|---|
    |설정|값|
    |함수 이름|imRegEvt|

1. 레거시 범주

1. MyASIM

1. 그런 다음 **저장**을 선택합니다.

    ```KQL
    imRegEvt
    | where ActionType == 'RegistryValueSet'
    ```

## <a name="proceed-to-exercise-10"></a>새 쿼리 탭에서 **imRegEvt**를 입력하고 **실행**을 선택합니다.

