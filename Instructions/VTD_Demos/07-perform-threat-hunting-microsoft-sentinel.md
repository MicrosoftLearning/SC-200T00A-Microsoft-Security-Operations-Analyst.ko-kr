---
ms.openlocfilehash: 6d1aeaf4445af8d38a6fe9f1689771c8243e67ed
ms.sourcegitcommit: 8bd0d3a1384dafb6db097ad5bff4ec65ee8b4d4b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/10/2022
ms.locfileid: "147541858"
---
# <a name="module-7---threat-hunting-in-microsoft-sentinel"></a>모듈 7 - Microsoft Sentinel에서 위협 헌팅

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## <a name="create-a-hunting-query"></a>헌팅 쿼리 만들기

이 작업에서는 헌팅 쿼리를 만들고 결과를 책갈피에 저장한 후 라이브 스트림을 만듭니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd** 를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음** 을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호** 를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인** 을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel* 을 입력하고 **Microsoft Sentinel** 을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. **로그** 를 선택합니다. 

1. 새 쿼리 1 공간에 다음 SQL 문을 입력합니다.

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

1. 이 문은 C2 알림을 일관되게 확인하기 위한 시각화를 제공하는 데 사용됩니다.  3m 설정을 30s로 조정하는 등 문을 조정해 봅니다.  count_ > 5 설정의 임계값 횟수를 다른 값으로 변경하여 결과의 변화를 확인합니다.

1. 지금까지 C2 서버에 알림을 전송하는 DNS 요청을 살펴보았습니다.  다음으로는 알림을 생성하는 디바이스를 확인합니다.  다음 KQL 문을 입력합니다.

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

1. 창의 오른쪽 위에 있는 **X** 를 선택하여 로그 창을 닫고 **확인** 을 선택하여 변경 내용을 취소합니다. 

1. Microsoft Sentinel 포털의 위협 관리 영역에서 **헌팅** 페이지를 선택합니다.

1. 명령 모음에서 **새 쿼리** 를 선택합니다.

1. 사용자 지정 쿼리 만들기 창의 이름에 **C2 Hunt** 를 입력합니다. 

1. *사용자 지정 쿼리* 에 다음 KQL 문을 붙여 넣습니다.

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

    - 엔터티 유형 드롭다운 목록에서 **호스트** 를 선택합니다.
    - 식별자 드롭다운 목록에서 **호스트 이름** 을 선택합니다.
    - 값 드롭다운 목록에서 **디바이스 이름** 을 선택합니다.

1. 아래로 스크롤하고, 전술 & 기술 아래에서 **명령 및 제어** 를 선택한 다음, **만들기** 를 선택하여 헌팅 쿼리를 만듭니다.

1. “Microsoft Sentinel - 헌팅” 블레이드의 목록에서 방금 만든 쿼리인 *C2 Hunt* 를 검색합니다.

1. 목록에서 **C2 Hunt** 를 선택합니다.

1. 오른쪽 창에서 아래로 스크롤하여 **쿼리 실행** 단추를 선택합니다.

1. 결과 열 아래의 가운데 창에 결과 수가 표시됩니다. 또는 위로 스크롤하여 결과 상자의 개수를 확인합니다.

1. **결과 보기** 를 선택합니다.

1. 결과의 첫 번째 행을 선택합니다. 

1. **책갈피 추가** 를 선택합니다.

1. 표시되는 창에서 **만들기** 를 선택합니다.

1. Microsoft Sentinel 포털의 헌팅 페이지로 돌아옵니다.

1. **책갈피** 탭을 선택합니다.

1. 결과 목록에서 책갈피를 선택합니다.

1. 플라이아웃 창에서 **조사** 를 선택합니다.

1. 조사 그래프를 살펴봅니다.

1. Microsoft Sentinel 포털의 헌팅 페이지로 돌아옵니다.

1. **쿼리** 탭을 선택합니다.

1. **C2 Hunt** 쿼리를 선택합니다.

1. 행 끝부분의 **...** 를 선택하여 상황에 맞는 메뉴를 엽니다.

1. **라이브 스트림에 추가** 를 선택합니다.

## <a name="you-have-completed-the-demo"></a>이 데모를 완료했습니다.