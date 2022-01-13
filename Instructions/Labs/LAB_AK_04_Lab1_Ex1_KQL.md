---
lab:
    title: '연습 1 - KQL(Kusto Query Language)을 사용하여 Microsoft Sentinel용 쿼리 만들기'
    module: '모듈 4 - KQL(Kusto Query Language)을 사용하여 Microsoft Sentinel용 쿼리 만들기'
---

# 모듈 4 - 랩 1 - 연습 1 - KQL(Kusto Query Language)을 사용하여 Microsoft Sentinel용 쿼리 만들기

## 랩 시나리오
여러분은 Microsoft Sentinel을 구현하는 중인 회사에서 일하는 보안 작업 분석가입니다. 로그 데이터 분석을 수행하여 악의적인 활동을 검색하고 시각화를 표시하고 위협 헌팅을 수행할 책임이 있습니다. 로그 데이터를 쿼리하려면 KQL(Kusto Query Language)을 사용합니다.

>**힌트:** 이 랩에서는 Microsoft Sentinel에 많은 KQL 스크립트를 입력합니다. 스크립트는 이 랩을 시작할 때 파일로 제공되었습니다. 다음 위치에서 스크립트를 다운로드할 수 있습니다.  https://github.com/MicrosoftLearning/SC-200T00KO-Microsoft-Security-Operations-Analyst/tree/master/Allfiles


### 작업 1: KQL 테스트 영역 액세스

이 작업에서는 KQL 문 작성을 연습할 수 있는 Log Analytics 환경에 액세스합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 브라우저에서 https://aka.ms/lademo 로 이동합니다. MOD 관리자 자격 증명을 사용하여 로그인합니다. 

3. 화면 왼쪽 탭에 나열되어 있는 사용 가능한 테이블을 살펴봅니다.

4. 쿼리 편집기에서 다음 쿼리를 입력하고 **실행** 단추를 선택합니다.  아래쪽 창에서 쿼리 결과가 표시됩니다.

```KQL
SecurityEvent
```

5. 첫 번째 레코드 다음의 **>** 를 선택하여 해당 행의 정보를 확장합니다.


### 작업 2: 기본 KQL 문 실행

이 작업에서는 기본적인 KQL 문을 작성합니다.

>**중요:**  각 쿼리에 대해 쿼리 창에서 이전 문을 지우거나, 마지막으로 연 탭 후에 **+** 를 선택함으로써 새 쿼리 창을 엽니다(최대 25개).

1. 다음 문에는 let 문을 사용하여 변수를 선언하는 방법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

2. 다음 문에는 let 문을 사용하여 동적 목록을 선언하는 방법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

3. 다음 문에는 "let" 문을 사용하여 동적 테이블을 선언하는 방법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
let LowActivityAccounts =
    SecurityEvent 
    | summarize cnt = count() by Account 
    | where cnt < 10;
LowActivityAccounts | where Account contains "sql"
```

4. 다음 문에는 모든 테이블과 열에서 쿼리 창에 표시되는 쿼리 시간 범위 내의 레코드를 검색하는 방법이 나와 있습니다. 쿼리 창에서 이 스크립트를 실행하기 전에 **Time range**를 "Last hour"로 변경합니다. 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
search "err"
```

>**경고:** 다음 스크립트를 실행할 때는 Time 범위를 "Last 24 hours"로 다시 변경해야 합니다.

5. 다음 문에는 "in" 절을 사용하여 나열한 테이블에서 쿼리 창에 표시되는 쿼리 시간 범위 내의 레코드를 검색하는 방법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
search in (SecurityEvent,SecurityAlert,A*) "err"
```

6. 다음 문에는 where 연산자를 사용하는 필터 사용 방식이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

    >**참고:** 아래의 각 코드 블록에서 쿼리를 입력한 후 "실행"을 선택해야 합니다.

```KQL
SecurityEvent
| where TimeGenerated > ago(1d)
```

```KQL
SecurityEvent
| where TimeGenerated > ago(1h) and EventID == "4624"
```

```KQL
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4624
| where AccountType =~ "user"
```

```KQL
SecurityEvent | where EventID in (4624, 4625)
```

7. 다음 문에는 쿼리 창에서 extend 연산자를 사용하여 필드를 만드는 방법이 나와 있습니다. 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
```

