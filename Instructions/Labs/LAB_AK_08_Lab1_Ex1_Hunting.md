---
lab:
  title: 연습 1 - Microsoft Sentinel에서 위협 헌팅 수행
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-1---perform-threat-hunting-in-microsoft-sentinel"></a>모듈 8 - 랩 1 - 연습 1 - Microsoft Sentinel에서 위협 헌팅 수행

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex1.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You have received threat intelligence about a Command and Control (C2 or C&amp;C) technique. You need to perform a hunt and watch for the threat.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The log data used in the lab was created in the previous module. See <bpt id="p1">**</bpt>Attack 3<ept id="p1">**</ept> on WIN1 server in Exercise 5.

>**참고:** 이전 모듈에서 데이터 살펴보기 프로세스는 이미 진행했으므로, 이 랩에서는 작업 시작을 위한 KQL 문이 제공됩니다. 


### <a name="task-1-create-a-hunting-query"></a>작업 1: 헌팅 쿼리 만들기

이 작업에서는 헌팅 쿼리를 만들고 결과를 책갈피에 저장한 후 라이브 스트림을 만듭니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. **로그**를 선택합니다. 

1. 새 쿼리 1 공간에 다음 KQL 문을 입력합니다.

   >**중요:** 먼저 메모장에 KQL 쿼리를 붙여넣은 다음, 해당 위치에서 새 쿼리 1 로그 창으로 복사하여 오류를 방지하세요.

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize count() by bin(TimeGenerated, 3m), c2
    | where count_ > 5
    | render timechart 
    ```

    ![스크린샷](../Media/SC200_hunting1.png)

1. The goal of the previous KQL query is to provide a visualization for a C2 beaconing on a consistent basis. Adjust grouping of values by changing the <bpt id="p1">*</bpt>3m<ept id="p1">*</ept> setting to <bpt id="p2">**</bpt>30s<ept id="p2">**</ept> within bin() and <bpt id="p3">**</bpt>Run<ept id="p3">**</ept> the query again.

1. Change it back to <bpt id="p1">*</bpt>3m<ept id="p1">*</ept>. Now change the <bpt id="p1">*</bpt>count_<ept id="p1">*</ept> threshold to <bpt id="p2">**</bpt>10<ept id="p2">**</ept> and <bpt id="p3">**</bpt>Run<ept id="p3">**</ept> the query again to witness the impact.

1. You have now identified DNS requests that are beaconing to a C2 server. Next, determine which devices are beaconing. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL Statement:

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

    ![스크린샷](../Media/SC200_hunting2.png)

    >**참고:** 생성된 로그 데이터는 WIN1 디바이스에서만 가져온 것입니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 로그 창을 닫고 **확인**을 선택하여 변경 내용을 취소합니다. 

1. Microsoft Sentinel 작업 영역을 다시 선택하고 위협 관리 영역에서 **헌팅** 페이지를 선택합니다.

1. 명령 모음에서 **+ 새 쿼리**를 선택합니다.

1. 사용자 지정 쿼리 만들기 창의 이름에 **C2 Hunt**를 입력합니다. 

1. *사용자 지정 쿼리*에 다음 KQL 문을 붙여 넣습니다.

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

1. 아래로 스크롤하고 엔터티 매핑(미리 보기)에서 다음을 선택합니다.

    - 엔터티 유형 드롭다운 목록에서 **호스트**를 선택합니다.
    - 식별자 드롭다운 목록에서 **호스트 이름**을 선택합니다.
    - 값 드롭다운 목록에서 **디바이스 이름**을 선택합니다.

1. 아래로 스크롤하고, 전술 & 기술 아래에서 **명령 및 제어** 를 선택한 다음, **만들기**를 선택하여 헌팅 쿼리를 만듭니다.

1. “Microsoft Sentinel - 헌팅” 블레이드의 목록에서 방금 만든 쿼리인 *C2 Hunt*를 검색합니다.

1. 목록에서 **C2 Hunt**를 선택합니다.

1. 오른쪽 창에서 아래로 스크롤하여 **쿼리 실행** 단추를 선택합니다.

1. 당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다.

1. C2 또는 C&C(명령 및 제어) 기술 관련 위협 인텔리전스를 수신했습니다.

1. 결과에서 첫 번째 행의 확인란을 선택합니다. 

1. 가운데 명령 모음에서 **책갈피 추가** 단추를 선택합니다.

1. 기본적으로 채워진 값을 검토하고 책갈피 추가 블레이드에서 **만들기**를 선택합니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 로그 창을 닫고 **확인**을 선택하여 변경 내용을 취소합니다. 

1. Microsoft Sentinel 포털의 헌팅 페이지로 돌아가서 가운데 창에서 **책갈피** 탭을 선택합니다.

1. 결과 목록에서 방금 만든 **C2 Hunt** 책갈피를 선택합니다.

1. 헌트를 수행하고 위협을 감시해야 합니다.

1. 이전 모듈에서와 마찬가지로 조사 그래프를 살펴봅니다.

1. 창의 오른쪽 위에 있는 **X**를 선택하여 조사 그래프 창을 닫고 **확인**을 선택하여 변경 내용을 취소합니다. 

1. **쿼리** 탭을 선택합니다.

1. **C2 Hunt** 쿼리를 다시 검색하고 선택합니다.

1. Right-click your query and select <bpt id="p1">**</bpt>Add to livestream<ept id="p1">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> This also can be done by sliding right and selecting the ellipsis <bpt id="p2">**</bpt>(...)<ept id="p2">**</ept> at the end of the row to open a context menu.

1. **중요:** 랩에서 사용되는 로그 데이터는 이전 모듈에서 작성된 것입니다.


### <a name="task-2-create-a-nrt-query-rule"></a>작업 2: NRT 쿼리 규칙 만들기

연습 5의 WIN1 서버에서 **공격 3**을 참조하세요.


1. Microsoft Sentinel에서 **분석** 페이지를 선택합니다. 

1. **만들기** 탭을 선택한 다음, **NRT 쿼리 규칙**을 선택합니다.
1. This starts the "Analytics rule wizard". For the <bpt id="p1">*</bpt>General<ept id="p1">*</ept> tab type:

    |설정|값|
    |---|---|
    |Name|**NRT C2 헌트**|
    |설명|**NRT C2 헌트**|
    |전술|**명령 및 제어**|
    |심각도|**높음**|

1. **다음: 규칙 논리 설정 >** 단추를 선택합니다. 


1. 규칙 쿼리의 경우 KQL 문을 입력합니다.

    ```KQL
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. Leave the rest of the options with the defaults. Select <bpt id="p1">**</bpt>Next: Incident settings&gt;<ept id="p1">**</ept> button.

