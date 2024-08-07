---
lab:
  title: 연습 1 - Microsoft Sentinel에서 위협 헌팅 수행
  module: Learning Path 8 - Perform threat hunting in Microsoft Sentinel
---

# 학습 경로 8 - 랩 1 - 연습 1 - Microsoft Sentinel에서 위협 헌팅 수행

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex1.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. C2 또는 C&C(명령 및 제어) 기술 관련 위협 인텔리전스를 수신했습니다. 헌트를 수행하고 위협을 감시해야 합니다.

>**중요:** 랩에서 사용되는 로그 데이터는 이전 모듈에서 작성된 것입니다. 연습 5의 WIN1 서버에서 **공격 3**을 참조하세요.

>**참고:** 이전 모듈에서 데이터 살펴보기 프로세스는 이미 진행했으므로, 이 랩에서는 작업 시작을 위한 KQL 문이 제공됩니다.

>**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Perform%20threat%20hunting%20in%20Microsoft%20Sentinel)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 


### 작업 1: 헌팅 쿼리 만들기

이 작업에서는 헌팅 쿼리를 만들고 결과를 책갈피에 저장한 후 라이브 스트림을 만듭니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(<https://portal.azure.com> )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. **로그**를 선택합니다. 

1. 새 쿼리 1 공간에 다음 KQL 문을 입력합니다.**

   >**중요:** 먼저 메모장에 KQL 쿼리를 붙여넣은 다음, 해당 위치에서 새 쿼리 1 로그 창으로 복사하여 오류를 방지하세요.**

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam 
    | order by count_ desc nulls last 
    ```

1. 다양한 결과를 검토합니다. 이제 사용자 환경에서 실행 중인 PowerShell 요청을 식별했습니다.

1. *"-file c2.ps1"* 을 표시하는 결과의 확인란을 선택합니다.

1. *결과* 창 명령 모음에서 **책갈피 추가** 단추를 선택합니다.

1. *엔터티 매핑*에서 **+ 새 엔터티 추가**를 선택합니다.

1. *엔터티*의 경우 **호스트**를 선택한 다음 값으로 **호스트 이름** 및 **컴퓨터**를 선택합니다.

1. *전술 및 기술*에서 **명령 및 제어**를 선택합니다.

1. *책갈피 추가* 블레이드에서 **만들기**를 선택합니다. 나중에 이 책갈피를 인시던트에 매핑할 것입니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 로그 창을 닫고 **확인**을 선택하여 변경 내용을 취소합니다.** 

1. Microsoft Sentinel 작업 영역을 다시 선택하고 *위협 관리* 영역에서 **헌팅** 페이지를 선택합니다.

1. 명령 모음에서 **쿼리** 탭을 선택한 다음 **+ 새 쿼리**를 선택합니다.

1. *사용자 지정 쿼리 만들기* 창에서 *이름*에 **PowerShell Hunt**를 입력합니다.

1. *사용자 지정 쿼리*에 다음 KQL 문을 붙여 넣습니다.

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam 
    | order by count_ desc nulls last 
    ```

1. 아래로 스크롤하여 *엔터티 매핑*에서 다음을 선택합니다.

    - 엔터티 유형 드롭다운 목록에서 **호스트**를 선택합니다.**
    - 식별자 드롭다운 목록에서 **호스트 이름**을 선택합니다.**
    - *값* 드롭다운 목록에서 **컴퓨터**를 선택합니다.

1. 아래로 스크롤하고, 전술 & 기술 아래에서 **명령 및 제어** 를 선택한 다음, **만들기**를 선택하여 헌팅 쿼리를 만듭니다.**

1. *"Microsoft Sentinel - 헌팅"* 블레이드의 목록에서 방금 만든 쿼리인 *PowerShell Hunt*를 쿼리합니다.

1. 목록에서 **PowerShell Hunt**를 선택합니다.

1. *결과* 열 아래 중간 창에 있는 결과 수를 검토합니다.

1. 오른쪽 창에서 **결과 보기** 단추를 선택합니다. KQL 쿼리가 자동으로 실행됩니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 로그 창을 닫고 **확인**을 선택하여 변경 내용을 취소합니다.** 

1. **PowerShell Hunt** 쿼리를 마우스 오른쪽 단추로 클릭하고 **라이브스트림에 추가**를 선택합니다. **힌트:** 또한 오른쪽으로 슬라이딩하고 행 끝에 있는 줄임표 **(...)** 를 선택하여 상황에 맞는 메뉴를 열어도 됩니다.

1. *상태*가 현재 *실행* 중인지 검토합니다. 이는 백그라운드에서 30초마다 실행되며 새 결과가 발견되면 Azure Portal(종 모양 아이콘)에서 알림을 받게 됩니다. 

1. 가운데 창에서 **책갈피** 탭을 선택합니다.

1. 결과 목록에서 방금 만든 책갈피를 선택합니다.

1. 오른쪽 창에서 아래로 스크롤하여 **조사** 단추를 선택합니다. **힌트:** 조사 그래프를 표시하는 데 몇 분 정도 걸릴 수 있습니다.

1. 이전 모듈에서와 마찬가지로 조사 그래프를 살펴봅니다. *WINServer*에 대한 *관련 경고*의 수가 많은 것을 확인합니다.

1. 창 오른쪽 상단에 있는 **X**를 선택하여 *조사* 그래프 창을 닫습니다. 

1. **>>** 아이콘을 선택하여 오른쪽 블레이드를 숨긴 다음 줄임표 **(...)** 아이콘이 나타날 때까지 오른쪽으로 스크롤합니다.

1. **기존 인시던트에 추가**를 선택합니다. 모든 인시던트가 오른쪽 창에 나타납니다.

1. 인시던트 중 하나를 선택한 다음 **추가**를 선택합니다.

1. 왼쪽으로 스크롤하면 이제 *심각도* 열이 인시던트 데이터로 채워져 있는 것을 확인할 수 있습니다.


### 작업 2: NRT 쿼리 규칙 만들기

이 작업에서는 LiveStream을 사용하는 대신 NRT 분석 쿼리 규칙을 만듭니다. NRT 규칙은 1분마다 실행되고 1분마다 조회됩니다. NRT 규칙의 이점은 경고 및 인시던트 생성 논리를 사용할 수 있다는 것입니다.

1. Microsoft Sentinel의 *구성*에서 **분석** 페이지를 선택합니다. 

1. **만들기** 탭을 선택한 다음, **NRT 쿼리 규칙**을 선택합니다.

1. 그러면 “분석 규칙 마법사”가 시작됩니다. 일반 탭에서 다음을 입력합니다.**

    |설정|값|
    |---|---|
    |속성|**NRT PowerShell 헌팅**|
    |설명|**NRT PowerShell 헌팅**|
    |전술|**명령 및 제어**.|
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

1. *자동화된 대응* 탭에서 **다음: 검토 및 만들기 >** 단추를 선택합니다.

1. *검토 및 만들기* 탭에서 **저장** 단추를 선택하여 새 예약된 분석 규칙을 만들고 저장합니다.

### 작업 3: 검색 작업 만들기

이 작업에서는 검색 작업을 사용하여 C2를 찾습니다.

>**참고:** *복원* 작업을 수행하면 Azure Pass 구독 크레딧이 고갈될 수 있는 비용이 발생합니다. 따라서 이 랩에서는 복원 작업을 수행하지 않습니다. 그러나 아래 단계에 따라 사용자 환경에서 복원 작업을 수행할 수 있습니다.

1. Microsoft Sentinel의 *일반*에서 **검색** 페이지를 선택합니다.

1. 검색 상자에 **reg.exe**를 입력한 다음 **시작**을 선택합니다.

1. 쿼리를 실행하는 새 창이 열립니다. 오른쪽 상단에서 줄임표 아이콘 **(...)** 을 선택한 다음 **작업 검색 모드**를 전환합니다.

1. 명령 모음에서 **작업 검색** 단추를 선택합니다. 

1. 검색 작업은 결과가 도착하자마자 결과가 포함된 새 테이블을 만듭니다. 결과는 *저장된 검색* 탭에서 확인할 수 있습니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 로그 창을 닫고 **확인**을 선택하여 변경 내용을 취소합니다.**

1. 명령 모음에서 **복원** 탭을 선택한 다음 **복원** 단추를 선택합니다.

1. *복원할 테이블 선택*에서 **SecurityEvent**를 검색하여 선택합니다.

1. 사용 가능한 옵션을 검토한 후 **취소** 단추를 선택합니다.

    >**참고:** 작업을 실행 중인 경우 복원이 몇 분 동안 실행되고 데이터를 새 테이블에서 사용할 수 있습니다.

## 연습 2 계속 진행