8. 다음 문에는 order by 연산자를 사용하여 결과를 정렬하는 방법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
| order by severityOrder desc
```

9. 다음 문에는 프로젝트 연산자를 사용하여 결과 집합을 필드를 지정하는 방법이 나와 있습니다.

    >**참고:** 아래의 각 코드 블록에서 쿼리를 입력한 후 "실행"을 선택해야 합니다.

쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent
| project Computer, Account
```

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
| order by severityOrder
| project-away severityOrder
```


### 작업 3: Summarize 연산자를 사용하여 KQL에서 결과 분석

이 작업에서는 데이터를 준비하는 KQL 문을 작성합니다.

1. 다음 문에는 count 함수 사용법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent
| where EventID == "4688"
| summarize count() by Process, Computer
```

2. 다음 문에는 count 함수 사용법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4624
| summarize cnt=count() by AccountType, Computer
```

3. 다음 문에는 dcount 함수 사용법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent
| summarize dcount(IpAddress)
```

4. 다음 문에는 arg_max 함수 사용법이 나와 있습니다.

다음 문은 컴퓨터 SQL12.NA.contosohotels.com에 대한 SecurityEvent 테이블에서 최신 행을 반환합니다.  arg_max 함수의 *는 해당 행의 모든 열을 요청합니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent 
| where Computer == "SQL12.na.contosohotels.com"
| summarize arg_max(TimeGenerated,*) by Computer
```

5. 다음 문에는 arg_min 함수 사용법이 나와 있습니다.

이 문에서는 컴퓨터 SQL12.NA.contosohotels.com의 가장 오래된 SecurityEvent가 결과 집합으로 반환됩니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent 
| where Computer == "SQL12.na.contosohotels.com"
| summarize arg_min(TimeGenerated,*) by Computer
```

6. 다음 문에는 파이프 "|"의 순서를 기준으로 결과를 파악해야 하는 이유가 나와 있습니다. 쿼리 창에서 다음 쿼리를 입력하고 각 문을 개별적으로 실행합니다. 

**쿼리 1**에는 마지막 작업이 로그인이었던 계정이 있습니다. 먼저 SecurityEvent 테이블이 요약되고 각 계정에 대한 최신 행이 반환됩니다.  그런 다음 EventID가 4624(로그인)인 행만 반환됩니다.

```KQL
SecurityEvent
| summarize arg_max(TimeGenerated, *) by Account
| where EventID == "4624"
```

**쿼리 2**에는 로그인된 계정의 가장 최근 로그인이 있습니다. SecurityEvent 테이블은 EventID = 4624만 포함하도록 필터링됩니다. 그러면 해당 결과가 계정별로 최신 로그인 행에 대해 요약됩니다.

```KQL
SecurityEvent
| where EventID == "4624"
| summarize arg_max(TimeGenerated, *) by Account
```

>**참고:**  "Completed." 막대를 선택하고 두 문 간에 데이터를 비교함으로써 "Total CPU" 및 "Data used for processed query"를 검토할 수도 있습니다.

7. 다음 문에는 make_list 함수 사용법이 나와 있습니다.

make_list 함수는 그룹에 있는 식의 모든 값에 대한 동적(JSON) 배열을 반환합니다. 이 KQL 쿼리는 먼저 where 연산자를 사용하여 EventID를 필터링합니다.  그런 다음 각 컴퓨터에서 결과는 계정의 JSON 배열입니다. 결과 JSON 배열에는 중복된 계정이 포함됩니다.

쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent
| where EventID == "4624"
| summarize make_list(Account) by Computer
```

8. 다음 문에는 make_set 함수 사용법이 나와 있습니다.

make_set 함수는 식이 그룹으로 가져오는 *개별* 값이 포함된 동적(JSON) 배열을 반환합니다. 이 KQL 쿼리는 먼저 where 연산자를 사용하여 EventID를 필터링합니다.  그런 다음 각 컴퓨터에서 결과는 고유한 계정의 JSON 배열입니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent
| where EventID == "4624"
| summarize make_set(Account) by Computer
```


