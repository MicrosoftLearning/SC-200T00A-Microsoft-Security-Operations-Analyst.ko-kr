---
lab:
  title: 연습 3 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트 연결
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# 학습 경로 8 - 랩 1 - 연습 3 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트 연결

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex3.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 조직에 있는 많은 데이터 원본의 로그 데이터를 연결하는 방법을 알아야 합니다. 여기에는 AMA를 통한 CEF(Common Event Format) 및 레거시 에이전트 데이터 커넥터를 통한 Syslog를 사용하는 Linux virtual machines 의 데이터 원본이 포함됩니다.

>**중요:** 학습 경로 #8에 대한 랩 연습은 *독립 실행형* 환경에 있습니다. 완료하기 전에 랩을 종료하면 구성을 다시 실행해야 합니다.

### 이 랩의 예상 완료 시간은 30분입니다.

>**중요:** 다음 작업에는 서로 다른 가상 머신에서 수행되는 단계가 있습니다. 가상 머신 이름 참조를 찾습니다.

### 작업 1: Microsoft Sentinel 작업 영역에 액세스

이 작업에서는 Microsoft Sentinel 작업 영역에 액세스합니다.

>**참고:** Microsoft Sentinel이 Azure 구독에 **defenderWorkspace**라는 이름으로 사전 배포되었으며 필요한 *콘텐츠 허브* 솔루션이 설치되어 있습니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 새 Microsoft Edge 브라우저를 시작합니다.

