---
lab:
  title: 연습 1 - 클라우드용 Microsoft Defender 사용
  module: Module 3 - Mitigate threats using Microsoft Defender for Cloud
ms.openlocfilehash: d9d41d575b31ccbc25d5a89c3a0337fed7371e7b
ms.sourcegitcommit: 175df7de88c9a609f8caf39840664bf992c5b6dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2022
ms.locfileid: "138025451"
---
# <a name="module-3---lab-1---exercise-1---enable-microsoft-defender-for-cloud"></a>모듈 3 - 랩 1 - 연습 1 - 클라우드용 Microsoft Defender 사용

## <a name="lab-scenario"></a>랩 시나리오

여러분은 클라우드용 Microsoft Defender를 사용하여 클라우드 워크로드 보호를 구현하고 있는 회사에서 일하는 보안 운영 분석가입니다.  이 랩에서는 클라우드용 Microsoft Defender를 사용하도록 설정합니다.


### <a name="task-1-access-the-azure-portal-and-set-up-a-subscription"></a>작업 1: Azure Portal 액세스 및 구독 설정

이 연습에서는 이 랩과 이후 랩을 완료하는 데 필요한 Azure 구독을 설정합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd** 를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저를 열거나 이미 열려 있는 경우 새 탭을 엽니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com) )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음** 을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인** 을 선택합니다.

1. Azure Portal의 검색 창에 *구독* 을 입력하고 **구독** 을 선택합니다. 

1. “Azure Pass - 스폰서쉽” 구독이 표시되는 경우(또는 선택한 언어로 동일한 이름) 작업 #2로 진행합니다. 표시되지 않으면 강사에게 테넌트 관리 사용자 자격 증명을 사용하여 Azure 구독을 만드는 방법을 질문하세요. **참고:** 구독 만들기 프로세스에는 최대 10분이 걸릴 수 있습니다. 

    >**중요:** 이러한 랩은 강의 중에 USD $10 미만의 Azure 서비스를 사용하도록 설계되었습니다.


### <a name="task-2-create-a-log-analytics-workspace"></a>작업 2: Log Analytics 작업 영역 만들기

이 작업에서는 클라우드용 Microsoft Defender에서 사용할 Log Analytics 작업 영역을 만듭니다.

1. Azure Portal의 검색 창에 Log Analytics 작업 영역을 입력하고 동일한 서비스 이름을 선택합니다.

1. 명령 모음에서 **+만들기** 를 선택합니다.

1. 리소스 그룹의 **새로 만들기** 를 선택합니다.

1. *RG-Defender* 를 입력하고 **확인** 을 선택합니다.

1. *uniquenameAzureDefender* 와 같은 고유한 이름을 입력합니다.

1. **검토 + 생성** 를 선택합니다.

1. 작업 영역 유효성 검사에 통과하면 **만들기** 를 선택합니다. 새 작업 영역이 프로비전될 때까지 기다립니다. 몇 분 정도 걸릴 수 있습니다.


### <a name="task-3-enable-microsoft-defender-for-cloud"></a>작업 3: 클라우드용 Microsoft Defender 사용

이 작업에서는 클라우드용 Microsoft Defender를 사용하도록 설정하고 구성합니다.

1. Azure Portal의 검색 창에 *Defender* 를 입력하고 **클라우드용 Microsoft Defender** 를 선택합니다.

1. **시작** 페이지의 **업그레이드** 탭 아래에서 구독이 선택되어 있는지 확인한 다음, 페이지 아래쪽에서 **업그레이드** 단추를 선택합니다. 평가판 시작 알림이 표시될 때까지 기다립니다. 약 2분이 걸립니다. **힌트:** 위쪽 막대에서 종 모양 단추를 클릭하여 Azure Portal 알림을 검토할 수 있습니다.

1. 구독에 이미 포함되어 있는 가상 머신에 에이전트를 설치하는 옵션이 다음 페이지에 표시됩니다. **에이전트를 설치하지 않고 계속** 또는 **아무 작업도 하지 않음** 을 선택합니다.

1. 포털 메뉴의 관리 영역에서 **환경 설정** 을 선택합니다.

1. **“Azure Pass - 스폰서쉽”** 구독(또는 사용 중인 언어로 동일한 이름)을 선택합니다. 

