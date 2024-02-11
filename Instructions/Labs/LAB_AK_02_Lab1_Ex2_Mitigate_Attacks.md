---
lab:
  title: 연습 2 - 엔드포인트용 Microsoft Defender를 사용하여 공격 완화
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# 학습 경로 2 - 랩 1 - 연습 2 - 엔드포인트용 Microsoft Defender를 사용하여 위협 완화

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

여러분은 엔드포인트용 Microsoft Defender를 구현하고 있는 회사에서 일하는 보안 운영 분석가입니다. 관리자는 몇 가지 디바이스를 온보딩하여 SecOps(Security Operations) 팀 응답 프로시저에 필요한 변경 내용에 대한 인사이트를 제공할 계획입니다.

엔드포인트용 Defender 공격 완화 기능을 탐색하려면 디바이스 온보딩에 성공했는지 확인하고 해당 프로세스 중에 생성된 경고 및 인시던트에 대해 조사합니다.

>**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다.

### 작업 1: 디바이스 온보딩 확인

이 작업에서는 디바이스가 성공적으로 온보딩되었는지 확인하고 테스트 경고를 만듭니다.

1. Microsoft Edge 브라우저의 Microsoft Defender XDR 포털에 아직 없는 경우 테넌트에 대한 관리(로 로그인)https://security.microsoft.com)합니다.

1. 왼쪽 메뉴**의 자산 영역에서 디바이스**를** 선택합니다**. 계속하기 전에 WIN1이 디바이스 페이지에 나타날 때까지 기다려 주세요. 그렇지 않으면, 나중에 생성될 경고를 보기 위해 이 작업을 반복해야 할 수 있습니다.

    >**참고:** 온보딩 프로세스를 완료하고 1시간 후에 디바이스 목록에 디바이스가 표시되지 않으면 온보딩 또는 연결 문제가 표시될 수 있습니다.

1. 왼쪽 메뉴 모음에서 설정** 선택한 **다음 설정 페이지에서 엔드포인트를** 선택합니다**.

1. 디바이스 관리 섹션에서 온보딩을** 선택하고 **"Windows 10 및 11"*이 운영 체제로 선택되어 있는지 확인*합니다. *이제 "온보딩된 첫 번째 디바이스"* 메시지가 완료됨*으로 표시됩니다*.

1. "2" 섹션 *아래로 스크롤합니다. 검색 테스트 실행"*, 복사 단추를 선택하여 검색 테스트 스크립트를 **복사** 합니다.  

1. WIN1 가상 머신의 Windows 검색 창에서 **CMD**를 입력하고 명령 프롬프트 앱의 오른쪽 창에서 **관리자 권한으로 실행**을 선택합니다.

1. “사용자 계정 컨트롤” 창이 표시되면 **예**를 선택하여 앱을 실행할 수 있도록 합니다. 

1. 관리istrator: 명령 프롬프트** 창을 마우스 오른쪽 단추로 클릭하여 **스크립트를 붙여넣고 Enter** 키를 눌러 **실행합니다.

    >**참고:** 스크립트를 성공적으로 실행한 후 몇 분 후에 Microsoft Defender XDR 포털에서 경고가 생성되면 창이 자동으로 닫힙니다.

<!--- ### Task 2: Simulated Attacks

>**Note:** The Evaluation lab and the Tutorials & simulations section of the portal is no longer available. Please refer to the **[interactive lab simulation](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** for a demonstration of the simulated attacks.

1. From the left menu, under **Endpoints**, select **Evaluation & tutorials** and then select **Tutorials & simulations** from the left side.

1. Select the **Tutorials** tab.

1. Under *Automated investigation (backdoor)* you will see a message describing the scenario. Below this paragraph, click **Read the walkthrough**. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named **Run the simulation** (page 5, starting at step 2) and follow the steps to run the attack. **Hint:** The simulation file *RS4_WinATP-Intro-Invoice.docm* can be found back in portal, just below the **Read the walkthrough** you selected in the previous step by selecting the **Get simulation file** button.

    <!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### 작업 2: 경고 및 인시던트 조사

이 태스크에서는 이전 태스크의 온보딩 검색 테스트 스크립트에서 생성된 경고 및 인시던트에 대해 조사합니다.

1. Microsoft Defender XDR 포털**의 왼쪽 메뉴 모음에서 인시던트 및 경고를** 선택한 다음 경고를 선택합니다****.

1. **경고** 창에서 의심스러운 PowerShell 명령줄*이라는 *경고를 선택하여 세부 정보를 로드합니다.

1. *경고 스토리* 타임라인 검토한 다음 세부 정보* 및 *권장 사항* 탭을 검토*합니다.

    >**참고:** 경고 세부 정보* 탭에서 인시던트 세부 정보* 섹션까지 *아래로 스크롤하고 하나의 엔드포인트* 링크에서 실행 인시던트(Execution Incident)를 선택하여 *인시던트 열기를 *선택할 수 있습니다.

1. Microsoft Defender XDR 포털**의 왼쪽 메뉴 모음에서 인시던트** 및 경고를 선택한 다음, 인시던트 선택 ****

1. 한 엔드포인트*에서 실행 인시던트라는 *새 인시던트가 오른쪽 창에 있습니다. 인시던트 이름을 선택하여 세부 정보를 로드합니다.

1. 인시던**트 **관리 링크(연필 아이콘 포함)를 선택하면 새 창 블레이드가 나타납니다.

1. 인시던트 태그 아래에 **"시뮬레이션"을** 입력하고 시뮬레이션(새로 만들기)**을 선택하여 **새 태그를 만듭니다.

1. **내게 할당** 토글을 선택하여 사용자 계정(Me)을 인시던트 소유자로 추가합니다.

1. **분류** 아래에서 드롭다운 메뉴를 확장합니다.

1. **정보, 예상 작업**에서 **보안 테스트**를 선택합니다.

1. 원하는 경우 메모를 추가하고 저장**을 선택하여 인시던트 업데이트 및 완료를 선택합니다**.

1. 공격 스토리, 경고, 자산, 조사, 증거 및 대응* 및 *요약* 탭의 내용을 *검토합니다. 디바이스 및 사용자가 자산 탭 아래에 *있습니다*. 실제 인시던트에서 *공격 스토리* 탭에는 인시던트 그래프*가 *표시됩니다. **힌트:** 표시 크기 때문에 일부 탭이 숨겨질 수 있습니다. 줄임표 탭(...)을 선택하여 해당 탭을 표시합니다.

<!---    >**Warning:** The simulated attacks here are an excellent source of learning through practice. Only perform the attacks in the instructions provided for this lab when using the course provided Azure tenant.  You may perform other simulated attacks *after* this training course is complete with this tenant. --->

## 이 랩을 완료했습니다.
