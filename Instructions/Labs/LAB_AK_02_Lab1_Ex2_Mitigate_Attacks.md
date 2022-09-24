---
lab:
  title: 연습 2 - 엔드포인트용 Microsoft Defender를 사용하여 공격 완화
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# <a name="module-2---lab-1---exercise-2---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>모듈 2 - 랩 1 - 연습 2 - 엔드포인트용 Microsoft Defender를 사용하여 위협 완화

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft Defender for Endpoint. Your manager plans to onboard a few devices to provide insight into required changes to the Security Operations (SecOps) team response procedures.

엔드포인트용 Defender 공격 완화 기능을 살펴보기 위해 시뮬레이션된 공격 2개를 실행합니다.


### <a name="task-1-simulated-attacks"></a>작업 1: 시뮬레이션된 공격

이 작업에서는 엔드포인트용 Microsoft Defender 기능을 살펴보기 위해 시뮬레이션된 공격 2개를 실행합니다.

1. 현재 위치가 Microsoft Edge 브라우저의 Microsoft 365 Defender 포털이 아닌 경우 https://security.microsoft.com) 으로 이동하고 테넌트에 대한 관리자로 로그인합니다.

1. 메뉴의 **엔드포인트**에서 **평가 및 자습서**를 선택한 다음, 왼쪽에서 **자습서 및 시뮬레이션**을 선택합니다.

1. **자습서** 탭을 선택합니다.

1. Under <bpt id="p1">*</bpt>Automated investigation (backdoor)<ept id="p1">*</ept> you will see a message describing the scenario. Below this paragraph, click <bpt id="p1">**</bpt>Read the walkthrough<ept id="p1">**</ept>. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named <bpt id="p1">**</bpt>Run the simulation<ept id="p1">**</ept> (page 5, starting at step 2) and follow the steps to run the attack. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> The simulation file <bpt id="p2">*</bpt>RS4_WinATP-Intro-Invoice.docm<ept id="p2">*</ept> can be found back in portal, just below the <bpt id="p3">**</bpt>Read the walkthrough<ept id="p3">**</ept> you selected in the previous step by selecting the <bpt id="p4">**</bpt>Get simulation file<ept id="p4">**</ept> button. 

1. 이제 마지막 3개 단계를 반복하여 자동 조사(파일리스 공격)를 실행합니다.

1. Microsoft 365 Defender 포털의 왼쪽 메뉴 모음에서 **인시던트 및 경고**를 선택한 다음, **인시던트**를 선택합니다.

1. A new incident called "Multi-stage incident..." will appear in the right pane. Allow at least 5 minutes for the incident to appear. Click the incident name to load its details.

1. **인시던트 관리** 단추를 선택하면 새 창 블레이드가 나타납니다. 

1. **인시던트 태그** 아래에 “자습서”를 입력하고 **자습서(새로 만들기)** 를 선택하여 새 태그를 만듭니다. 

1. **내게 할당** 토글을 선택하여 사용자 계정을 인시던트 소유자로 추가합니다. 

1. **분류** 아래에서 드롭다운 메뉴를 확장합니다. 

1. **정보, 예상 작업**에서 **보안 테스트**를 선택합니다. 

1. 원하는 경우 설명을 추가하고 **저장**을 클릭하여 완료합니다.

1. Review the contents of the Alerts, Devices, Users, Investigations, Evidence and Response, Graph tabs. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> Some tabs might be hidden due the size of your display. Select the ellipsis tab (...) to make them appear.

>여러분은 엔드포인트용 Microsoft Defender를 구현하고 있는 회사에서 일하는 보안 운영 분석가입니다.

## <a name="you-have-completed-the-lab"></a>이 랩을 완료했습니다.
