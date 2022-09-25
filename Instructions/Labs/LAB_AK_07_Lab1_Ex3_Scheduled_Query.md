---
lab:
  title: 연습 3 - 예약된 쿼리 만들기
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-3---create-a-scheduled-query"></a>모듈 7 - 랩 1 - 연습 3 - 예약된 쿼리 만들기

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex3.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. After connecting your data sources to Microsoft Sentinel, you create custom analytics rules to help discover threats and anomalous behaviors in your environment.

분석 규칙은 사용자 환경에서 특정 이벤트 또는 이벤트 세트를 검색하고, 특정 이벤트 임계값 또는 조건에 도달하면 경고를 생성하고, SOC에서 심사 및 조사를 위해 인시던트를 생성하고, 자동화된 추적 및 수정 프로세스를 통해 위협에 대응합니다.


### <a name="task-1-create-a-scheduled-query"></a>작업 1: 예약된 쿼리 만들기

이 작업에서는 예약된 쿼리를 만들고 이를 이전 연습에서 만든 Teams 채널에 연결합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. 구성 영역에서 **분석**을 선택합니다.

1. **+ 만들기** 단추를 선택하고 **예약된 쿼리 규칙**을 선택합니다.

1. 분석 규칙 마법사의 일반 탭에서 Azure AD 역할 할당 감사 내역 이름을 입력합니다.

1. 전술의 경우 **지속성**을 선택합니다.

1. 심각도는 **낮음**을 선택합니다.

1. **다음: 규칙 논리 설정 >** 단추를 선택합니다.

1. 규칙 쿼리에 다음 KQL 문을 붙여넣습니다.

    ><bpt id="p1">**</bpt>Warning:<ept id="p1">**</ept> When using the Paste function to the virtual machine extra (pipe) characters could be added. Make sure you use Notepad first to paste the following query.

    ```KQL
    AuditLogs  
    | where isnotempty(InitiatedBy.user.userPrincipalName) and Result == 'success' and OperationName contains "member to role" and AADOperationType startswith "Assign"
    | extend InitiatedByUPN = tostring(InitiatedBy.user.userPrincipalName)
    | extend InitiatedFromIP = iff(tostring(AdditionalDetails.[7].value) == '', tostring(AdditionalDetails.[6].value), tostring(AdditionalDetails.[7].value))
    | extend TargetUser = tostring(TargetResources.[2].displayName)
    | extend TargetRoleName = tostring(TargetResources.[0].displayName)
    | project TimeGenerated, InitiatedByUPN, InitiatedFromIP, TargetUser, TargetRoleName, AADOperationType, OperationName
    ```

1. Select <bpt id="p1">**</bpt>View query results<ept id="p1">**</ept>. You should not receive any results nor any errors. If you receive an error, please review that the query appears just like the previous KQL statement. Close the <bpt id="p1">*</bpt>Logs<ept id="p1">*</ept> window by selecting the upper right <bpt id="p2">**</bpt>X<ept id="p2">**</ept> and select <bpt id="p3">**</bpt>OK<ept id="p3">**</ept> to discard to save changes to go back to the wizard.

1. “분석 규칙 마법사 - 예약된 새 규칙 만들기” 블레이드의 *경고 보강* 영역에서 **엔터티 매핑**을 선택하고 다음 값을 선택합니다. 

    - 엔터티 유형 드롭다운 목록에서 **Account**를 선택합니다.
    - 식별자 드롭다운 목록에서 **FullName**을 선택합니다.
    - 값 드롭다운 목록에서 **InitiatedByUPN**을 선택합니다.

1. 그런 다음, **새 엔터티 추가**를 선택하고 다음 값을 선택합니다.

    - 엔터티 유형 드롭다운 목록에서 **IP**를 선택합니다.
    - 식별자 드롭다운 목록에서 **Address**를 선택합니다.
    - 값 드롭다운 목록에서 **InitiatedFromIP**를 선택합니다.

1. 아래로 스크롤하여 쿼리 예약에서 다음을 설정합니다.

    |설정|값|
    |---|---|
    |쿼리 실행 간격|5분|
    |마지막부터 데이터 보기|1일|

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. 경고 임계값 영역에서 경고가 모든 이벤트를 등록하도록 하므로 값을 변경하지 않고 그대로 둡니다.

