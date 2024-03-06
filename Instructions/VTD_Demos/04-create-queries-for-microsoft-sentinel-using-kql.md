# 모듈 4 KQL(Kusto 쿼리 언어)을 사용하여 Microsoft Sentinel에 대한 쿼리 만들기

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## KQL 테스트 영역 액세스

이 작업에서는 KQL 문 작성을 연습할 수 있는 Log Analytics 환경에 액세스합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 브라우저에서 https://aka.ms/lademo으로 이동합니다. MOD 관리자 자격 증명을 사용하여 로그인합니다. 

1. 화면 왼쪽 탭에 나열되어 있는 사용 가능한 테이블을 살펴봅니다.

1. 쿼리 편집기에서 다음 쿼리를 입력하고 실행 단추를 선택합니다.  아래쪽 창에서 쿼리 결과가 표시됩니다.

    ```KQL
    SecurityEvent
    ```

1. 첫 번째 레코드 옆에 있는 **>** 을 선택하여 해당 행의 정보를 펼칩니다.

### 작업 2: 기본 KQL 문 실행

이 작업에서는 기본적인 KQL 문을 작성합니다.

1. `search` 연산자는 다중 테이블/다중 열 검색 환경을 제공합니다. 다음 쿼리는`search` 연산자의 사용을 보여 줍니다.

```KQL
search "err" 

search in (SecurityEvent,SecurityAlert,A*) "err"
```

1. `where` 연산자는 조건자를 충족하는 행의 하위 집합으로 테이블을 필터링합니다. 다음 쿼리는`where` 연산자의 사용을 보여 줍니다.

```KQL
SecurityEvent | where EventID in (4624, 4625)

SecurityEvent 
| where TimeGenerated > ago(1d) 

SecurityEvent 
| where TimeGenerated > ago(1h) and EventID == "4624" 

SecurityEvent 
| where TimeGenerated > ago(1h) 
| where EventID == 4624 
| where AccountType =~ "user" 
```

1. 다음 문에는 `let` 문을 사용하여 변수를 선언하는 방법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. 다음 문에는 `let` 문을 사용하여 동적 목록을 선언하는 방법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

1. 다음 문에는 모든 테이블과 열에서 쿼리 창에 표시되는 쿼리 시간 범위 내의 레코드를 검색하는 방법이 나와 있습니다. 쿼리 창에서 이 스크립트를 실행하기 전에 Time 범위를 "Last hour"로 변경합니다. 다음 문을 입력하고 **실행**을 선택합니다.

```KQL
search "err"
```

**경고:** 다음 스크립트를 실행할 때는 TIme 범위를 "Last 24 hours"로 다시 변경해야 합니다.

### 렌더링 연산자를 사용하여 KQL에서 시각화 만들기

이 작업에서는 KQL 문을 사용하여 시각화를 생성합니다.

1. 다음 문에는 막대형 차트를 사용하여 결과를 시각화하는 render 함수 사용법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

1. 다음 문에는 시계열을 사용하여 결과를 시각화하는 render 함수 사용법이 나와 있습니다.

bin() 함수는 주어진 bin 크기의 정수 배수로 값을 반내림합니다.  summarize by... 형식과 함께 자주 사용됩니다. 분산된 값 집합이 있는 경우 값이 특정 값의 더 작은 집합으로 그룹화됩니다.  생성된 시계열과 파이프를 시간 차트 형식의 렌더링 연산자로 결합하면 시계열 시각화가 제공됩니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## 이 데모를 완료했습니다.
