---
ms.openlocfilehash: 9267efde7b1d184fa4201ba07be947ffff21311e
ms.sourcegitcommit: 6934bbcd5d9774aa44dd949cf9523e8a43a505d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2022
ms.locfileid: "147168466"
---
# <a name="module-4-configure-your-microsoft-sentinel-environment"></a>모듈 4 Microsoft Sentinel 환경 구성

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## <a name="explore-the-microsoft-sentinel-interface"></a>Microsoft Sentinel 인터페이스 살펴보기

1. [필수 구성 요소](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4) 섹션을 완료하는 동안 이전에 만든 Microsoft Sentinel 인터페이스로 돌아갑니다.

1. 새로 만든 Microsoft Sentinel 작업 영역 내를 이동하면서 사용자 인터페이스 옵션을 숙지합니다.

## <a name="create-a-watchlist"></a>관심 목록 만들기

이 작업에서는 관심 목록을 만듭니다.

1. 화면 아래쪽의 검색 상자에 `Notepad`를 입력합니다.  결과에서 **메모장** 을 선택합니다.

1. `Hostname`을 입력한 다음 새 줄을 입력합니다.

1. 2~6행에 다음 호스트 이름을 추가합니다.
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. 메뉴에서 **파일 - 다른 이름으로 저장** 을 선택하고 파일 이름을 `HighValue.csv`로 지정합니다.  그런 후에 파일 형식을 **모든 파일( *.* )** 로 변경합니다.  그런 다음 **저장** 을 선택합니다.

1. 메모장을 닫습니다.

1. Microsoft Sentinel의 **내 관심 목록** 영역에서 **관심 목록** 옵션을 선택합니다.

1. 명령 모음에서 **새로 추가** 를 선택합니다.

1. 관심 목록 마법사에 다음 정보를 입력합니다.  이름: HighValueHosts  설명: 중요 호스트  관심 목록 별칭: HighValueHosts

1. **다음: 원본 >** 을 선택합니다.

1. 방금 만든 `HighValue.csv` 파일을 찾습니다. 

1. CSV 파일이 로드되면 **SearchKey 필드** 드롭다운에서 상자에서 **Hostname** 을 선택합니다.

1. **다음: 검토 및 만들기 >** 를 선택합니다.

1. **만들기** 를 선택합니다.

1. 화면에 관심 목록 목록이 다시 표시됩니다.

1. 새 관심 목록을 선택합니다.  오른쪽 탭에서 **Log Analytics에서 보기** 를 선택합니다.

1. 다음 KQL 문이 자동 실행되고 결과가 표시됩니다.

```KQL
_GetWatchlist('HighValueHosts')
```
**참고** 가져오기가 완료되려면 시간이 다소 걸릴 수 있습니다.

이제 KQL 문에서 _GetWatchlist('HighValueHosts')를 사용하여 목록에 액세스할 수 있습니다. 참조할 열은 *Hostname* 입니다.

## <a name="create-a-threat-indicator"></a>위협 표시기 만들기

이 작업에서는 표시기를 만듭니다.

1. Microsoft Sentinel의 **위협 관리** 영역에서 **위협 인텔리전스** 옵션을 선택합니다.

1. 명령 모음에서 **새로 추가** 를 선택합니다.

1. 유형 드롭다운에서 사용 가능한 여러 표시기 유형을 검토합니다.  그런 후에 **domain-name** 을 선택합니다. 도메인 상자에 이니셜을 입력합니다. 예를 들어 fmg.com 등을 입력할 수 있습니다.

1. 위협 유형에 대해 **+ 추가** 를 선택하고 **악의적 활동** 을 복사하여 필드에 붙여넣습니다.

1. 이름에는 도메인에 사용한 것과 같은 값을 입력합니다. 예를 들어 fmg.com 등을 입력할 수 있습니다.

1. **유효 기간(시작)** 필드의 값을 오늘 날짜로 설정합니다.

1. **적용** 을 선택합니다.

**참고** 표시기가 표시되려면 시간이 다소 걸릴 수 있습니다.

1. 일반 영역에서 **로그** 옵션을 선택합니다.  쿼리 창을 표시하려면 "항상 쿼리 표시" 옵션을 사용하지 않도록 설정해야 할 수도 있습니다.

1. 다음 KQL 문을 실행합니다.

```KQL
ThreatIntelligenceIndicator 
```
결과를 오른쪽으로 스크롤하여 DomainName 열을 확인합니다. 다음 KQL 문을 실행하여 DomainName 열만 표시할 수도 있습니다.  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## <a name="you-have-completed-the-demo"></a>이 데모를 완료했습니다.