1. 인시던트 설정 탭에서 기본값을 그대로 두고 **다음: 자동화된 응답 >** 단추를 선택합니다.

1. 자동화된 응답 탭에서 경고 자동화 아래의 **PostMessageTeams-OnAlert**를 선택한 다음, **다음:  검토** 단추를 클릭합니다.

1. 검토 탭에서 **만들기** 단추를 선택하여 새 예약된 분석 규칙을 만듭니다.



### <a name="task-3-create-a-search"></a>작업 3: 검색 만들기

이 작업에서는 검색 작업을 사용하여 C2를 찾습니다. 


1. Microsoft Sentinel에서 **검색** 페이지를 선택합니다. 

1. **복원** 탭을 선택합니다.

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The lab will not have Archived tables to restore from.  The normal process would restore archived tables to include in the Search job.
1. **취소**를 선택합니다.
1. **검색** 탭을 선택합니다.
1. 테이블을 선택하고 **DeviceRegistryEvents**로 변경합니다.
1. 검색 상자에 **reg.exe**를 입력합니다.  
1. **저장된 검색**을 선택합니다. 
1. 검색 작업은 **DeviceRegistryEvents_####_SRCH**라는 새 테이블을 만듭니다. 
1. Wait for the search job to complete.  The status will display <bpt id="p1">*</bpt>Updating<ept id="p1">*</ept>. Then <bpt id="p1">*</bpt>In progress<ept id="p1">*</ept>. Then <bpt id="p1">*</bpt>Search completed<ept id="p1">*</ept>. 
1. **검색 결과 보기**를 선택합니다.
1. 로그에서 새 탭을 엽니다.
1. 새 테이블 이름인 **DeviceRegistryEvents_####_SRCH**를 입력하고 실행합니다.

## <a name="proceed-to-exercise-2"></a>연습 2 계속 진행
