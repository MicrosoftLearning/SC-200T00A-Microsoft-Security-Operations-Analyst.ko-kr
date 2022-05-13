---
lab:
  title: 연습 2 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Windows 디바이스 연결
  module: Module 6 - Connect logs to Microsoft Sentinel
ms.openlocfilehash: 9605e4624286654c8d99e1c1fdfc7c88e9508f54
ms.sourcegitcommit: a90325f86a3497319b3dc15ccf49e0396c4bf749
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2022
ms.locfileid: "141493928"
---
# <a name="module-6---lab-1---exercise-2---connect-windows-devices-to-microsoft-sentinel-using-data-connectors"></a>모듈 6 - 랩 1 - 연습 2 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Windows 디바이스 연결

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 조직에 있는 많은 데이터 원본의 로그 데이터를 연결하는 방법을 알아야 합니다. 다음 데이터 원본은 온-프레미스 환경 또는 기타 퍼블릭 클라우드와 같은 Azure 내부 및 외부의 Windows 가상 머신입니다.


### <a name="task-1-create-a-windows-virtual-machine-in-azure"></a>작업 1: Azure에서 Windows 가상 머신 만들기

이 작업에서는 Azure에서 Windows 가상 머신을 만듭니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd** 를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음** 을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호** 를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인** 을 선택합니다.

1. **+ 리소스 만들기** 를 선택합니다. **힌트:** 이미 Azure Portal에 있는 경우 위쪽 막대에서 *Microsoft Azure* 를 선택하여 홈으로 이동해야 할 수 있습니다.

1. **서비스 및 마켓플레이스 검색** 상자에 *Windows 10* 을 입력하고 드롭다운 목록에서 **Microsoft Window 10** 을 선택합니다.

1. 플랜 드롭다운 목록을 열고 **Windows 10 Enterprise 버전 21H2** 를 선택합니다. **미리 설정된 구성으로 시작** 을 선택하여 계속 진행합니다.

1. **개발/테스트** 를 선택한 다음, **VM 계속 만들기** 를 선택합니다.

1. 리소스 그룹에 대해 **새로 만들기** 를 선택하고, RG-AZWIN01을 이름으로 입력하고, **확인** 을 선택합니다.

    >**참고:** 이는 추적을 위한 새 리소스 그룹입니다. 

1. 가상 머신 이름에 AZWIN01을 입력합니다.

1. 지역 기본값으로 **미국 동부** 를 그대로 둡니다.

1. 아래로 스크롤하여 가상 머신의 크기를 검토합니다. 비어 있는 것 같은 경우 **모든 크기 보기** 를 선택하고 Azure 사용자들이 가장 많이 사용함에서 VM 크기 중 하나를 선택하고 **선택** 을 클릭합니다.

1. 선택한 사용자 이름을 입력합니다. **힌트:** admin 또는 root 같은 예약어를 사용하지 마세요.

1. 선택한 암호를 입력합니다. **힌트:** 테넌트 암호를 다시 사용하는 것이 더 간편할 수 있습니다. 리소스 탭에서 찾을 수 있습니다.

1. 페이지 아래쪽으로 스크롤하고 라이선스 아래 확인란을 선택하여 적격 라이선스가 있는지 확인합니다.

1. **검토 + 만들기** 를 선택하고 유효성 검사를 통과할 때까지 기다립니다.

1. **만들기** 를 선택합니다. 리소스가 작성될 때까지 기다립니다. 몇 분 정도 걸릴 수 있습니다.


### <a name="task-2-connect-an-azure-windows-virtual-machine"></a>작업 2: Azure Windows 가상 머신을 연결합니다.

이 작업에서는 Microsoft Sentinel에 Azure Windows 가상 머신을 연결합니다.

1. Azure Portal의 검색 창에 *Sentinel* 을 입력하고 **Microsoft Sentinel** 을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 데이터 커넥터 탭에서 **레거시 에이전트를 통한 보안 이벤트** 커넥터를 검색하고 목록에서 선택합니다.

1. 커넥터 정보 블레이드에서 **커넥터 페이지 열기** 를 선택합니다.

1. 구성 섹션의 “1. 에이전트 다운로드 및 설치”에서 **Azure Windows 가상 머신에 에이전트 설치** 옵션을 선택합니다.

1. **Azure Windows 가상 머신용 에이전트 다운로드 및 설치** 를 선택합니다. 그러면 Azure 구독에서 사용 가능한 가상 머신이 표시됩니다.

1. 이전 작업에서 방금 만든 **AZWIN01** 가상 머신을 선택한 다음, **연결** 을 선택합니다. “상태”에 이 작업 영역이 표시될 때까지 기다립니다.

