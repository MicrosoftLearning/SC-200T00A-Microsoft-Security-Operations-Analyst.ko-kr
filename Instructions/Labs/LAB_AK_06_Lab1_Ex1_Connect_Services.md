---
lab:
  title: 연습 1 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 데이터 연결
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# 학습 경로 6 - 랩 1 - 연습 1 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 데이터 연결

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 조직에 있는 많은 데이터 원본의 로그 데이터를 연결하는 방법을 알아야 합니다. 조직에는 Microsoft 365, Microsoft 365 Defender, Azure 리소스, 비 Azure 가상 머신 등의 데이터가 있습니다. 먼저 Microsoft 원본 연결을 시작합니다.

>**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Connect%20data%20to%20Microsoft%20Sentinel%20using%20data%20connectors)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 


### 작업 1: Microsoft Sentinel 작업 영역에 액세스

이 작업에서는 Microsoft Sentinel 작업 영역에 액세스합니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저를 엽니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 이전 랩에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 탐색 메뉴에서 분석을 선택합니다.

1. 규칙 템플릿에서 클라우드용 Microsoft Defender* 따라 인시던트 만들기를 선택합니다*.

1. 규칙 정보 창에서 규칙** 만들기를 선택하거나 줄임표(...) 및 **+ 규칙** 만들기를 선택합니다**.

1. 분석 규칙 마법사에서 다음: 자동화된 응답을 선택한 **다음, 다음: 검토 및 만들기**를 선택합니다**.**

1. **저장**을 선택합니다.

### 작업 2: 클라우드용 Microsoft Defender 데이터 커넥터 커넥트

이 작업에서는 클라우드용 Microsoft Defender 데이터 커넥터를 연결합니다.

1. Microsoft Sentinel 왼쪽 메뉴에서 콘텐츠 관리 섹션까지 *아래로 스크롤하고 콘텐츠 허브**를 선택합니다**.*

1. 콘텐츠 허브*에서 *클라우드용 Microsoft Defender** 솔루션을 검색**하고 목록에서 선택합니다.

1. *클라우드용 Microsoft Defender* 솔루션 세부 정보 페이지에서 설치**를 선택합니다**.

1. 설치가 완료되면 클라우드용 Microsoft Defender** 솔루션을 검색**하여 선택합니다.

1. *클라우드용 Microsoft Defender* 솔루션 세부 정보 페이지에서 관리 선택 ****

    >**참고:** 클라우드용 Microsoft Defender 솔루션은 *구독 기반 클라우드용 Microsoft Defender(레거시)* 데이터 커넥터, *테넌트 기반 클라우드용 Microsoft Defender(미리 보기)* 데이터 커넥터 및 분석 규칙을 설치 ** 합니다.

1. *구독 기반 클라우드용 Microsoft Defender(레거시)* 데이터 커넥터 검사 상자를 선택하고 커넥터 열기 페이지를** 선택합니다**.

1. 구성* 섹션의 ** 지침* 탭**에서 "Azure Pass - 스폰서쉽" 구독의 검사 상자를 선택하고** 상태** 옵션을 오른쪽으로 밉**니다.

    >**참고:** 연결이 끊긴 것으로 다시 전환되는 경우 학습 경로 3, 연습 1, 작업 1을 검토하여 계정에 적절한 권한을 할당하세요.

1. *이제 **상태가* 커넥트** "양방향 동기화"를 사용하도록 설정*해야 *합니다.

    <!--- 1. Scroll down and under the *Create incidents - Recommended!* area, verify that *Create incidents automatically from all alerts generated in this connected service* is **Enabled**. --->

### 작업 3: Azure 활동 데이터 커넥터 커넥트

이 작업에서는 Azure 활동* 데이터 커넥터를 *연결합니다.

1. Microsoft Sentinel 왼쪽 메뉴에서 콘텐츠 관리 섹션까지 *아래로 스크롤하고 콘텐츠 허브**를 선택합니다**.*

1. 콘텐츠 허브*에서 *Azure 활동** 솔루션을 검색**하고 목록에서 선택합니다.

1. *Azure 활동* 솔루션 페이지에서 설치**를 선택합니다**.

1. 설치가 완료되면 관리를 선택합니다 **.**

    >**참고:** Azure 활동* 솔루션은 *Azure 활동* 데이터 커넥터, 12개의 *분석 규칙, 14개의 헌팅 쿼리 및 1개의 통합 문서를 설치합니다.

1. Azure 활동* 데이터 커넥터를 *선택하고 커넥터 열기 페이지를** 선택합니다**.

1. *[지침] 탭 아래의 ** 구성* 영역에서 아래로 스크롤하여 "2입니다. 구독 커넥트..."를 선택하고 **Azure Policy 할당 마법사를 시작합니다>**.

1. **기본 사항** 탭의 **범위** 아래에서 줄임표 단추(...)를 선택하고, 드롭다운 목록에서 “Azure Pass - 스폰서쉽” 구독을 선택하고, **선택**을 클릭합니다.

1. **매개 변수** 탭을 선택하고 **기본 Log Analytics 작업 영역** 드롭다운 목록에서 *uniquenameDefender* 작업 영역을 선택합니다. 이 작업은 Log Analytics 작업 영역에 정보를 보내는 구독 구성을 적용합니다.

1. **수정** 탭에서 **수정 작업 만들기** 확인란을 선택합니다. 이 작업은 기존 Azure 리소스에 정책을 적용합니다.

1. **검토 + 만들기** 단추를 선택하여 구성을 검토합니다.

1. **만들기**를 선택하여 완료합니다.

## 연습 2 진행
