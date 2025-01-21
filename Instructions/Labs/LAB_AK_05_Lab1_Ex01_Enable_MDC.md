---
lab:
  title: 연습 1 - 클라우드용 Microsoft Defender 사용
  module: Learning Path 5 - Mitigate threats using Microsoft Defender for Cloud
---

# 학습 경로 5 - 랩 1 - 연습 1 - 클라우드용 Microsoft Defender 사용

## 랩 시나리오

여러분은 클라우드용 Microsoft Defender를 사용하여 클라우드 워크로드 보호를 구현하고 있는 회사에서 일하는 보안 운영 분석가입니다. 이 랩에서는 클라우드용 Microsoft Defender를 사용하도록 설정합니다.

>**중요:** 학습 경로 #5에 대한 랩 연습은 *독립 실행형* 환경에 있습니다. 완료하기 전에 랩을 종료하면 구성을 다시 실행해야 합니다.

### 이 랩의 예상 완료 시간은 15분입니다.

### 작업 1: 클라우드용 Microsoft Defender 사용

이 작업에서는 클라우드용 Microsoft Defender를 사용하도록 설정하고 구성합니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.

1. Microsoft Edge 브라우저에서 <https://portal.azure.com>의 Azure Portal로 이동합니다.
  
1. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Microsoft Azure Portal의 검색 창에 *Defender*를 입력하고 **클라우드용 Microsoft Defender**를 선택합니다.

1. 클라우드용 Microsoft Defender의 왼쪽 탐색 메뉴에서 *관리* 섹션을 확장하고 **환경 설정**을 선택합니다.

1. **모두 펼치기** 버튼을 선택하면 모든 구독 및 리소스를 볼 수 있습니다.

1. **MOC Subscription-lodxxxxxxxx** 구독(또는 사용 중인 언어로 동일한 이름)을 선택합니다.

1. 이제 클라우드용 Microsoft Defender 플랜으로 보호되는 Azure 리소스를 검토합니다.

    >**중요:** 모든 Defender 플랜이 *끄기*인 경우 **모든 계획 사용**을 선택합니다. *월 200달러 Microsoft Defender for API 계획 1*을 선택한 다음 **저장**을 선택합니다. 페이지 상단에서 **저장**을 선택하고 *"사용자의 Defender 플랜 구독이 성공적으로 저장되었습니다."* 메시지가 나타날 때까지 기다립니다. 알림이 표시됩니다.

1. 설정 영역(저장 옆)에서 **설정 및 모니터링** 탭을 선택합니다.

1. 모니터링 확장을 검토합니다. 여기에는 Virtual Machines, 컨테이너 및 스토리지 계정에 대한 구성이 포함됩니다.

1. **계속** 버튼을 선택하거나 페이지 오른쪽 상단의 'X'를 선택하여 "설정 및 모니터링" 페이지를 닫습니다.

1. 페이지 오른쪽 상단의 'X'를 선택하여 설정 페이지를 닫으면 **환경 설정**으로 돌아갑니다.

<!---1. Select the Log analytics workspace you created earlier *uniquenameDefender* to review the available options and pricing.

1. Select **Enable all plans** (to the right of Select Defender plan) and then select **Save**. Wait for the *"Microsoft Defender plan for workspace uniquenameDefender were saved successfully!"* notification to appear.

    >**Note:** If the page is not being displayed, refresh your Edge browser and try again.

1. Close the Defender plans page by selecting the 'X' on the upper right of the page to go back to the **Environment settings**. --->

### 작업 2: 클라우드용 Microsoft Defender 대시보드 이해

1. Microsoft Azure Portal의 검색 창에 *Defender*를 입력하고 **클라우드용 Microsoft Defender**를 선택합니다.

1. 클라우드용 Microsoft Defender 왼쪽 탐색 메뉴의 *일반* 섹션에서 **개요**를 선택합니다.

1. 개요 블레이드는 보안 태세에 대한 통합 보기를 제공하며 보안 태세, 규정 준수, 워크로드 보호, 방화벽 관리자, 인벤토리 및 정보 보호(미리 보기)와 같은 여러 독립적인 클라우드 보안 핵심 요소를 포함합니다. 이러한 각 핵심 요소에는 해당 범주에 대한 심층적인 인사이트와 조치를 취할 수 있는 전용 대시보드도 있어 보안 전문가가 쉽게 액세스하고 가시성을 높일 수 있습니다.

    >**참고:** 위쪽 메뉴 모음을 사용하면 구독 단추를 선택하여 구독을 보고 필터링할 수 있습니다. 이 랩에서는 하나만 사용하지만 다른/추가 구독을 선택하면 선택한 구독의 보안 태세를 반영하도록 인터페이스가 조정됩니다.

1. **새로운 기능** 아이콘 링크를 클릭하면 새 기능, 버그 수정 등을 최신 상태로 유지할 수 있는 최신 릴리스 정보가 포함된 새 탭이 열립니다.

    >**참고:** 상단 메뉴의 상위 숫자입니다. 이 보기를 사용하면 연결된 클라우드 계정과 함께 구독, 활성 권장 사항 및 보안 경고의 요약을 볼 수 있습니다.

1. 상단 메뉴 모음에서 **Azure 구독**을 선택합니다. 이렇게 하면 사용 가능한 구독에서 선택할 수 있는 환경 설정으로 전환됩니다.

1. **개요** 페이지로 돌아가서 **보안 태세** 타일을 검토합니다. 현재 *보안 점수*와 완료된 제어 및 권장 사항의 수를 확인할 수 있습니다. 이 타일을 선택하면 구독 전체의 드릴다운 보기로 리디렉션됩니다.

1. **규정 준수** 타일에서는 Azure 및 하이브리드 클라우드 환경에 대한 지속적인 평가를 기반으로 규정 준수 상태에 대한 인사이트를 얻을 수 있습니다. 이 타일은 Microsoft Cloud Security 벤치마크 및 최저 규정 준수 규정 표준인 다음 표준을 보여 줍니다. 데이터를 보려면 먼저 보안 정책을 추가해야 합니다.

1. 이 타일을 선택하면 **규정 준수** 대시보드로 리디렉션되며, 여기서 추가 표준을 추가하고 현재 표준을 탐색할 수 있습니다.

1. 다음 연습에서는 *클라우드용 Microsoft Defender***보안 태세** 및 **규정 준수**에 대해 계속 살펴보겠습니다.

## 연습 2 계속 진행
