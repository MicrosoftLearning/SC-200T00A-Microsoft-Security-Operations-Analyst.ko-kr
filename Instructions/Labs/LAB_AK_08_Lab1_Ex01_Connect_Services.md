---
lab:
  title: 연습 1 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 데이터 연결
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# 학습 경로 8 - 랩 1 - 연습 1 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 데이터 연결

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 조직에 있는 많은 데이터 원본의 로그 데이터를 연결하는 방법을 알아야 합니다. 조직에는 Microsoft 365, Microsoft 365 Defender, Azure 리소스, 비 Azure 가상 머신 등의 데이터가 있습니다. 먼저 Microsoft 원본 연결을 시작합니다.

>**중요:** 학습 경로 #8에 대한 랩 연습은 *독립 실행형* 환경에 있습니다. 완료하기 전에 랩을 종료하면 구성을 다시 실행해야 합니다.

### 이 랩의 예상 완료 시간은 20분입니다.

### 작업 1: Microsoft Sentinel 작업 영역에 액세스

이 작업에서는 Microsoft Sentinel 작업 영역에 액세스합니다.

>**참고:** Microsoft Sentinel이 Azure 구독에 **defenderWorkspace**라는 이름으로 사전 배포되었으며 필요한 *콘텐츠 허브* 솔루션이 설치되어 있습니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저를 엽니다.

1. Edge 브라우저에서 Azure Portal(<https://portal.azure.com> )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel **defenderWorkspace**을 선택합니다.

1. 다음 작업을 진행합니다.

### 작업 2: 클라우드용 Microsoft Defender 데이터 커넥터 연결

이 작업에서는 클라우드용 Microsoft Defender 데이터 커넥터를 연결합니다.

   <!--- >>**Important:** To *Enable* Bi-directional sync, please rerun  **[Lab 05 Exercise 1](https://microsoftlearning.github.io/SC-200T00A-Microsoft-Security-Operations-Analyst/Instructions/Labs/LAB_AK_05_Lab1_Ex01_Enable_MDC.html)**, Task 2, and select **Setup** from the *Microsoft Defender for Cloud* navigation menu to verify all eligible Azure subscriptions are onboarded. --->

1. Microsoft Sentinel 탐색 메뉴에서 **콘텐츠 관리** 섹션까지 아래로 스크롤하여 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **클라우드용 Microsoft Defender** 솔루션을 검색하고 목록에서 선택합니다.

1. *클라우드용 Microsoft Defender* 솔루션 세부 정보 페이지에서 **관리**를 선택합니다.

    >**참고:** *클라우드용 Microsoft Defender* 솔루션은 *구독 기반 클라우드용 Microsoft Defender(레거시)* 데이터 커넥터, *테넌트 기반 클라우드용 Microsoft Defender(미리 보기)* 및 분석 규칙을 설치합니다. *테넌트 기반 클라우드용 Microsoft Defender(미리 보기)* 데이터 커넥터는 테넌트에 여러 구독이 있는 경우 사용됩니다.

1. *구독 기반 클라우드용 Microsoft Defender(레거시)* 데이터 커넥터 확인란을 선택하고 **커넥터 페이지 열기**를 선택합니다.

1. *구성* 섹션에서 *MOC 구독-XXXXXXXXXXX* 확인란을 **선택**하고 **연결** 링크를 선택하거나, **상태** 옵션을 오른쪽으로 밉니다.

1. 양방향 동기화를 사용하도록 설정하려면 **모든 구독에 대해 Microsoft Defender 사용** 링크를 선택합니다.

    >**참고:** 링크를 보려면 오른쪽으로 스크롤해야 할 수 있습니다.

1. *클라우드용 Microsoft Defender - 시작* 페이지에서 *MOC 구독-XXXXXXXXXXX* 확인란을 선택해야 하며 *Microsoft Defender 플랜*은 *사용 - 부분(평가판 30일 남음)* 으로 표시되어야 합니다.

1. 오른쪽 위에서 **X(닫기)** 단추를 선택하여 *시작* 페이지를 닫습니다. *클라우드용 Microsoft Defender* 구성 페이지로 돌아와야 합니다.

1. 이제 *MOC 구독-XXXXXXXXXXX*의 *상태*가 **연결됨**으로 설정되고 *양방향 동기화*가 *사용*으로 설정됩니다.

    >**참고:** 브라우저를 새로 고쳐야 할 수도 있습니다.

### 작업 3: Azure 활동 데이터 커넥터 연결

이 작업에서는 *Azure Activity* 데이터 커넥터를 연결합니다.

1. Microsoft Sentinel 탐색 메뉴에서 *콘텐츠 관리* 섹션까지 아래로 스크롤하여 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **Azure Activity** 솔루션을 검색하고 목록에서 선택합니다.

1. *Azure 활동* 솔루션 세부 정보 페이지에서 **관리**를 선택합니다.

    >**참고:** *Azure 활동* 솔루션은 *Azure 활동* 데이터 커넥터, 13개의 분석 규칙, 14개의 헌팅 쿼리 및 1개의 통합 문서를 설치합니다.

1. *Azure Activity* 데이터 커넥터를 선택하고 **커넥터 페이지 열기**를 선택합니다.

1. *지침* 탭 아래의 *구성* 영역에서 "2. 구독 연결..."까지 아래로 스크롤하고 **Azure Policy 할당 마법사 시작>** 을 선택합니다.

1. **기본 사항** 탭의 **범위** 아래에서 줄임표 단추(...)를 선택하고, 드롭다운 목록에서 *MOC 구독-XXXXXXXXXXX* 구독을 선택하고, **선택**을 클릭합니다.

    >**참고:** 선택적 리소스 그룹을 선택하지 *마세요*.

1. **매개 변수** 탭을 선택하고 **기본 Log Analytics 작업 영역** 드롭다운 목록에서 *uniquenameDefender* 작업 영역을 선택합니다. 이 작업은 구독 구성을 적용하여 Log Analytics 작업 영역에 정보를 보냅니다.

1. **수정** 탭에서 **수정 작업 만들기** 확인란을 선택합니다. 이 작업은 기존 Azure 리소스에 정책을 적용합니다.

1. **검토 + 만들기** 단추를 선택하여 구성을 검토합니다.

1. **만들기**를 선택하여 완료합니다.

## 연습 2 계속 진행
