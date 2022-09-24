---
lab:
  title: 연습 1 - Microsoft Sentinel 환경 구성
  module: Module 5 - Configure your Microsoft Sentinel environment
---

# <a name="module-5---lab-1---exercise-1---configure-your-microsoft-sentinel-environment"></a>모듈 5 - 랩 1 - 연습 1 - Microsoft Sentinel 환경 구성

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod5_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft Sentinel. You are responsible for setting up the Microsoft Sentinel environment to meet the company requirement to minimize cost, meet compliance regulations, and provide the most manageable environment for your security team to perform their daily job responsibilities.


### <a name="task-1-initialize-the-microsoft-sentinel-workspace"></a>작업 1: Microsoft Sentinel 작업 영역 초기화

이 작업에서는 Microsoft Sentinel 작업 영역을 만듭니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저를 엽니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. **+ 만들기**를 선택합니다.

1. Next, select the Log Analytics workspace you created earlier, for example <bpt id="p1">*</bpt>uniquenameDefender<ept id="p1">*</ept> and select <bpt id="p2">**</bpt>Add<ept id="p2">**</ept>. The activation could take a few minutes.

    >**참고:** 여기에 Log Analytics 작업 영역이 표시되지 않으면 모듈 3, 연습 1, 작업 2를 참조하여 만듭니다.

1. 새로 만든 Microsoft Sentinel 작업 영역 내를 이동하면서 사용자 인터페이스 옵션을 숙지합니다.


### <a name="task-2-create-a-watchlist"></a>작업 2: 관심 목록 만들기

이 작업에서는 Microsoft Sentinel에서 관심 목록을 만듭니다.

1. In the search box at the bottom of the Windows 10 screen, enter <bpt id="p1">*</bpt>Notepad<ept id="p1">*</ept>. Select <bpt id="p1">**</bpt>Notepad<ept id="p1">**</ept> from the results.

1. *Hostname*을 입력하고 Enter 키를 눌러 새 줄을 시작합니다.

1. 메모장의 행 2에서 다음 호스트 이름을 각각 다른 줄에 복사합니다.

    ```Notepad
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. From the menu select, <bpt id="p1">**</bpt>File - Save As<ept id="p1">**</ept>, Name the file <bpt id="p2">*</bpt>HighValue.csv<ept id="p2">*</ept>, change the file type to <bpt id="p3">**</bpt>All files(<bpt id="p4">*</bpt>.<ept id="p4">*</ept>)<ept id="p3">**</ept> and select <bpt id="p5">**</bpt>Save<ept id="p5">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> The file can be saved in the <bpt id="p2">*</bpt>Documents<ept id="p2">*</ept> folder.

1. 메모장을 닫습니다.

1. Microsoft Sentinel의 구성 영역에서 **관심 목록** 옵션을 선택합니다.

1. 명령 모음에서 **+ 새 항목 추가**를 선택합니다.

1. 관심 목록 마법사에 다음 정보를 입력합니다.

    |일반 설정|값|
    |---|---|
    |Name|**HighValueHosts**|
    |설명|**중요 호스트**|
    |관심 목록 별칭|**HighValueHosts**|

1. **다음: 원본 >** 을 선택합니다.

1. 파일 업로드에서 **파일 찾아보기**를 선택하고 방금 만든 *HighValue.csv* 파일을 찾습니다.

1. SearchKey 필드에서 **Hostname**을 선택합니다.

1. **다음: 검토 및 만들기 >** 를 선택합니다.

1. 입력한 설정을 검토하고 **만들기**를 선택합니다.

1. 화면에 관심 목록 페이지가 다시 표시됩니다.

1. *HighValueHosts* 관심 목록을 선택하고 오른쪽 탭에서 **로그에서 보기**를 선택합니다.

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> It could take some time for the watchlist to appear. <bpt id="p1">**</bpt>Please continue to with the following task and run this command on the next lab<ept id="p1">**</ept>.
    
    >당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다.

1. 오른쪽 위에 있는 ‘x’를 선택하여 로그 창을 닫고 **확인**을 선택하여 저장되지 않은 편집 내용을 삭제합니다.


### <a name="task-3-create-a-threat-indicator"></a>작업 3: 위협 표시기 만들기

이 작업에서는 Microsoft Sentinel에서 표시기를 만듭니다.

1. Microsoft Sentinel의 위협 관리 영역에서 **위협 인텔리전스** 옵션을 선택합니다.

1. 명령 모음에서 **+ 새 항목 추가**를 선택합니다.

1. 비용을 최소화하고, 규정 준수 규정을 충족하며, 보안 팀이 일상적인 업무 책임을 수행하도록 가장 관리 가능한 환경을 제공하기 위해 회사의 요구 사항을 충족하는 Microsoft Sentinel 환경을 설정할 책임이 있습니다.

1. 위협 형식에서 **malicious-activity**를 선택합니다.

1. For the <bpt id="p1">*</bpt>Name<ept id="p1">*</ept>, enter the same value used for the Domain. An example would be <bpt id="p1">*</bpt>fmg.com<ept id="p1">*</ept>.

1. *유효 기간(시작)* 필드의 값을 오늘 날짜로 설정합니다.

1. **적용**을 선택합니다.

1. Select the <bpt id="p1">**</bpt>Logs<ept id="p1">**</ept> option under the General area. You might want to disable the "Always show queries" option and close the <bpt id="p1">*</bpt>Queries<ept id="p1">*</ept> window to run the KQL statements.

1. 다음 KQL 문을 실행합니다.

    ```KQL
    ThreatIntelligenceIndicator
    ```

    >**참고:** 표시기가 표시되려면 시간이 다소 걸릴 수 있습니다.

1. Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column. 

    ```KQL
    ThreatIntelligenceIndicator | project DomainName
    ```

### <a name="task-4-configure-log-retention"></a>작업 4: 로그 보존 구성

이 작업에서는 SecurityEvent 테이블의 보존 기간을 변경합니다.

1. Microsoft Sentinel의 구성 영역에서 **설정** 옵션을 선택합니다.
1. **작업 영역 설정**을 선택합니다.
1. Log Analytics 작업 영역의 설정 영역에서 **테이블(미리 보기)** 옵션을 선택합니다.
1. 테이블 이름 **SecurityEvent**를 선택한 다음 **...** 를 선택합니다.
1. **테이블 관리**를 선택합니다.
1. Select <bpt id="p1">**</bpt>180 days<ept id="p1">**</ept> for <bpt id="p2">*</bpt>Total retention period<ept id="p2">*</ept>. Then <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.


## <a name="you-have-completed-the-lab"></a>이 랩을 완료했습니다.
