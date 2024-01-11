# 모듈 7 - Microsoft Sentinel에서 위협 헌팅

**참고** 이 데모의 성공적인 완료는 필수 구성 요소 문서의[ 모든 단계를 ](00-prerequisites.md)완료하는 데 따라 달라집니다. 

## 헌팅 쿼리 만들기

이 작업에서는 헌팅 쿼리를 만들고, 결과를 책갈피로 지정하고, Livestream을 만듭니다.

1. 암호를 사용하여 관리 WIN1 가상 머신에 로그인합니다 **. Pa55w.rd**.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. **로그인 대화 상자에서** 랩 호스팅 공급자가 **제공한 테넌트 전자 메일** 계정을 복사하여 붙여넣은 다음을 선택합니다****.

1. **암호** 입력 대화 상자에서 랩 호스팅 공급자가 **제공한 테넌트 암호를** 복사하여 붙여넣은 다음, 로그인을** 선택합니다**.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. 로그 선택 **** 

1. {b>새 쿼리 1<b} 공간에 다음 KQL 문을 입력합니다.

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

1. 이 문의 목표는 C2 비콘을 일관되게 검사 시각화를 제공하는 것입니다.  시간을 내어 3m 설정을 30대 이상으로 조정합니다.  count_ > 5 설정의 임계값 횟수를 다른 값으로 변경하여 결과의 변화를 확인합니다.

1. 이제 C2 서버로 비콘을 표시하는 DNS 요청을 식별했습니다.  다음으로, 어떤 디바이스가 비콘을 수신하는지 확인합니다.  다음 KQL 문을 입력합니다.

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

**참고** 생성된 로그 데이터는 온보딩된 디바이스에서만 가져온 것입니다.

1. 창의 *오른쪽 위에 있는 X**를 **선택하여 로그* 창을 닫고 확인을 선택하여 **** 변경 내용을 카드. 

1. Microsoft Sentinel 포털의 위협 관리 영역에서 **헌팅** 페이지를 선택합니다.

1. 명령 모음에서 새 쿼리**를 선택합니다**.

1. 사용자 지정 쿼리* 만들기 창에서 *이름* 형식 **C2 Hunt에 *대해**

1. 사용자 지정 쿼리*의 *경우 다음 KQL 문을 입력합니다.

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

1. 아래로 스크롤하고 엔터티 매핑(미리 보기)* 아래에서 *다음을 선택합니다.

    - *엔터티 유형* 드롭다운 목록에서 호스트**를 선택합니다**.
    - *식별자* 드롭다운 목록에서 HostName을** 선택합니다**.
    - *값* 드롭다운 목록에서 DeviceName을** 선택합니다**.

1. 아래로 스크롤하여 전술 및 기술 아래에서 *명령 및 제어**를 선택한 **다음 만들기**를 선택하여 **헌팅 쿼리를 만듭니*다.

1. *"Microsoft Sentinel - 헌팅"* 블레이드에서 목록에서 방금 만든 쿼리인 *C2 Hunt*를 검색합니다.

1. 목록에서 **C2 Hunt**를 선택합니다.

1. 오른쪽 창에서 아래로 스크롤하여 **쿼리 실행** 단추를 선택합니다.

1. 결과 열 아래의 가운데 창에 ** 결과 수가 표시됩니다. 또는 위로 스크롤하여 결과* 상자의 *개수를 확인합니다.

1. 결과** 보기를 선택합니다**.

1. 결과에서 첫 번째 행을 선택합니다. 

1. **북마크 추가**를 선택합니다.

1. 표시되는 창에서 만들기**를 선택합니다**.

1. Microsoft Sentinel 포털의 헌팅 페이지로 돌아옵니다.

1. **책갈피 탭을** 선택합니다.

1. 결과 목록에서 책갈피를 선택합니다.

1. 플라이아웃 창에서 조사를** 선택합니다**.

1. 조사 그래프를 탐색합니다.

1. Microsoft Sentinel 포털의 헌팅 페이지로 돌아옵니다.

1. **쿼리** 탭 선택

1. C2 헌트** 쿼리를 **선택합니다.

1. 행 끝부분의 **...** 를 선택하여 상황에 맞는 메뉴를 엽니다.

1. 라이브 스트림**에 추가를 선택합니다**.

## 데모를 완료했습니다.