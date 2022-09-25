# <a name="module-2-demo---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>모듈 2 데모 - 엔드포인트용 Microsoft Defender를 사용하여 위협 완화



**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## <a name="simulated-attacks"></a>시뮬레이션된 공격

이 작업에서는 엔드포인트용 Microsoft Defender 기능을 살펴보기 위해 시뮬레이션된 공격 1개를 실행합니다.

1. 브라우저에 Microsoft Defender 보안 센터가 아직 열려 있지 않으면 Microsoft Defender 보안 센터(https://security.microsoft.com) )로 이동하여 테넌트 관리자로 로그인합니다.

1. 메뉴의 **엔드포인트**에서 **평가 및 자습서**를 선택한 다음, 왼쪽에서 **자습서 및 시뮬레이션**을 선택합니다.

1. **자습서** 탭을 선택합니다.

1. Under <bpt id="p1">*</bpt>Automated investigation (backdoor)<ept id="p1">*</ept> you will see a message describing the scenario. Below this paragraph, click <bpt id="p1">**</bpt>Read the walkthrough<ept id="p1">**</ept>. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named <bpt id="p1">**</bpt>Run the simulation<ept id="p1">**</ept> (page 5, starting at step 2) and follow the steps to run the attack. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> The simulation file <bpt id="p2">*</bpt>RS4_WinATP-Intro-Invoice.docm<ept id="p2">*</ept> can be found back in portal, just below the <bpt id="p3">**</bpt>Read the walkthrough<ept id="p3">**</ept> you selected in the previous step by selecting the <bpt id="p4">**</bpt>Get simulation file<ept id="p4">**</ept> button.

    1. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> After executing the file with the  exploit, you can return to the <bpt id="p2">[</bpt>Microsoft 365 Defender Security Center<ept id="p2">](https://security.microsoft.com)</ept> and click on the <bpt id="p3">**</bpt>Incidents<ept id="p3">**</ept> tab to see the alerts. The guide incorrectly references the <bpt id="p1">*</bpt>Microsoft Defender ATP portal<ept id="p1">*</ept> which has been migrated and rebranded.
    1. Open the incident page and click <bpt id="p1">**</bpt>Manage Incident<ept id="p1">**</ept>. Click <bpt id="p1">**</bpt>Resolve incident<ept id="p1">**</ept> to resolve all of the active alerts.


## <a name="you-have-completed-the-demo"></a>이 데모를 완료했습니다.