1. 쿼리가 위에 지정된 경고 임계값보다 더 많은 결과를 반환하는 한 이벤트 그룹화 영역에서는 실행될 때마다 단일 경고를 생성하려고 하므로 **모든 이벤트를 단일 경고로 그룹화**합니다.

1. 하단에서 **다음: 인시던트 설정 >** 단추를 선택합니다. 

1. 인시던트 설정 탭에서 기본 옵션을 검토합니다.

1. 하단에서 **다음: 자동화된 응답 >** 단추를 선택합니다.

1. 경고 자동화 영역의 자동화된 응답 탭에서 이전 연습에서 만든 *PostMessageTeams-OnAlert* 플레이북을 선택합니다.
1. 인시던트 자동화 탭에서 **새로 추가**를 선택합니다.
1. 자동화 규칙 이름에 **계층 2**를 입력합니다.
1. 작업에서 **소유자 할당**을 선택합니다.
1. Then select <bpt id="p1">**</bpt>Assign to me<ept id="p1">**</ept>. Then select <bpt id="p1">**</bpt>Apply<ept id="p1">**</ept>.

1. 하단에서 **다음: 검토 >** 단추를 선택합니다.
  
1. **만들기**를 선택합니다.


### <a name="task-2-test-our-new-rule"></a>작업 2: 새 규칙 테스트

이 작업에서는 새 예약된 쿼리 규칙을 테스트합니다.

1. 당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다.

1. “사용자 - 모든 사용자” 페이지가 표시되도록 관리 영역에서 **사용자**를 선택합니다.

1. “Christie Cline - 프로필” 페이지가 표시되도록 목록에서 사용자 **Christie Cline**을 선택합니다.

1. “Christie Cline - 할당된 역할” 페이지가 표시되도록 관리 영역에서 **할당된 역할**을 선택합니다.

1. 명령 모음에서 **+ 할당 추가**를 선택합니다.

1. Microsoft Sentinel을 사용하여 위협을 검색하고 완화하는 방법을 파악해야 합니다.

    >**참고:** 새 역할 할당을 확인하려면 **새로 고침** 단추를 클릭해야 합니다. 

1. 오른쪽 위에 있는 ‘x’를 두 번 선택하여 “Christie Cline - 할당된 역할” 및 “사용자 - 모든 사용자” 페이지를 닫습니다.

1. “Contoso - 개요” Azure Active Directory 페이지의 *모니터링*에서 **감사 로그**를 선택합니다.

1. 데이터 원본을 Microsoft Sentinel에 연결한 후, 사용자 환경에서 위협 및 비정상적인 동작을 검색하는 데 도움이 되는 사용자 지정 분석 규칙을 만듭니다.

1. 이전에 Sentinel용으로 만든 Log Analytics 작업 영역에 대한 진단 설정 항목이 있는지 검토합니다. 

1. 오른쪽 위에서 ‘x’를 선택하여 페이지를 닫습니다.

1. “Contoso - 감사 로그”로 돌아가서 이전에 수행한 역할의 변경을 나타내는 카테고리: RoleManagement에 대한 항목이 표시될 때까지 **새로 고침**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. **인시던트** 메뉴 옵션을 선택합니다.

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The alert triggered may take 5+ minutes to process. You may continue with the next exercise and return to this point later. For automatic updating of the Incidents page, select the <bpt id="p1">**</bpt>Auto-refresh incidents<ept id="p1">**</ept> toggle.

1. You should see the newly created Incident. Select the Incident and review the information in the right blade.

1. Go back to Microsoft Teams by selecting the tab in your Edge browser. If you closed it, just open a new tab and type <ph id="ph1">https://teams.microsoft.com</ph>. Go to the <bpt id="p1">*</bpt>SOC<ept id="p1">*</ept> Teams, select the <bpt id="p2">*</bpt>New Alerts<ept id="p2">*</ept> channel and see the message post about the incident.

## <a name="proceed-to-exercise-4"></a>연습 4 계속 진행
