---
lab:
  title: 연습 1 - 엔드포인트용 Microsoft Defender 배포
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# <a name="module-2---lab-1---exercise-1---deploy-microsoft-defender-for-endpoint"></a>모듈 2 - 랩 1 - 연습 1 - 엔드포인트용 Microsoft Defender 배포

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft Defender for Endpoint. Your manager plans to onboard a few devices to provide insight into required changes to the Security Operations (SecOps) team response procedures.

You start by initializing the Defender for Endpoint environment. Next, you onboard the initial devices for your deployment by running the onboarding script on the devices. You configure security for the environment. Lastly, you create Device groups and assign the appropriate devices.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept>  The lab Virtual Machines are used through different modules. SAVE your virtual machines. If you exit the lab without saving, you will be required to re-run some configurations again.

>**참고:** 이전 모듈의 작업 3을 성공적으로 완료했는지 확인합니다.


### <a name="task-1-initialize-microsoft-defender-for-endpoint"></a>작업 1: 엔드포인트용 Microsoft Defender 초기화

이 작업에서는 엔드포인트용 Microsoft Defender 포털 초기화를 수행합니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 현재 위치가 Microsoft 365 Defender 포털이 아닌 경우 Microsoft Edge 브라우저를 시작합니다.

1. Edge 브라우저에서 Microsoft 365 Defender 포털(https://security.microsoft.com) )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. **Microsoft 365 Defender** 포털에 있는 탐색 메뉴의 왼쪽에서 **설정**을 선택합니다.

1. **설정** 페이지에서 **디바이스 검색**을 선택합니다. 

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you do not see the <bpt id="p2">**</bpt>Device discovery<ept id="p2">**</ept> option under <bpt id="p3">**</bpt>Settings<ept id="p3">**</ept>, logout by selecting the top-right circle with your account initials and select <bpt id="p4">**</bpt>Sign out<ept id="p4">**</ept>. Other options that you might want to try is to refresh the page with Ctrl+F5 or open the page InPrivate. Login again with the <bpt id="p1">**</bpt>Tenant Email<ept id="p1">**</ept> credentials.

1. In Discovery setup make sure <bpt id="p1">**</bpt>Standard discovery (recommended)<ept id="p1">**</ept> is selected. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you do not see the option, refresh the page.


### <a name="task-2-onboard-a-device"></a>작업 2: 디바이스 온보딩

이 작업에서는 온보딩 스크립트를 사용하여 엔드포인트용 Microsoft Defender에 디바이스를 온보딩합니다.

1. 현재 위치가 브라우저의 Microsoft 365 Defender 포털이 아닌 경우 Microsoft Edge 브라우저를 시작하고 https://security.microsoft.com) 으로 이동하고 **테넌트 메일** 자격 증명으로 로그인합니다.

1. 왼쪽 메뉴 모음에서 **설정**을 선택한 다음 설정 페이지에서 **엔드포인트**를 선택합니다.

1. 디바이스 관리 섹션에서 **온보딩**을 선택합니다.

1. 여러분은 엔드포인트용 Microsoft Defender를 구현하고 있는 회사에서 일하는 보안 운영 분석가입니다.

1. 다운로드한 zip 파일을 마우스 오른쪽 단추로 클릭하고, **모두 추출...** 을 선택하고, 완료되면 압축을 푼 파일 표시가 선택되어 있는지 확인하고, **추출**을 선택합니다.

1. 귀하의 관리자가 몇몇 디바이스를 온보딩하여 보안 운영(SecOps) 팀 응답 절차에 필요한 변경 내용에 대한 인사이트를 제공하려고 합니다.

1. Right-click on the extracted file "WindowsDefenderATPLocalOnboardingScript.cmd" again and choose <bpt id="p1">**</bpt>Run as Administrator<ept id="p1">**</ept>.  <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you encounter the Windows SmartScreen window, select on <bpt id="p2">**</bpt>More info<ept id="p2">**</ept>, and choose <bpt id="p3">**</bpt>Run anyway<ept id="p3">**</ept>. 
    
1. 먼저 엔드포인트용 Defender 환경을 초기화합니다.

1. 그런 다음 디바이스에서 온보딩 스크립트를 실행하여 배포할 초기 디바이스를 온보딩합니다.

1. 환경에 대한 보안을 구성합니다.  

1. WIN1 가상 머신의 Windows 검색 창에서 **CMD**를 입력하고 명령 프롬프트 앱의 오른쪽 창에서 **관리자 권한으로 실행**을 선택합니다. 

1. “사용자 계정 컨트롤” 창이 표시되면 **예**를 선택하여 앱을 실행할 수 있도록 합니다. 

1. 마지막으로 디바이스 그룹을 만들고 적절한 디바이스를 할당합니다.

1. In the Microsoft 365 Defender portal, in the left-hand menu, under the <bpt id="p1">**</bpt>Assets<ept id="p1">**</ept> area, select <bpt id="p2">**</bpt>Devices<ept id="p2">**</ept>. If the device is not shown, complete the next task and come back to check it back later. It can take up to 60 minutes for the first device to be displayed in the portal.

    >**참고:** 온보딩 프로세스를 완료하고 한 시간 후에 디바이스 목록에 디바이스가 표시되지 않으면 온보딩 또는 연결 문제가 표시될 수 있습니다.


### <a name="task-3-configure-roles"></a>작업 3: 역할 구성

이 작업에서는 디바이스 그룹에 사용할 역할을 구성합니다.

1. Microsoft 365 Defender 포털의 왼쪽 메뉴 모음에서 **설정**을 선택한 다음 **엔드포인트**를 선택합니다. 

1. 권한 영역에서 **역할**을 선택합니다.

1. **역할 켜기** 단추를 선택합니다.

1. **+ 항목 추가**를 선택합니다.

1. 역할 추가 대화 상자에서 다음을 입력합니다.

    |일반 설정|값|
    |---|---|
    |역할 이름|**계층 1 지원**|
    |사용 권한|라이브 응답 기능 - 고급|

1. **중요:**  랩 가상 머신은 다양한 모듈을 통해 사용됩니다.

1. **저장**을 선택합니다.


### <a name="task-4-configure-device-groups"></a>작업 4: 디바이스 그룹 구성

이 작업에서는 액세스 제어 및 자동화 구성이 가능하도록 디바이스 그룹을 구성합니다.

1. Microsoft 365 Defender 포털의 왼쪽 메뉴 모음에서 **설정**을 선택한 다음 **엔드포인트**를 선택합니다. 

1. 권한 영역에서 **디바이스 그룹**을 선택합니다.

1. **+ 디바이스 그룹 추가** 아이콘을 선택합니다.

1. 일반 탭에서 다음 정보를 입력합니다.

    |일반 설정|값|
    |---|---|
    |디바이스 그룹 이름|**주기적**|
    |자동화 수준|전체 - 자동으로 위협 수정|

1. **다음**을 선택합니다.

1. 디바이스 탭에서 OS 조건으로 **Windows 10**을 선택하고 **다음**을 선택합니다.

1. 가상 머신을 저장해 두세요.

1. 저장하지 않고 랩을 종료하면 일부 구성을 다시 실행해야 합니다.

1. **완료**를 선택합니다.

1. Device group configuration has changed. Select <bpt id="p1">**</bpt>Apply changes<ept id="p1">**</ept> to check matches and recalculate groupings.

1. 이제 방금 만든 “일반” 및 동일한 수정 수준을 가진 “그룹화되지 않은 디바이스(기본값)”의 두 가지 디바이스 그룹을 포함하려고 합니다.

## <a name="proceed-to-exercise-2"></a>연습 2 계속 진행