1. ‘x’를 선택하여 창을 닫습니다. 구성 섹션의 “2. 스트림할 이벤트 선택”에서 **모든 이벤트** 를 선택한 다음, **변경 내용 적용** 을 선택합니다.


### <a name="task-3-connect-a-non-azure-windows-machine"></a>작업 3: 비 Azure Windows 컴퓨터 연결

이 작업에서는 Microsoft Sentinel에 비 Azure Windows 가상 머신을 연결합니다.

>**중요:** 다음 단계는 이전에 작업한 컴퓨터와는 다른 컴퓨터에서 수행합니다. 가상 머신 이름 참조를 찾습니다.

1. WIN2 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd** 를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저를 엽니다.

1. 브라우저를 열고 이전 랩에서 사용했던 자격 증명으로 Azure Portal(https://portal.azure.com )에 로그인합니다.

1. Azure Portal의 검색 창에 *Sentinel* 을 입력하고 **Microsoft Sentinel** 을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. **데이터 커넥터** 를 선택한 다음, **레거시 에이전트를 통한 보안 이벤트** 커넥터를 검색하고, 목록에서 선택합니다.

1. 커넥터 정보 블레이드에서 **커넥터 페이지 열기** 를 선택합니다.

1. 구성 섹션의 “1. 에이전트 다운로드 및 설치”에서 이제 **비 Azure Windows 컴퓨터에 에이전트 설치** 옵션을 선택합니다.

1. **Azure Windows 이외의 머신용 에이전트 다운로드 및 설치** 를 선택합니다. 

    >**참고:** Log Analytics 작업 영역에는 연결된 2개의 Windows 컴퓨터가 표시됩니다. 이는 이전에 연결된 WINServer 및 AZWIN01 가상 머신에 해당합니다.

1. **Windows 에이전트 다운로드(64비트)** 링크를 선택합니다.

1. 다운로드된 *MMASetup-AMD64.exe* 파일 아래에서 **파일 열기** 를 선택하고 **예** 를 선택하여 표시되는 사용자 계정 컨트롤 창에서 실행 파일을 실행할 수 있도록 합니다.

1. 시작 대화 상자에서 **다음** 을 선택하고, “Microsoft 소프트웨어 사용 조건” 페이지에서 **동의함** 을 선택하고, 대상 프롬프트에서 **다음** 을 선택하여 기본 경로를 그대로 사용합니다.

1. 에이전트 설치 옵션 메시지에서 **Azure Log Analytics(OMS)에 에이전트 연결** 옵션을 선택한 후 **다음** 을 선택합니다.

1. Microsoft Sentinel이 열려 있는 브라우저의 에이전트 관리 페이지에서 **작업 영역 ID** 를 복사하여 대화 상자에 있는 작업 영역 ID에 붙여넣습니다. 

1. Microsoft Sentinel이 열려 있는 브라우저의 에이전트 관리 페이지에서 **기본 키** 를 복사하여 대화 상자에 있는 작업 영역 키에 붙여넣습니다. 

1. **다음** 을 선택하여 구성을 저장합니다.

1. Microsoft 업데이트 페이지에서 **다음** 을 선택합니다.

1. **설치** 를 선택합니다. Microsoft Monitoring Agent 설정이 완료될 때까지 기다립니다.

1. 구성이 완료되면 **마침** 을 선택합니다.


### <a name="task-4-install-and-collect-sysmon-logs"></a>작업 4: Sysmon 설치 및 로그 수집

이 작업에서는 Sysmon을 설치하여 Sysmon 로그를 수집합니다.

>**참고:** 다음 지침에 따라 작업을 수행하면 기본 구성으로 Sysmon이 설치됩니다. 프로덕션 컴퓨터에서 Sysmon을 사용하려면 커뮤니티에서 제공되는 구성을 조사해야 합니다.

1. 브라우저에서 새 탭을 열고 https://docs.microsoft.com/sysinternals/downloads/sysmon 으로 이동합니다.

1. **Sysmon 다운로드** 를 선택하여 해당 페이지에서 Sysmon을 다운로드합니다.

1. *Sysmon.zip* 을 가리키고 폴더 아이콘을 선택합니다. 다운로드한 파일을 마우스 오른쪽 단추로 클릭하고, **모두 추출...** 을 선택하고, **압축을 풀어서 다음 폴더에 저장:** 아래에 *C:\Sysmon* 을 입력하고, **추출** 을 선택합니다. 

1. WIN2의 Windows 작업 표시줄 검색 창에 *명령* 을 입력합니다. 검색 결과에 명령 프롬프트 앱이 표시됩니다. 명령 프롬프트 앱을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행** 을 선택합니다. 표시되는 사용자 계정 컨트롤 창에서 **예** 를 선택하여 앱을 실행할 수 있도록 합니다.

1. *cd \sysmon* 을 입력합니다.

1. *notepad sysmon.xml* 을 입력하여 새 파일을 만듭니다. **예** 를 선택하여 파일 만들기를 확인합니다.

1. 브라우저에서 새 탭을 열고 https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml 로 이동합니다.

1. **원시** 단추를 선택합니다. 모두 선택하고 GitHub에서 해당 파일의 콘텐츠를 복사하여 방금 만든 sysmon.xml 메모장 파일에 다시 붙여넣습니다.

1. 메모장에서 **파일** 을 선택한 다음, **저장** 을 선택하여 파일을 저장합니다.

1. 명령 프롬프트로 돌아가서 다음을 입력하고 Enter 키를 누릅니다. **sysmon.exe -accepteula -i sysmon.xml**

    >**중요:** 출력에 "Configuration file validated" 및 "Sysmon started" 메시지가 나타나는지 확인합니다. 표시되지 않는 경우 데이터가 제대로 복사되고 sysmon.xml 파일이 저장되었는지 확인합니다.

1. 브라우저에서 Azure Portal(https://portal.azure.com )이 열려 있는 탭으로 다시 이동합니다. 

1. Azure Portal의 검색 창에서 *Sentinel* 을 입력한 다음, **, Microsoft Sentinel** 을 선택하고, 이전에 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. Microsoft Sentinel의 구성 영역에서 **설정** 을 선택한 다음, **작업 영역 설정 >** 탭을 선택합니다.

1. 설정 영역에서 **에이전트 구성** 을 선택합니다. **Windows 이벤트 로그** 탭은 기본적으로 선택됩니다.

1. **+ Windows 이벤트 로그 추가** 단추를 선택합니다.

1. 로그 이름 필드에 **Microsoft-Windows-Sysmon/Operational** 을 입력합니다.

1. **적용** 을 선택합니다. 이를 통해 이벤트 뷰어에서 Sysmon에 의해 생성된 모든 이벤트를 수집합니다.


### <a name="task-5-onboard-microsoft-defender-for-endpoint-device"></a>작업 5: 엔드포인트용 Microsoft Defender 디바이스 온보딩

이 작업에서는 엔드포인트용 Microsoft Defender에 디바이스를 온보딩합니다.

>**매우 중요**: 이 과정의 “모듈 2 - 연습 1”에 대한 랩을 완료하고 지금까지 가상 머신을 저장한 경우 이 작업을 건너뛸 수 있습니다. 그렇지 않으면 WIN1 컴퓨터를 엔드포인트용 Defender에 다시 온보딩해야 합니다.

>**중요:** 다음 단계는 이전에 작업한 컴퓨터와는 다른 컴퓨터에서 수행합니다. 가상 머신 이름 참조를 찾습니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd** 를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Microsoft 365 Defender 포털(https://security.microsoft.com) )로 이동하고, 현재 포털에 없는 경우 **테넌트 메일** 자격 증명으로 로그인합니다.

1. 왼쪽 메뉴 모음에서 **설정** 을 선택한 다음 설정 페이지에서 **엔드포인트** 를 선택합니다.

1. 디바이스 관리 섹션에서 **온보딩** 을 선택합니다.

1. **온보딩 패키지 다운로드** 를 선택합니다.

1. 다운로드한 .zip 파일의 압축을 풉니다.

1. Windows 명령 프롬프트를 **관리자** 권한으로 실행합니다. 사용자 계정 컨트롤 메시지가 표시되면 실행에 동의합니다.

1. 방금 관리자 권한으로 압축을 푼 WindowsDefenderATPLocalOnboardingScript.cmd 파일을 실행합니다. **참고:** 이 파일의 기본 위치는 c:\users\admin\downloads 디렉터리입니다. 스크립트에서 표시되는 질문에 답변으로 Y 키를 누릅니다. 

1. 포털의 온보딩 페이지에서 검색 테스트 스크립트를 복사한 다음 열린 명령 창에서 실행합니다. 새 **관리자: 명령 프롬프트** 창을 열어야 할 수도 있습니다. 이 창을 열려면 Windows 검색 창에 *CMD* 를 입력하고 **관리자 권한으로 실행** 을 선택합니다.

1. 엔드포인트 영역의 Microsoft 365 Defender 포털에서 **디바이스 인벤토리** 를 선택합니다. 이제 목록에 디바이스가 표시됩니다.

## <a name="proceed-to-exercise-3"></a>연습 3 계속 진행
