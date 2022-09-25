---
lab:
  title: 연습 1 - 클라우드용 Microsoft Defender 사용
  module: Module 3 - Mitigate threats using Microsoft Defender for Cloud
---

# <a name="module-3---lab-1---exercise-1---enable-microsoft-defender-for-cloud"></a>모듈 3 - 랩 1 - 연습 1 - 클라우드용 Microsoft Defender 사용

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod3_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing cloud workload protection with Microsoft Defender for Cloud.  In this lab you will enable Microsoft Defender for Cloud.


### <a name="task-1-access-the-azure-portal-and-set-up-a-subscription"></a>작업 1: Azure Portal 액세스 및 구독 설정

이 연습에서는 이 랩과 이후 랩을 완료하는 데 필요한 Azure 구독을 설정합니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저를 열거나 이미 열려 있는 경우 새 탭을 엽니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com) )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *구독*을 입력하고 **구독**을 선택합니다. 

1. If the <bpt id="p1">*</bpt>"Azure Pass - Sponsorship"<ept id="p1">*</ept> subscription is shown (or equivalent name in your selected language), proceed to Task #2. Otherwise, ask your instructor on how to create the Azure subscription with your tenant admin user credentials. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The subscription creation process could take up to 10 minutes. 

    >**중요:** 이러한 랩은 강의 중에 USD $10 미만의 Azure 서비스를 사용하도록 설계되었습니다.


### <a name="task-2-create-a-log-analytics-workspace"></a>작업 2: Log Analytics 작업 영역 만들기

이 작업에서는 클라우드용 Microsoft Defender에서 사용할 Log Analytics 작업 영역을 만듭니다.

1. Azure Portal의 검색 창에 Log Analytics 작업 영역을 입력하고 동일한 서비스 이름을 선택합니다.

1. 명령 모음에서 **+만들기**를 선택합니다.

1. 리소스 그룹의 **새로 만들기**를 선택합니다.

1. *RG-Defender*를 입력하고 **확인**을 선택합니다.

1. *uniquenameAzureDefender*와 같은 고유한 이름을 입력합니다.

1. **검토 + 생성**를 선택합니다.

1. Once the workspace validation has passed, select <bpt id="p1">**</bpt>Create<ept id="p1">**</ept>. Wait for the new workspace to be provisioned, this may take a few minutes.


### <a name="task-3-enable-microsoft-defender-for-cloud"></a>작업 3: 클라우드용 Microsoft Defender 사용

이 작업에서는 클라우드용 Microsoft Defender를 사용하도록 설정하고 구성합니다.

1. Azure Portal의 검색 창에 *Defender*를 입력하고 **클라우드용 Microsoft Defender**를 선택합니다.

1. On the <bpt id="p1">**</bpt>Getting started<ept id="p1">**</ept> page, under the <bpt id="p2">**</bpt>Upgrade<ept id="p2">**</ept> tab, make sure your subscription is selected, and then select the <bpt id="p3">**</bpt>Upgrade<ept id="p3">**</ept> button at the bottom of the page. Wait for the <bpt id="p1">*</bpt>Trial started<ept id="p1">*</ept> notification to appear, it takes about 2 minutes. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You can click the bell button on the top bar to review your Azure portal notifications.

1. The next page shows the option to install the agent on virtual machines already in the subscription. Select <bpt id="p1">**</bpt>Continue without installing agents<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Do nothing here<ept id="p2">**</ept>.

1. 포털 메뉴의 관리 영역에서 **환경 설정**을 선택합니다.

1. **“Azure Pass - 스폰서쉽”** 구독(또는 사용 중인 언어로 동일한 이름)을 선택합니다. 

1. 모든 클라우드용 Microsoft Defender 플랜 사용에서 사용하도록 설정된 기능과 다음을 위한 Microsoft Defender 열에서 보호된 Azure 리소스를 검토합니다. 

