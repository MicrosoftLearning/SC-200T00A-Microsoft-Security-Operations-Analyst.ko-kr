---
lab:
  title: 연습 3 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트 연결
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-3---connect-linux-hosts-to-microsoft-sentinel-using-data-connectors"></a>모듈 6 - 랩 1 - 연습 3 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트 연결

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex3.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data are Linux virtual machines using the Common Event Formatting (CEF) and Syslog connectors.


><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> There are steps within the next Tasks that are done in different virtual machines. Look for the Virtual Machine name references.

### <a name="task-1-access-the-microsoft-sentinel-workspace"></a>작업 1: Microsoft Sentinel 작업 영역에 액세스

이 작업에서는 Microsoft Sentinel 작업 영역에 액세스합니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 새 Microsoft Edge 브라우저를 시작합니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 이전 랩에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.


### <a name="task-2-connect-a-linux-host-using-the-common-event-format-connector"></a>작업 2: Common Event Format 커넥터를 사용하여 Linux 호스트 연결

이 작업에서는 CEF(Common Event Format) 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트를 연결합니다.

1. Select <bpt id="p1">**</bpt>Data connectors<ept id="p1">**</ept> from the Configuration area in Microsoft Sentinel. From the Data Connectors tab, search for the <bpt id="p1">**</bpt>Common Event Format (CEF)<ept id="p1">**</ept> connector and select it from the list.

1. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

1. 구성에서 1.2 Linux 머신에 CEF 수집기 설치에 나와 있는 명령을 클립보드에 복사합니다. 

1. Launch your <bpt id="p1">**</bpt>LIN1<ept id="p1">**</ept> virtual machine. Login with the username and password provided by your lab hoster. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might need to press the Enter key to see the login prompt. 

1. Note the IP address for your LIN1 server. See the screenshot below as an example:

    ![linux 로그인](../Media/LinuxLoginExample.png)

1. 당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다.

1. 구체적인 Linux 서버 정보에 맞게 다음 PowerShell 명령을 수정하여 입력하고 Enter 키를 누릅니다.

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. 조직에 있는 많은 데이터 원본의 로그 데이터를 연결하는 방법을 알아야 합니다.

    ![linux 로그인](../Media/PSconnectLinux.png)

1. 다음 데이터 원본은 CEF(Common Event Formatting) 및 Syslog 커넥터를 사용하는 Linux 가상 머신입니다. 

1. 붙여넣은 후 Enter 키를 누르기 전에 아래와 같이 단어 *python*에 문자 **3**을 추가합니다.

    ![ConnectorScript](../Media/ConnectorScript.png)


1. Once the script is adjusted press Enter. The script will run against your Linux server remotely. When the script processes properly it should look like this screen:

    ![ConnectorScript](../Media/LinuxConnected.png)

1. **종료**를 입력하여 LIN1에 대한 원격 셸 연결을 닫습니다.


### <a name="task-3-connect-a-linux-host-using-the-syslog-connector"></a>작업 3: Syslog 커넥터를 사용하여 Linux 호스트 연결

이 작업에서는 Syslog 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트를 연결합니다.

1. Microsoft Sentinel 포털이 열려 있는 Edge 브라우저로 돌아가서 오른쪽 위 모서리에서 ‘x’를 선택하여 “CEF(Common Event Format)” 데이터 커넥터 페이지를 닫습니다. 

1. 데이터 커넥터 탭에서 **Syslog** 커넥터를 검색하고 목록에서 선택합니다.

1. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

1. 구성에서 **Azure 이외의 Linux 머신에 에이전트 설치**섹션을 엽니다.

1. **Azure 외 Linux 컴퓨터용 에이전트 다운로드 및 설치** 링크를 선택합니다. 

    >**중요:** 다음 작업에는 서로 다른 가상 머신에서 수행되는 단계가 있습니다.

1. **Linux 서버** 탭을 선택합니다.

    >가상 머신 이름 참조를 찾습니다.

1. *Linux용 에이전트 다운로드 및 설치* 영역의 명령을 클립보드에 복사합니다.

1. Launch your LIN2 virtual machine. Login with the username as password provided by your lab hoster. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might need to press the Enter key to see the login prompt.

1. Note the IP address for your LIN2 server. See the screenshot below as an example:

    ![linux 로그인](../Media/LinuxLoginExample.png)

1. Go back to the <bpt id="p1">**</bpt>WIN1<ept id="p1">**</ept> virtual machine. Select the Windows PowerShell used in the previous task.

1. 구체적인 Linux 서버 정보에 맞게 다음 PowerShell 명령을 수정하여 입력하고 Enter 키를 누릅니다.

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. Enter <bpt id="p1">*</bpt>yes<ept id="p1">*</ept> to confirm the connection and then type the user's password and press enter. Your screen should look something like this:

    ![linux 로그인](../Media/PSconnectLinux.png)

1. You are now ready to paste the <bpt id="p1">*</bpt>Download and onboard agent for Linux<ept id="p1">*</ept> command from the earlier step. Make sure that script is in the clipboard. In PowerShell right-click the top bar and choose <bpt id="p1">**</bpt>Edit<ept id="p1">**</ept> and then <bpt id="p2">**</bpt>Paste<ept id="p2">**</ept>.

1. Once the script is pasted, press Enter. The script will run against your Linux server remotely. Wait

1. 완료되면 **종료**를 입력하여 LIN2에 대한 원격 셸 연결을 닫습니다.


### <a name="task-4-configure-the-facilities-you-want-to-collect-and-their-severities-for-the-syslog-connector"></a>작업 4: Syslog 커넥터용으로 수집할 기능 및 해당 심각도 구성

이 작업에서는 Syslog 수집 기능을 구성합니다.

1. Microsoft Sentinel 포털이 열려 있는 Edge 브라우저로 돌아가서 오른쪽 위 모서리에서 ‘x’를 두 번 선택하여 “Log Analytics 작업 영역” 페이지와 “Syslog” 데이터 커넥터 페이지를 닫습니다.

1. Microsoft Sentinel 포털의 구성에서 **설정** 선택한 다음, **작업 영역 설정** 탭을 선택합니다.

1. **설정** 영역에서 **레거시 에이전트 관리**를 선택합니다.

1. **Syslog** 탭을 선택합니다.

1. **+ 기능 추가** 단추를 선택합니다.

1. *기능 이름* 드롭다운 메뉴에서 **인증**을 선택합니다.

1. **+ 기능 추가** 단추를 다시 선택합니다.

1. 기능 이름 드롭다운 메뉴에서 **authpriv**를 선택합니다.

1. **적용**을 선택하여 변경 내용을 저장합니다.

## <a name="proceed-to-exercise-4"></a>연습 4 계속 진행