1. Edge 브라우저에서 Azure Portal(<https://portal.azure.com> )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel **defenderWorkspace**을 선택합니다.

### 작업 2: Common Event Format 커넥터를 사용하여 Linux 호스트 연결

이 작업에서는 AMA 데이터 커넥터를 통해 CEF(Common Event Format)를 사용하여 Linux 호스트를 Microsoft Sentinel에 연결합니다. 또한 이벤트를 수집하는 DCR(데이터 수집 규칙)을 만듭니다. Azure Arc는 DCR을 만드는 데 필요한 대로 이 Linux 호스트에 미리 설치되었습니다.

1. **LIN1** 가상 머신을 시작합니다. 랩 호스터가 제공한 사용자 이름 및 암호를 사용하여 로그인합니다. **힌트:** 로그인 프롬프트가 표시되면 Enter 키를 눌러야 할 수 있으며, *사용자 이름 및 암호*를 적어두는 것이 좋습니다.

1. LIN1 서버의 IP 주소를 적어 둡니다. 아래 스크린샷을 예제로 참조하세요.

    ![linux 로그인](../Media/LinuxLoginExample.png)

1. **WIN1** 가상 머신으로 돌아갑니다. 새 Microsoft Edge 브라우저를 시작합니다.

1. 작업 표시줄의 검색 양식에 **Windows PowerShell**을 입력한 다음 **Windows PowerShell**을 선택하여 Windows PowerShell을 시작합니다.

1. 구체적인 Linux 서버 정보에 맞게 다음 PowerShell 명령을 수정하여 입력하고 Enter 키를 누릅니다.

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. 예를 입력하여 연결을 확인한 다음, 사용자의 암호를 입력하고 Enter 키를 누릅니다. 화면이 이제 다음과 같이 표시됩니다.

    ![linux 로그인](../Media/PSconnectLinux.png)

1. SSH 세션의 Linux 프롬프트에서 다음 명령을 입력합니다. *Enter 키를 누르지 않습니다.*

    ```cmd
    azcmagent connect -g "defender-RG" -l "EastUS" -s "Subscription ID string"
    ```

1. **구독 ID 문자열**을 랩 호스팅 서비스 공급자가 제공한 *구독 ID*로 바꿉니다(*리소스 탭). 따옴표를 유지해야 합니다.

1. **Enter** 키를 입력하여 명령을 실행합니다(몇 분 정도 걸릴 수 있습니다).

1. *로그인하려면 웹 브라우저를 사용하여 <https://microsoft.com/devicelogin> 페이지를 열고 코드를 메세지를 입력하고* Ctrl+링크를 클릭하여 장치 로그인 페이지를 엽니다. 제공된 코드를 복사하여 *액세스를 허용하려면 코드 입력* 상자에 붙여넣고 **다음**을 선택합니다.

    ![Linux azcmagent 장치 로그인](../Media/device-login.png)

1. *계정 선택* 대화상자에서 랩 호스팅 제공업체가 제공한 **테넌트 전자 메일**을 선택합니다. *인증 완료* 메시지를 기다렸다가 브라우저 탭을 닫고 *명령 프롬프트* 창으로 돌아갑니다. 또는 *로그인* 대화상자가 표시되면 랩 호스팅 제공업체에서 제공한 **테넌트 이메일** 및 **테넌트 암호**를 입력하고 **로그인**을 선택합니다. *인증 완료* 메시지를 기다렸다가 브라우저 탭을 닫고 *명령 프롬프트* 창으로 돌아갑니다.

1. 명령 실행이 완료되면 *명령 프롬프트* 창을 열어두고 다음 명령을 입력하여 연결이 성공했는지 확인합니다.

    ```cmd
    azcmagent show
    ```

1. 명령 출력에서 *에이전트 상태*가 **연결됨**인지 확인합니다. 아직 *PowerShell 명령 프롬프트* 창을 닫지 않습니다.

1. 새 Microsoft Edge 브라우저를 시작합니다.

1. Edge 브라우저에서 Azure Portal(<https://portal.azure.com> )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel **defenderWorkspace**을 선택합니다.

1. Microsoft Sentinel 왼쪽 탐색 메뉴에서 *콘텐츠 관리* 섹션까지 아래로 스크롤하여 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **Common Event Format** 솔루션을 검색하고 목록에서 선택합니다.

1. *Common Event Format* 솔루션 페이지에서 **관리**를 선택합니다.

    >**참고:** *Common Event Format* 솔루션은 AMA를 통한 *CEF(Common Event Format)* 와 기존 에이전트를 통한 *CEF(Common Event Format)* 데이터 커넥터를 모두 설치합니다.

1. *AMA를 통한 CEF(Common Events Format)* 데이터 커넥터를 선택하고 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

1. *구성* 섹션에서 **+데이터 수집 규칙 만들기** 단추를 선택합니다.

1. *데이터 수집 규칙 만들기* 페이지의 *기본* 탭에서 규칙 이름에 **AZLINDCR**을 입력한 후 **다음: 리소스**를 선택합니다.

1. *리소스* 탭의 *범위*에서 *MOC 구독*을 확장합니다.

    >**힌트:** *범위* 열 앞에 있는 ">"를 선택하여 전체 *범위* 계층 구조를 확장할 수 있습니다.

1. **defender-RG**를 확장한 다음 **LIN1**을 선택합니다.

    >**참고:** *LIN1* 가상 머신은 ubuntuxxx와 같은 다른 이름으로 나타날 수 있습니다.

1. **다음: 수집**을 선택합니다. *수집* 탭에서  *LOG_ALERT* 드롭다운 메뉴를 선택하고 **LOG_WARNING**을 선택합니다.

1. **다음: 검토 + 만들기**를 선택하고 **만들기**를 선택합니다. 배포가 완료될 때까지 기다립니다.

    >**참고:** 브라우저를 새로 고쳐야 할 수도 있습니다.

1. 이제 *AMA를 통한 CEF(Common Event Format)* 데이터 커넥터에 **연결됨**이 표시됩니다.

1. 데이터 수집 규칙은 AMA(Azure Monitor 에이전트)를 설치하고 *CEF 수집기* 설치 명령은 CEF 수집기를 설치하기 위해 LIN1 시스템에 사전 배포되었습니다.

1. *PowerShell 명령 프롬프트* 창으로 돌아갑니다.  LIN1 가상 머신에 연결되어 있어야 합니다.

1. Linux 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    ```cmd
    netstat -lnptv
    ```

1. 포트 514에서 수신 대기하는 rsyslog(또는 syslog-ng) 디먼이 표시되어야 합니다.

    >**참고:** *CommonSecurityLog* 테이블에서 CEF 이벤트를 쿼리할 수 있습니다.

1. **종료**를 입력하여 LIN1에 대한 원격 셸 연결을 닫습니다.

### 작업 3: Syslog 커넥터를 사용하여 Linux 호스트 연결

이 작업에서는 Syslog 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트를 연결합니다.

1. Microsoft Sentinel 포털이 열려 있는 Microsoft Edge 브라우저로 돌아가서 오른쪽 상단 모서리에 있는 'x'를 선택하여 "AMA를 통한 CEF(Common Event Format)" 데이터 커넥터 페이지를 닫습니다.

1. Microsoft Sentinel 왼쪽 메뉴에서 *콘텐츠 관리* 섹션까지 아래로 스크롤하고 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **Syslog** 솔루션을 검색하고 목록에서 선택합니다.

1. *Syslog* 솔루션 페이지에서 **관리**를 선택합니다.

    >**참고:** *Syslog* 솔루션은 2개의 *Syslog* 데이터 커넥터, 7개의 분석 규칙, 9개의 헌팅 쿼리, 2개의 파서 및 21개의 통합 문서를 설치합니다.

1. *레거시 에이전트를 통한 Syslog* 데이터 커넥터를 선택하고, 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

1. *구성* 섹션에서 **Azure Linux가 아닌 컴퓨터에 에이전트 설치**를 확장합니다.

1. **Azure 외 Linux 컴퓨터용 에이전트 다운로드 및 설치** 링크를 선택합니다.

    >**참고:** Log Analytics 작업 영역에는 연결된 2개의 Windows 컴퓨터가 표시됩니다.** 이는 이전에 연결된 WINServer 및 AZWIN01 가상 머신에 해당합니다.

1. **Linux 서버** 탭을 선택합니다.

    >**참고:** Log Analytics 작업 영역에는 연결된 1개의 Linux 컴퓨터가 표시됩니다. 이는 이전에 CEF 커넥터와 연결된 LIN1(ubuntu1) 가상 머신에 해당합니다.

1. **Log Analytics 에이전트 지침**을 선택합니다.

1. *Linux용 에이전트 다운로드 및 설치* 영역의 명령을 클립보드에 복사합니다.

1. LIN2 가상 머신을 시작합니다. 랩 호스터가 제공한 암호로 사용자 이름으로 로그인합니다. **힌트:** 로그인 프롬프트를 보려면 Enter 키를 눌러야 할 수 있습니다.

1. LIN2 서버의 IP 주소를 적어 둡니다. 아래 스크린샷을 예제로 참조하세요.

    ![linux 로그인](../Media/LinuxLoginExample.png)

1. **WIN1** 가상 머신으로 돌아갑니다. 이전 작업에 사용된 Windows PowerShell을 선택합니다.

1. 구체적인 Linux 서버 정보에 맞게 다음 PowerShell 명령을 수정하여 입력하고 Enter 키를 누릅니다.

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. 예를 입력하여 연결을 확인한 다음, 사용자의 암호를 입력하고 Enter 키를 누릅니다. 화면이 이제 다음과 같이 표시됩니다.

    ![linux 로그인](../Media/PSconnectLinux.png)

1. 이제 이전 단계의 Linux용 에이전트 다운로드 및 설치 명령을 붙여넣을 준비가 되었습니다. 스크립트가 클립보드에 있는지 확인합니다. PowerShell에서 상단 표시줄을 마우스 오른쪽 단추로 클릭하고 **편집**, **붙여넣기**를 차례로 선택합니다.

1. 스크립트를 붙여넣은 후에 Enter 키를 누릅니다. 스크립트가 Linux 서버에 대해 원격으로 실행됩니다. 연결 시도 간격

1. 완료되면 **종료**를 입력하여 LIN2에 대한 원격 셸 연결을 닫습니다.

### 작업 4: Syslog 커넥터용으로 수집할 기능 및 해당 심각도 구성

이 작업에서는 Syslog 수집 기능을 구성합니다.

1. Microsoft Sentinel 포털이 열려 있는 Edge 브라우저로 돌아가서 오른쪽 위 모서리에서 ‘x’를 두 번 선택하여 “Log Analytics 작업 영역” 페이지와 “Syslog” 데이터 커넥터 페이지를 닫습니다.

1. Microsoft Sentinel 포털의 구성에서 **설정** 선택한 다음, **작업 영역 설정** 탭을 선택합니다.

1. *클래식* 영역에서 **레거시 에이전트 관리**를 선택합니다.

1. **Syslog** 탭을 선택합니다.

1. **+ 기능 추가** 단추를 선택합니다.

1. *기능 이름* 드롭다운 메뉴에서 **인증**을 선택합니다.

1. **+ 기능 추가** 단추를 다시 선택합니다.

1. *시설 이름* 드롭다운 메뉴에서 **syslog**를 선택합니다.

1. **적용**을 선택하여 변경 내용을 저장합니다.

## 연습 4 계속 진행