1. 설정 영역에서 **자동 프로비전**을 선택합니다.

1. 여러분은 클라우드용 Microsoft Defender를 사용하여 클라우드 워크로드 보호를 구현하고 있는 회사에서 일하는 보안 운영 분석가입니다.

1. 페이지 오른쪽 위에 있는 ‘x’를 선택하여 설정 페이지를 닫고 **환경 설정**으로 다시 돌아가서 구독 왼쪽에서 ‘>’을 선택합니다.

1. 이 랩에서는 클라우드용 Microsoft Defender를 사용하도록 설정합니다.

    >**참고:** 페이지가 표시되지 않으면 Edge 브라우저를 새로 고치고 다시 시도합니다.


### <a name="task-4-install-azure-arc-on-an-on-premises-server"></a>작업 4: 온-프레미스 서버에 Azure Arc 설치

이 작업에서는 더 쉽게 온보딩할 수 있도록 온-프레미스 서버에 Azure Arc를 설치합니다.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. Log in to <bpt id="p1">**</bpt>WINServer<ept id="p1">**</ept> virtual machine as Administrator with the password: <bpt id="p2">**</bpt>Passw0rd!<ept id="p2">**</ept> if required.  

1. Microsoft Edge 브라우저를 열고 https://portal.azure.com 에 있는 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Arc*를 입력하고 **Azure Arc**를 선택합니다.

1. 탐색 창의 **인프라** 아래에서 **서버**를 선택합니다.

1. **+추가**를 선택합니다.

1. "단일 서버 추가" 섹션에서 **스크립트 생성**을 선택합니다.

1. **다음**을 선택하여 리소스 세부 정보 탭으로 이동합니다.

1. Select the Resource group you created earlier. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> <bpt id="p2">*</bpt>RG-Defender<ept id="p2">*</ept>

    >**참고:** 리소스 그룹을 아직 만들지 않은 경우 다른 탭을 열고, 리소스 그룹을 만들고, 다시 시작합니다.

1. Review the <bpt id="p1">*</bpt>Server details<ept id="p1">*</ept> and <bpt id="p2">*</bpt>Connectivity method<ept id="p2">*</ept> options. Keep the default values and select <bpt id="p1">**</bpt>Next<ept id="p1">**</ept> to get to the Tags tab.

1. **다음**을 선택하여 스크립트 다운로드 및 실행 탭으로 이동합니다.

1. 1\. 구독 등록 단계에서 **등록**을 선택합니다.

    >**참고:** 처리를 위해 3분 이상 기다립니다.

1. Scroll down and select the <bpt id="p1">**</bpt>Download<ept id="p1">**</ept> button. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> if your browser blocks the download, take action in the browser to allow it. In Edge Browser, select the ellipsis button (...) if needed and then select <bpt id="p1">**</bpt>Keep<ept id="p1">**</ept>. 

1. Windows 시작 단추를 마우스 오른쪽 단추로 클릭하고 **Windows PowerShell(관리자)** 을 선택합니다.

1. Enter <bpt id="p1">*</bpt>Administrator<ept id="p1">*</ept> for "Username" and <bpt id="p2">*</bpt>Passw0rd!<ept id="p2">*</ept> for "Password" if you get a UAC prompt.

1. 입력: cd C:\Users\Administrator\Downloads

1. *Set-ExecutionPolicy -ExecutionPolicy Unrestricted*를 입력하고 Enter 키를 누릅니다.

1. 모두 예에 해당하는 **A** 키를 누른 다음 Enter 키를 누릅니다.

1. *.\OnboardingScript.ps1*을 입력하고 Enter 키를 누릅니다.  

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> If you get the error <bpt id="p2">*</bpt>"The term .\OnboardingScript.ps1 is not recognized..."<ept id="p2">*</ept>, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for <bpt id="p1">*</bpt>".\OnboardingScript (1).ps1"<ept id="p1">*</ept> or other file numbers in the running directory.