1. 모든 클라우드용 Microsoft Defender 플랜 사용에서 사용하도록 설정된 기능과 다음을 위한 Microsoft Defender 열에서 보호된 Azure 리소스를 검토합니다. 

1. 설정 영역에서 **자동 프로비전** 을 선택합니다.

1. 자동 프로비전 - 확장을 검토합니다. **Azure VM용 Log Analytics 에이전트** 가 **꺼짐** 으로 설정되어 있는지 확인합니다.

1. 페이지 오른쪽 위에 있는 ‘x’를 선택하여 설정 페이지를 닫고 **환경 설정** 으로 다시 돌아가서 구독 왼쪽에서 ‘>’을 선택합니다.

1. 이전 *uniquenameDefender* 를 만든 Log Analytics 작업 영역을 선택하여 사용 가능한 옵션과 가격을 검토합니다. **모든 클라우드용 Microsoft Defender 플랜 사용** 을 선택하고 **저장** 을 선택합니다. “작업 영역 uniquenameDefender에 대한 Azure Defender 플랜이 성공적으로 저장되었습니다.” 알림이 표시될 때까지 기다립니다.

    >**참고:** 페이지가 표시되지 않으면 Edge 브라우저를 새로 고치고 다시 시도합니다.


### <a name="task-4-install-azure-arc-on-an-on-premises-server"></a>작업 4: 온-프레미스 서버에 Azure Arc 설치

이 작업에서는 더 쉽게 온보딩할 수 있도록 온-프레미스 서버에 Azure Arc를 설치합니다.

>**중요:** 다음 단계는 이전에 작업한 컴퓨터와는 다른 컴퓨터에서 수행합니다. 가상 머신 이름 참조를 찾습니다.

1. WINServer 가상 머신에 Administrator로 로그인합니다. 암호로는 **Passw0rd!** 를 사용합니다(필요한 경우).  

1. Microsoft Edge 브라우저를 열고 https://portal.azure.com 에 있는 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음** 을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호** 를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인** 을 선택합니다.

1. Azure Portal의 검색 창에 *Arc* 를 입력하고 **Azure Arc** 를 선택합니다.

1. 탐색 창의 **인프라** 아래에서 **서버** 를 선택합니다.

1. **+추가** 를 선택합니다.

1. "단일 서버 추가" 섹션에서 **스크립트 생성** 을 선택합니다.

1. **다음** 을 선택하여 리소스 세부 정보 탭으로 이동합니다.

1. 앞에서 만든 리소스 그룹을 선택합니다. **힌트:** *RG-Defender*

    >**참고:** 리소스 그룹을 아직 만들지 않은 경우 다른 탭을 열고, 리소스 그룹을 만들고, 다시 시작합니다.

1. 서버 세부 정보 및 연결 방법 옵션을 검토합니다.  기본값을 유지하고 **다음** 을 선택하여 태그 탭으로 이동합니다.

1. **다음** 을 선택하여 스크립트 다운로드 및 실행 탭으로 이동합니다.

1. 1\. 구독 등록 단계에서 **등록** 을 선택합니다.

    >**참고:** 처리를 위해 3분 이상 기다립니다.

1. 아래로 스크롤하여 **다운로드** 단추를 선택합니다. **힌트:** 브라우저에서 다운로드를 차단하는 경우 브라우저에서 다운로드를 허용하도록 설정합니다. Edge 브라우저에서 필요한 경우 줄임표 단추(...)를 선택한 다음, **유지** 를 선택합니다. 

1. Windows 시작 단추를 마우스 오른쪽 단추로 클릭하고 **Windows PowerShell(관리자)** 을 선택합니다.

1. UAC 프롬프트가 표시되면 “사용자 이름”으로 *Administrator* 를 입력하고 “암호”로 *Passw0rd* 를 입력합니다.

1. 입력: cd C:\Users\Administrator\Downloads

1. *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* 를 입력하고 Enter 키를 누릅니다.

1. 모두 예에 해당하는 **A** 키를 누른 다음 Enter 키를 누릅니다.

