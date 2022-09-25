# <a name="module-4-create-queries-for-microsoft-sentinel-using-kusto-query-language-kql"></a>모듈 4 KQL(Kusto 쿼리 언어)을 사용하여 Microsoft Sentinel에 대한 쿼리 만들기

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## <a name="access-the-kql-testing-area"></a>KQL 테스트 영역 액세스

이 작업에서는 KQL 문 작성을 연습할 수 있는 Log Analytics 환경에 액세스합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

2. Go to <ph id="ph1">https://aka.ms/lademo</ph> in your browser. Login with the MOD Administrator credentials. 

3. 화면 왼쪽 탭에 나열되어 있는 사용 가능한 테이블을 살펴봅니다.

4. In the query editor, enter the following query and select the Run button.  You should see the query results in the bottom window.

    ```KQL
    SecurityEvent
    ```

5. 첫 번째 레코드 옆에 있는 **>** 을 선택하여 해당 행의 정보를 펼칩니다.

### <a name="task-2-run-basic-kql-statements"></a>작업 2: 기본 KQL 문 실행

이 작업에서는 기본적인 KQL 문을 작성합니다.

1. The following statement demonstrates the use of the let statement to declare variables. In the Query Window, enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 


```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. The following statement demonstrates the use of the let statement to declare a dynamic list. In the Query Window enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 


```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

1. The following statement demonstrates searching across all tables and columns for records within the query time range display in the query window. In the Query Window before running this script change the Time range to "Last hour". Enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 

```KQL
search "err"
```

**경고:** 다음 스크립트를 실행할 때는 TIme 범위를 "Last 24 hours"로 다시 변경해야 합니다.

### <a name="create-visualizations-in-kql-with-the-render-operator"></a>Render 연산자를 사용하여 KQL에서 시각화 만들기

이 작업에서는 KQL 문을 사용하여 시각화를 생성합니다.

1. The following statement demonstrates the render function visualizing results with a barchart. In the Query Window. Enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

2. 다음 문에는 시계열을 사용하여 결과를 시각화하는 render 함수 사용법이 나와 있습니다.

브라우저에서 https://aka.ms/lademo으로 이동합니다. 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## <a name="you-have-completed-the-demo"></a>이 데모를 완료했습니다.