### 작업 4: Render 연산자를 사용하여 KQL에서 시각화 만들기

이 작업에서는 KQL 문을 사용하여 시각화를 생성합니다.

1. 다음 문에는 막대형 차트를 사용하여 결과를 시각화하는 render 함수 사용법이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

2. 다음 문에는 시계열을 사용하여 결과를 시각화하는 render 함수 사용법이 나와 있습니다.

bin() 함수는 주어진 bin 크기의 정수 배수로 값을 반내림합니다.  summarize by... 형식과 함께 자주 사용됩니다. 분산된 값 집합이 있는 경우 값이 특정 값의 더 작은 집합으로 그룹화됩니다.  생성된 시계열과 파이프를 시간 차트 형식의 렌더링 연산자로 결합하면 시계열 시각화가 제공됩니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1h) 
| render timechart
```


### 작업 5: KQL에서 다중 테이블 문 작성

이 작업에서는 다중 테이블 KQL 문을 작성합니다.

1. 다음 문에는 테이블 두 개 이상을 가져온 다음 모든 테이블의 행을 반환하는 union 연산자의 사용법이 나와 있습니다. 결과가 파이프 문자에 어떻게 전달되고 영향을 받는지 이해하는 것은 중요합니다. 쿼리 창에서 다음 문을 입력하고 각각에 대해 **실행**을 선택하여 결과를 봅니다. 

**쿼리 1**은 SecurityEvent의 모든 행과 SecurityAlert의 모든 행을 반환합니다.

```KQL
SecurityEvent 
| union SecurityAlert  
```

**쿼리 2**는 SecurityEvent의 모든 행과 SecurityAlert의 모든 행의 수인 행 1개와 열 1개를 반환합니다.

```KQL
SecurityEvent 
| union SecurityAlert  
| summarize count() 
| project count_
```

**쿼리 3**은 SecurityEvent의 모든 행과 SecurityAlert의 하나의 행을 반환합니다.  SecurityAlert의 행에는 SecurityAlert 행의 수가 포함됩니다.

```KQL
SecurityEvent 
| union (SecurityAlert  | summarize count()) 
| project count_
```

2. 다음 문에는 union 연산자가 여러 테이블을 통합하는 와일드카드를 지원하는 방식이 나와 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
union Security* 
| summarize count() by Type
```

3. 다음 문에는 join 연산자의 사용법이 나와 있습니다. join 연산자는 두 테이블의 행을 병합한 다음 각 테이블에서 지정된 열의 값 일치 여부를 확인하여 새 테이블을 생성합니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
SecurityEvent 
| where EventID == "4624" 
| summarize LogOnCount=count() by EventID, Account 
| project LogOnCount, Account 
| join kind = inner (
     SecurityEvent 
     | where EventID == "4634" 
     | summarize LogOffCount=count() by EventID, Account 
     | project LogOffCount, Account 
) on Account
```

조인에서 지정된 첫 번째 테이블은 왼쪽 테이블로 간주됩니다.  조인 키워드 뒤의 테이블은 오른쪽 테이블입니다.  테이블의 열로 작업을 할 때는 참조 대상 테이블 열을 구분하기 위해 $left.Column name 이름 및 $right.Column 이름을 사용합니다. 


### 작업 6: KQL에서 문자열 데이터 작업

이 작업에서는 KQL 문을 사용하여 구조화된 문자열 필드 및 구조화되지 않은 문자열 필드 작업을 수행합니다.

1. 다음 문에는 extract 함수 사용법이 나와 있습니다.  텍스트 문자열에서 정규식에 일치하는 항목을 추출합니다. 추출된 하위 문자열을 지정된 형식으로 변환하는 옵션이 있습니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
print extract("x=([0-9.]+)", 1, "hello x=45.6|wo") == "45.6"
```

