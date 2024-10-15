# 모듈 6 Microsoft Sentinel을 사용하여 탐지 만들기 및 조사 수행

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다.

**중요:** VTD-5002-FY25에는 이 데모가 필요하지 않습니다.

## NRT 쿼리 규칙 만들기

이 작업에서는 NRT(Near Real Time) 분석 쿼리 규칙을 만듭니다.

1. Microsoft Sentinel의 *구성*에서 **분석** 페이지를 선택합니다.

1. **만들기** 탭을 선택한 다음, **NRT 쿼리 규칙**을 선택합니다.

1. 그러면 “분석 규칙 마법사”가 시작됩니다. 일반 탭에서 다음을 입력합니다.**

    |설정|값|
    |---|---|
    |속성|**NRT PowerShell 헌팅**|
    |설명|**NRT PowerShell 헌팅**|
    |전술 및 기술|**명령 및 제어**.|
    |심각도
          |**높음**|

1. **다음: 규칙 논리 설정 >** 단추를 선택합니다. 

1. 규칙 쿼리의 경우 KQL 문을 입력합니다.**

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

1. 쿼리에 오류가 없는지 확인하려면 **쿼리 결과 보기 >** 를 선택합니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 로그 창을 닫고 **확인**을 선택하여 변경 내용을 취소합니다.** 

1. *결과 시뮬레이션*에서 **현재 데이터로 테스트**를 선택합니다. 예상되는 *일일 경고* 수를 확인합니다.

1. *엔터티 매핑*에서 다음을 선택합니다.

    - 엔터티 유형 드롭다운 목록에서 **호스트**를 선택합니다.**
    - 식별자 드롭다운 목록에서 **호스트 이름**을 선택합니다.**
    - *값* 드롭다운 목록에서 **컴퓨터**를 선택합니다.

1. 아래로 스크롤하여 **다음: 인시던트 설정>** 단추를 선택합니다.

1. *인시던트 설정* 탭의 경우 기본값을 그대로 두고 **다음: 자동화된 응답 >** 단추를 선택합니다.

1. **다음: 검토 + 만들기 >** 를 클릭합니다.

1. *검토 및 만들기* 탭에서 **저장** 단추를 선택하여 새 예약된 분석 규칙을 만들고 저장합니다.

## AMA(Azure Monitor 에이전트)로 구성된 공격 검색 Windows

이 작업에서는 사용자가 만든 `NRT` 규칙에서 생성된 인시던트 조사를 수행합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자용 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자용 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. `Microsoft Sentinel`에서 `Threat management` 메뉴 섹션으로 이동하여 **인시던트** 선택

**참고** `Incident`이(가) 표시되는 데 몇 분 정도 걸릴 수 있습니다.

1. 사용자가 만든 `NRT` 규칙에서 구성한 `Severity` 및 `Title`와(과) 일치하는 인시던트가 표시됩니다.

1. `Incident`을(를) 선택하면 `detail` 창이 열립니다.

1. **전체 세부 정보 보기**를 선택하고 **조사** 단추를 선택합니다.

1. 다음 `NRT PowerShell Hunt` 인시던트에 대한 `Entities` 연결을 탐색합니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 `Investigation` 창을 닫습니다.

1. `Logs` 탭을 선택하고 다음 KQL 문을 입력합니다.

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

**참고** 이 쿼리는 `Queries History`에서 찾을 수 있으며 여기에서 **실행**할 수 있습니다.

1. **완료** 단추를 선택하여 `Logs` 창을 닫습니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 `Incident` 창을 닫습니다.

## 이 데모를 완료했습니다.
