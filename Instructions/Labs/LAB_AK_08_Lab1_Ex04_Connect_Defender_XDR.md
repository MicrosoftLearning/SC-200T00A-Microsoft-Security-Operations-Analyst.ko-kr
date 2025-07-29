---
lab:
  title: 연습 4 - 데이터 커넥터를 사용하여 Defender XDR을 Microsoft Sentinel에 연결
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# 학습 경로 8 - 랩 1 - 연습 4 - 데이터 커넥터를 사용하여 Defender XDR을 Microsoft Sentinel에 연결

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex4.png)

Microsoft Defender XDR과 Microsoft Sentinel을 모두 배포한 회사에서 근무하는 보안 운영 분석가라고 가정합니다. Microsoft Sentinel을 Defender XDR에 연결하는 통합 보안 운영 플랫폼을 준비해야 합니다. 다음 단계는 Defender XDR Content Hub 솔루션을 설치하고 Defender XDR 데이터 커넥터를 Microsoft Sentinel에 배포하는 것입니다.

>**참고:** 이 연습의 환경은 제품에서 생성된 시뮬레이션입니다. 제한된 시뮬레이션으로 페이지의 링크가 사용하도록 설정되지 않을 수 있으며 지정된 스크립트를 벗어나는 텍스트 기반 입력은 지원되지 않을 수 있습니다. "이 기능은 시뮬레이션 내에서 사용할 수 없습니다."라는 팝업 메시지가 표시됩니다. 이 경우 확인을 선택하고 연습 단계를 계속합니다.

![팝업 오류 메시지](../Media/simulation-pop-up-error.png)

### 작업 1: Defender XDR 연결

이 작업에서는 Microsoft Defender XDR 커넥터를 배포합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저에서 다음 링크를 선택하여 시뮬레이트된 환경을 엽니다. [Azure Portal]( https://app.highlights.guide/start/1c894b46-4b0a-40cb-b0f0-1e1c86c615f3?token=16d48b6c-eace-4a1f-8050-098d29d23a89).

1. Azure Portal *홈* 페이지에서 **Microsoft Sentinel** 아이콘을 선택합니다.

1. *Microsoft Sentinel* 페이지에서 **Woodgrove-LogAnalyiticWorkspace** 작업 영역을 선택합니다.

1. Microsoft Sentinel 왼쪽 메뉴에서 **콘텐츠 관리** 섹션까지 아래로 스크롤하고 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **Microsoft Defender XDR** 솔루션을 검색하고 목록에서 선택합니다.

1. *Microsoft Defender XDR* 솔루션 세부 정보 페이지에서 **설치**를 선택합니다.

1. 설치가 완료되면 **Microsoft Defender XDR** 솔루션을 검색하여 선택합니다.

1. *Microsoft Defender XDR* 솔루션 세부 정보 페이지에서 **관리** 선택

1. *Microsoft Defender XDR* 데이터 커넥터 확인란을 선택하고 **커넥터 페이지 열기**를 선택합니다.

1. 연결이 성공했다는 메시지가 표시됩니다.

### 작업 2: Microsoft Sentinel 및 Microsoft Defender XDR 연결

이 작업에서는 시뮬레이션을 계속하고 Microsoft Sentinel 작업 영역을 Microsoft Defender XDR에 연결합니다.

1. 페이지 맨 위에 있는 "이동 경로 탐색" 메뉴 링크를 사용하여 Microsoft Sentinel *콘텐츠 허브*로 돌아가서 탐색 메뉴 일반 섹션에서 **개요(미리 보기)** 를 선택합니다.

1. *한곳에 SIEM 및 XDR 가져오기* 메시지에서 **자세한 정보** 단추를 선택합니다.

1. **자세한 정보** 단추를 선택하면 *Microsoft Defender XDR* 포털의 브라우저에서 새 탭이 열립니다.

1. **Defender Defender** 포털 **홈** 화면 위쪽에 *한곳에 SIEM 및 XDR 가져오기* 메시지와 함께 배너가 표시됩니다. **작업 영역 연결** 단추를 선택합니다.

1. *작업 영역 선택* 페이지에서 **woodgrove-loganalyiticsworkspace** Microsoft Sentinel 작업 영역을 선택합니다.

1. **다음** 단추를 선택합니다.

1. **기본 작업 영역 설정** 페이지의 드롭다운 메뉴에 **woodgrove-loganalyiticsworkspace** Microsoft Sentinel 작업 영역이 표시됩니다. **다음** 단추를 선택합니다.

1. *검토 및 완료* 페이지에서 *작업 영역* 선택 항목이 올바른지 확인하고 *작업 영역이 연결되면 예상되는 사항* 아래에 있는 글머리 기호 항목을 검토합니다. **연결** 단추를 선택합니다.

1. *작업 영역에 연결하려고 합니다.* 메시지가 표시됩니다. **연결** 단추를 선택합니다.

1. 이제 *작업 영역이 연결됨* 페이지에 있어야 합니다.

1. **닫기** 버튼을 선택합니다.

1. **Defender XDR** 포털의 **홈** 화면에서 *통합 SIEM 및 XDR이 준비됨*이라는 메시지와 함께 맨 위에 배너가 표시됩니다. **헌팅 시작** 단추를 선택합니다.

1. *고급 헌팅*에서 "Microsoft Sentinel에서 콘텐츠 탐색"이라는 메시지가 표시됩니다. *고급 헌팅* 탐색 메뉴의 해당 탭 아래에서 *Microsoft Sentinel* 테이블, 함수 및 쿼리를 찾을 수 있습니다.

1. **스키마** 탭 아래로 스크롤하여 **Microsoft Sentinel** 제목으로 이동한 다음, **ThreatIntelligenceIndicator** 테이블을 두 번 클릭합니다.

1. *쿼리* 창에 위협 인텔리전스 지표를 반환하는 (KQL) 쿼리가 표시됩니다. **쿼리 실행** 단추를 선택합니다.

1. 결과가 *결과* 창에 표시됩니다.

1. 축소된 경우 왼쪽 주 메뉴 창을 확장하고 새 **Microsoft Sentinel** 메뉴 항목을 확장합니다. *검색*, *위협 관리*, *콘텐츠 관리* 및 *구성 * 선택 항목이 표시됩니다.

    >**참고:** Azure Microsoft Sentinel 포털과 Microsoft Defender XDR 포털의 Sentinel 간에는 기능 차이**[포털 기능 차이](https://learn.microsoft.com/azure/sentinel/microsoft-sentinel-defender-portal#capability-differences-between-portals)** 가 있습니다.

1. Microsoft Defender XDR **Microsoft Sentinel** 메뉴 항목에서 **구성**, **데이터 커넥터**를 차례로 선택합니다.

1. *데이터 커넥터* 페이지에 **연결된 상태**의 기타 데이터 커넥터와 **Azure 활동**이 표시됩니다.

>**참고:** 다른 Microsoft Sentinel 기능을 자유롭게 탐색하고 비교할 수 있지만 시뮬레이션이므로 Microsoft Defender 포털에서 Microsoft Sentinel을 탐색하는 기능은 제한적입니다. 실제 환경에서는 Microsoft Defender 포털에서 전체 Microsoft Sentinel 기능을 탐색할 수 있습니다.

## 랩이 끝났습니다. 학습 경로 9 - 랩 1 - 연습 1 - Microsoft 보안 규칙 수정을 계속 진행하세요.