2. 다음 문에서는 extract 함수를 사용하여 SecurityEvent 테이블의 Account 필드에서 Account Name을 가져옵니다. 쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
let top3 = SecurityEvent
| where TimeGenerated > ago(1h)
| where AccountType == 'User'
| extend Account_Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account))
| summarize Attempts = count() by Account_Name
| where Account_Name != ""
| top 3 by Attempts 
| summarize make_list(Account_Name);
SecurityEvent
| where TimeGenerated > ago(1h)
| where AccountType == 'User'
| extend Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account))
| extend Account_Name = iff(Name in (top3), Name, "Other")
| where Account_Name != ""
| summarize Attempts = count() by Account_Name
| sort by Attempts
```

3. 다음 문에는 parse 함수 사용법이 나와 있습니다. parse 함수는 문자열 식을 평가하고 해당 값을 계산 열 하나 이상으로 구문 분석합니다. 계산된 열에는 구문 분석에 실패한 문자열에 대한 Null이 포함됩니다.

```KQL
let Traces = datatable(EventText:string)
[
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=23, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=15, lockTime=02/17/2016 08:40:00, releaseTime=02/17/2016 08:40:00, previousLockTime=02/17/2016 08:39:00)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=20, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=22, lockTime=02/17/2016 08:41:01, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=16, lockTime=02/17/2016 08:41:00, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:00)"
];
Traces  
| parse EventText with * "resourceName=" resourceName ", totalSlices=" totalSlices:long * "sliceNumber=" sliceNumber:long * "lockTime=" lockTime ", releaseTime=" releaseTime:date "," * "previousLockTime=" previousLockTime:date ")" *  
| project resourceName, totalSlices, sliceNumber, lockTime, releaseTime, previousLockTime
```

4. 다음 문에는 동적 필드 사용법이 나와 있습니다.

Log Analytics 테이블에는 동적으로 정의된 필드 형식이 있습니다. 동적 필드에는 키-값 쌍이 포함되어 있습니다.

동적 필드 내의 문자열에 액세스하기 위해 점 표기법을 사용합니다. AppAvailabilityResults 테이블의 Properties 필드는 동적 형식입니다. 해당 예제에서는, SyntheticMonitorId의 Properties.SyntheticMonitorId 필드 이름에 액세스할 수 있습니다.

쿼리 창에서 다음 문을 입력하고 **실행**을 선택합니다. 

```KQL
AppAvailabilityResults
| project Properties.SyntheticMonitorId
```

5. 다음 문에는 문자열 필드에 저장된 JSON을 조작하는 함수가 나와 있습니다. 많은 로그는 JSON 형식으로 데이터를 전송합니다. 해당 경우에는 JSON 데이터를 쿼리 가능한 필드로 변환하는 방법을 알아야 합니다. 

쿼리 창에서 다음 문을 각각 입력하고 **실행**을 선택합니다. 

```KQL
SecurityAlert
| extend ExtendedProperties = todynamic(ExtendedProperties) 
| extend ActionTaken = ExtendedProperties.ActionTaken
| extend AttackerIP = ExtendedProperties["Attacker IP"]
```
mv-expand 연산자는 다중 값 동적 배열 또는 속성 모음을 여러 개의 레코드로 확장합니다.

```KQL
SecurityAlert
| mv-expand entity = todynamic(Entities)
```
mv-apply 연산자는 각 레코드에 하위 쿼리를 적용하고 모든 하위 쿼리 결과의 합집합을 반환합니다.

```KQL
SecurityAlert
| where TimeGenerated >= ago(7d)
| mv-apply entity = todynamic(Entities) on 
( where entity.Type == "account" | extend account = strcat (entity.NTDomain, "\\", entity.Name))
```

6. 함수를 만들려면

    >**참고:** 이 랩의 데이터에 사용되는 랩 데모 환경에서는 함수를 만들 수 없습니다. 하지만 함수는 랩 환경에서 사용할 중요한 개념이므로 숙지해 두어야 합니다. 

쿼리를 실행한 후 **저장 단추** 단추를 선택하고 드롭다운에서 **함수로 저장**을 선택합니다. 원하는 이름(예: *MailboxForward*)을 **함수 이름** 상자에 입력하고 *일반*과 같은 **레거시 범주**를 입력한 다음 **저장**을 선택합니다.

KQL에서 함수 별칭을 통해 함수를 사용할 수 있습니다.

```KQL
MailboxForward
```

## 이 랩을 완료했습니다.