1. *.\OnboardingScript.ps1* 을 입력하고 Enter 키를 누릅니다.  

    >**중요:** “.\OnboardingScript.ps1 용어가 인식되지 않음...”이라는 오류가 표시되는 경우 WINServer 가상 머신에서 작업 4에 대한 단계를 수행하고 있는지 확인합니다. 여러 다운로드로 인해 파일 이름이 변경되는 다른 문제가 있을 수 있습니다. 실행 중인 디렉터리에서 *“.\OnboardingScript (1).ps1”* 또는 다른 파일 번호를 검색합니다.

1. **R** 키를 눌러 한 번 실행하고 Enter 키를 누릅니다(몇 분 정도 걸릴 수 있음).

1. Edge 브라우저로 돌아가서 새 탭을 열고 주소 표시줄에 https://microsoft.com/devicelogin 을 입력합니다.

1. Windows PowerShell 창으로 돌아가서 에이전트를 인증하기 위해 스크립트의 마지막 줄에서 “...코드 입력” 뒤에 표시되는 코드를 복사합니다.

1. Edge 브라우저로 돌아가서 **코드** 상자에 붙여넣고 **다음** 을 선택합니다. 테넌트 관리자 계정을 선택하고 Azure Connected Machine 에이전트에 로그인하려고 하시나요? 창에서 **계속** 을 선택합니다. 

1. Windows PowerShell 창으로 돌아가서 “Azure에 리소스를 온보딩했습니다.”라는 메시지가 표시될 때까지 기다립니다. **참고:** 새 인증 코드가 포함된 메시지 줄이 표시되면 마지막 3단계를 다시 반복해야 합니다.

1. 스크립트를 다운로드한 Azure Portal 페이지로 돌아가서 **닫기** 를 선택합니다. **Azure Arc를 사용하여 서버 추가** 를 닫고 Azure Arc **서버** 페이지로 돌아갑니다.

1. WINServer 서버 이름이 표시될 때까지 **새로 고침** 을 선택합니다.

    >**참고:** 몇 분 정도 걸릴 수 있습니다.


### <a name="task-5-protect-an-on-premises-server"></a>작업 5: 온-프레미스 서버 보호

이 작업에서는 WINServer 가상 머신에 필요한 에이전트를 수동으로 설치합니다.

1. **클라우드용 Microsoft Defender** 로 이동하고 **시작** 페이지를 선택합니다.

1. **시작** 탭을 선택합니다.

1. 아래로 스크롤하고 비 Azure 서버 추가 섹션에서 **구성** 을 선택합니다.

1. 앞에서 만든 작업 영역 옆의 **업그레이드** 를 선택합니다. 이 작업은 몇 분 정도 걸릴 수 있습니다. “작업 영역 uniquenameDefender에 대한 Azure Defender 플랜이 성공적으로 저장되었습니다.” 알림이 표시될 때까지 기다립니다.

1. 앞에서 만든 작업 영역 옆의 **+ 서버 추가** 를 선택합니다.

1. **Windows 에이전트 다운로드(64비트)** 를 선택합니다.

1. **파일 열기** 를 선택하여 다운로드한 *MMASetup-AMD64.exe* 파일을 실행합니다.

1. **에이전트 설치 옵션** 마법사 페이지가 나타날 때까지 **다음** 을 선택하고, **Azure Log Analytics(OMS)에 에이전트 연결** 을 선택한 후, **다음** 을 선택합니다.

1. Azure Portal의 **작업 영역 키** 텍스트 상자에 있는 **작업 영역 ID** 및 **기본 키** 값을 복사하여 해당하는 마법사 페이지 필드에 붙여넣고 **다음** 을 선택합니다.

1. 설치를 계속 진행합니다. 완료되면 **마침** 을 선택합니다.

1. “클라우드용 Microsoft Defender” 포털로 이동하고 **인벤토리** 를 선택합니다.

1. *WINServer* 가상 머신은 최소한 5분 후에 표시됩니다. 보려면 **새로 고침** 을 선택해야 할 수 있습니다. **힌트:** 총 리소스 아래에 숫자 1이 표시되면 필터를 제거하여 *WINServer* 가상 머신을 표시합니다.

1. 다음 랩으로 이동하고 나중에 돌아와서 **클라우드용 Microsoft Defender** 의 **인벤토리** 섹션을 검토할 수 있습니다.

## <a name="proceed-to-exercise-2"></a>연습 2 계속 진행