1. **R** 키를 눌러 한 번 실행하고 Enter 키를 누릅니다(몇 분 정도 걸릴 수 있음).

1. Edge 브라우저로 돌아가서 새 탭을 열고 주소 표시줄에 https://microsoft.com/devicelogin 을 입력합니다.

1. Windows PowerShell 창으로 돌아가서 에이전트를 인증하기 위해 스크립트의 마지막 줄에서 “...코드 입력” 뒤에 표시되는 코드를 복사합니다.

1. Go back to the Edge browser and paste it in the <bpt id="p1">**</bpt>Code<ept id="p1">**</ept> box and select <bpt id="p2">**</bpt>Next<ept id="p2">**</ept>. Select your tenant admin account and select <bpt id="p1">**</bpt>Continue<ept id="p1">**</ept> in the <bpt id="p2">*</bpt>Are you trying to sign in to Azure Connected Machine Agent?<ept id="p2">*</ept> window. 

1. Go back to the Windows PowerShell window and wait for the message <bpt id="p1">*</bpt>"Successfully Onboarded Resource to Azure"<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you see a message line with a new authentication code, you need to repeat the last 3 steps again.

1. “Azure Pass - 스폰서쉽” 구독이 표시되는 경우(또는 선택한 언어로 동일한 이름) 작업 #2로 진행합니다.

1. WINServer 서버 이름이 표시될 때까지 **새로 고침**을 선택합니다.

    >**참고:** 몇 분 정도 걸릴 수 있습니다.


### <a name="task-5-protect-an-on-premises-server"></a>작업 5: 온-프레미스 서버 보호

이 작업에서는 **WINServer** 가상 머신에 필요한 에이전트를 수동으로 설치합니다.

1. **클라우드용 Microsoft Defender**로 이동하고 **시작** 페이지를 선택합니다.

1. **시작** 탭을 선택합니다.

1. 아래로 스크롤하고 비 Azure 서버 추가 섹션에서 **구성**을 선택합니다.

1. 표시되지 않으면 강사에게 테넌트 관리 사용자 자격 증명을 사용하여 Azure 구독을 만드는 방법을 질문하세요.

1. 앞에서 만든 작업 영역 옆의 **+ 서버 추가**를 선택합니다.

1. **Windows 에이전트 다운로드(64비트)** 를 선택합니다.

1. **파일 열기**를 선택하여 다운로드한 *MMASetup-AMD64.exe* 파일을 실행합니다.

1. **에이전트 설치 옵션** 마법사 페이지가 나타날 때까지 **다음**을 선택하고, **Azure Log Analytics(OMS)에 에이전트 연결**을 선택한 후, **다음**을 선택합니다.

1. Azure Portal의 **작업 영역 키** 텍스트 상자에 있는 **작업 영역 ID** 및 **기본 키** 값을 복사하여 해당하는 마법사 페이지 필드에 붙여넣고 **다음**을 선택합니다.

1. **참고:** 구독 만들기 프로세스에는 최대 10분이 걸릴 수 있습니다.

1. “클라우드용 Microsoft Defender” 포털로 이동하고 **인벤토리**를 선택합니다.

1. The <bpt id="p1">**</bpt>WINServer<ept id="p1">**</ept> virtual machine will appear after at least 5 minutes. You may have to select <bpt id="p1">**</bpt>Refresh<ept id="p1">**</ept> to see it. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you see the number 1 under <bpt id="p2">*</bpt>Total resources<ept id="p2">*</ept> remove the filter to show the <bpt id="p3">*</bpt>WINServer<ept id="p3">*</ept> virtual machine.

1. 다음 랩으로 이동하고 나중에 돌아와서 **클라우드용 Microsoft Defender**의 **인벤토리** 섹션을 검토할 수 있습니다.

## <a name="proceed-to-exercise-2"></a>연습 2 계속 진행
