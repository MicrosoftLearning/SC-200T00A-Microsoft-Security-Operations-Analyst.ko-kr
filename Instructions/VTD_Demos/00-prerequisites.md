
# Microsoft 보안 운영 분석가
트레이너 준비 가이드:

## 목적

이 문서는 `Defend Against Threats with Extended Detection and Response` 및 `Configure Security Operations Using Microsoft Sentinel`에 대한 Microsoft 보안 가상 학습일 학습을 준비하는 발표자에게 유용합니다. 이 자료는 SC-200: Microsoft 보안 작업 분석가 인증 시험의 일부입니다.

## 데모 필수 구성 요소

이 과정의 랩을 진행하려면 Microsoft 365 E5 사용 허가를 받은 테넌트와 Azure 구독이 필요합니다.

* 자신을 위해 Microsoft Learning Azure Pass를 요청할 수 있습니다.
* 데모를 수행하기 최소 2주 전에 이러한 패스를 요청해야 합니다. 패스를 받으면 해당 패스를 활성화해야 합니다. 
* Azure Pass는 공개적으로 사용할 수 있는 Microsoft Azure 평가판 구독과 동일한 방식으로 효과적으로 작동합니다. 즉, Pass를 사용하여 수행할 수 있는 작업이 제한됩니다.
* 랩 지침은 [SC-200 Microsoft Learning GitHub 리포지토리](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/)에 있습니다.
* 데모에 사용할 컴퓨터에는 최신 Microsoft Edge 브라우저가 설치되어 있어야 합니다.

## Azure Pass 활성화

## 엔드포인트용 Defender 배포

### Microsoft 365 자격 증명 가져오기

랩을 시작하면 Microsoft Virtual Lab 환경에서 액세스할 수 있도록 무료 평가판 테넌트가 제공됩니다. 이 테넌트에는 고유한 사용자 이름과 암호가 자동으로 할당됩니다. Microsoft Virtual Lab 환경 내에서 Azure와 Microsoft 365에 로그인할 수 있도록 이 사용자 이름과 암호를 검색해야 합니다.

이 과정은 학습 파트너가 여러 승인된 랩 호스팅 공급자 중 하나를 통해 제공하는 것입니다. 따라서 테넌트와 연결된 테넌트 ID를 검색하는 실제 단계는 랩 호스팅 공급자별로 다를 수 있습니다. 그러므로 과정에서 이 정보를 검색하는 방법과 관련된 필요한 지침은 강사가 제공합니다. 나중에 사용할 수 있도록 기록해 두어야 하는 정보는 다음과 같습니다.

    - **테넌트 접미사 ID.** 랩 전반에서 Microsoft 365에 로그인하는 데 사용할 onmicrosoft.com 계정용 ID입니다. 이 ID의 형식은 **{username}@M365xZZZZZZ.onmicrosoft.com**입니다. 여기서 ZZZZZZ는 랩 호스팅 공급자가 제공한 고유 테넌트 접미사 ID입니다. 나중에 사용할 수 있도록 이 ZZZZZZ 부분의 내용을 기록해 둡니다. 랩 단계를 진행할 때 Microsoft 365 포털에 로그인하라는 메시지가 표시되면 여기서 적어 둔 ZZZZZZ 값을 입력해야 합니다.
    - **테넌트 암호.** 랩 호스팅 공급자가 제공한 관리자 계정의 암호입니다.
    

### 엔드포인트용 Microsoft Defender 초기화

이 작업에서는 엔드포인트용 Microsoft Defender 초기화를 수행합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Microsoft 365 Defender 포털(https://security.microsoft.com))로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

**Microsoft 365 Defender** 포털의 탐색 메뉴 왼쪽에서 **홈**을 선택합니다.

    >**Note:** You may need to scroll all the way to the menu top.

1. **홈** 포털 페이지에 **Microsoft 365 Defender 시작**이 표시됩니다.

1. **Microsoft 365 Defender 켜기** 메시지가 있는 **Microsoft 365 Defender**라는 타일을 찾을 때까지 타일을 아래로 스크롤합니다.

    >**힌트:** 타일의 오른쪽 하단에 있어야 합니다.

1. **새 기능 켜기** 단추를 선택합니다.

1. 페이지 상단에 *로드 및 초기화 중*이라는 메시지가 잠시 표시된 다음 커피 머그 이미지와 다음 메시지가 표시됩니다. **잠시 기다려 주세요! 데이터에 사용한 새 공간을 준비하고 연결하고 있습니다.** 완료하는 데 약 5분 정도 소요됩니다. *다음 랩에 필요하므로 페이지를 열어두고 완료되었는지 확인합니다.*

    >**참고:** "잠깐만요! 데이터를 위한 새 공간을 준비하고 연결하는 중입니다."라는 메시지가 나타나지 않거나 "설정 > Microsoft 365 Defender > 계정" 페이지가 열립니다. 그러나 "데이터 저장 위치를 로드하지 못했습니다. 나중에 다시 시도하세요"라는 메시지가 표시되는 경우 "일반" 메뉴에서 "경고 서비스 설정"을 선택하거나 탐색 메뉴로 이동하여 "자산" 섹션까지 아래로 스크롤한 후 "장치"를 선택합니다.

1. 새 공간이 성공적으로 완료되면 계정, 이메일 경고, 경고 서비스 설정, 권한 및 역할, 스트리밍 API에 대한 Microsoft 365 Defender 일반 설정이 표시됩니다. 또한 **미리 보기 기능**이 켜져 있는 것을 볼 수 있습니다.

**참고**: 호스트된 랩 환경에서는 데이터 스토리지 위치가 선택되어 있습니다. 또한 이 학습 테넌트가 관리되는 적절한 지리에 있습니다. 여전히 데이터 보존 길이를 선택할 수 있지만 필수는 아닙니다.

1. **설정**에서 **엔드포인트**를 선택합니다.

1. 디바이스 관리 섹션에서 **온보딩**을 선택합니다.

    >**참고:** 왼쪽 메뉴 모음의 **자산** 섹션에서 디바이스 온보딩을 수행할 수도 있습니다. 자산을 확장하고 디바이스를 선택합니다. 디바이스 인벤토리 페이지에서 컴퓨터 및 모바일이 선택된 상태에서 **디바이스 온보딩**까지 아래로 스크롤합니다. 그러면 **설정 > 엔드포인트** 페이지로 이동합니다.

1. "1. 디바이스 온보딩" 영역에서 배포 방법 드롭다운에 "로컬 스크립트(최대 디바이스 10대에 사용 가능)"가 표시되었는지 확인하고 **온보딩 패키지 다운로드** 단추를 선택합니다.

1. Documents 폴더 등의 로컬 폴더에 다운로드한 zip 파일의 압축을 풉니다.

1. 압축을 푼 WindowsDefenderATPLocalOnboardingScript.cmd 파일을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.  Windows SmartScreen이 표시되면 실행을 선택합니다.

**참고** 이 파일의 기본 위치는 c:\users\admin\downloads 디렉터리입니다.
    
1. 스크립트에서 표시되는 질문에 답변으로 **Y** 키를 누릅니다. 스크립트 실행이 완료되면 "Successfully onboarded machine..."과 같은 메시지가 명령 화면에 표시됩니다. 

1. 포털의 온보딩 페이지에서 검색 테스트 스크립트를 복사한 다음 열린 명령 창에서 실행합니다.  새 **관리자: 명령 프롬프트** 창을 열어야 할 수도 있습니다. 이 창을 열려면 Windows 검색 창에 *CMD*를 입력하고 **관리자 권한으로 실행**을 선택합니다.

1. Microsoft 365 Defender 포털 메뉴에서 **디바이스 인벤토리**를 선택합니다. 이제 목록에 디바이스가 표시됩니다.

**참고** 디바이스가 포털에 표시되려면 최대 5분이 걸릴 수 있습니다.


### 역할 구성

이 작업에서는 디바이스 그룹에 사용할 역할을 구성합니다.

1. Microsoft 365 Defender 포털의 왼쪽 메뉴 모음에서 **설정**을 선택합니다. 

1. **엔드포인트**를 선택하고 권한 영역에서 **역할**을 선택합니다.

1. **역할 켜기** 단추를 선택합니다.

1. **항목 추가**를 선택합니다.

1. 역할뷰 추가 대화 상자에서 다음 정보를 입력합니다.

    |일반 설정|값|
    |---|---|
    |역할 이름|**계층 1 지원**|
    |사용 권한|라이브 응답 기능 - 고급|

1. **다음**을 선택합니다.

1. 할당된 사용자 그룹 탭에서 **sg-IT**를 선택하고 **선택한 그룹 추가**를 선택합니다.

1. **저장**을 선택합니다.

### 디바이스 그룹 구성

이 작업에서는 액세스 제어 및 자동화 구성이 가능하도록 디바이스 그룹을 구성합니다.

1. 왼쪽 메뉴 모음에서 **설정**을 선택합니다. 

1. **엔드포인트**를 선택하고 권한 영역에서 **디바이스 그룹**을 선택합니다.

1. 디바이스 그룹 **추가**를 선택합니다.

1. 일반 탭에서 다음 정보를 입력합니다.

    |일반 설정|값|
    |---|---|
    |디바이스 그룹 이름|**Regular**|
    |자동화 수준|전체 - 자동으로 위협 수정|

1. **다음**을 선택합니다.

1. . 디바이스 탭에서 OS 조건으로 **Windows 10**을 선택하고 **다음**을 선택합니다.

1. 디바이스 미리 보기 탭에서 **미리 보기 표시**를 선택하여 WIN1 가상 머신을 확인합니다. **다음**을 선택합니다. 
**힌트:** 미리 보기 목록에 가상 머신이 표시되지 않으면 돌아가서 OS 조건에 대해서도 없음을 선택합니다.** VM에 대한 데이터가 아직 채워지지 않았습니다.

1. 사용자 액세스 탭에서 **sg-IT**를 선택하고 **선택한 그룹 추가**를 선택합니다.

1. **완료**를 선택합니다.

1. 디바이스 그룹 구성이 변경되었습니다. **변경 내용 적용**을 선택하여 일치 항목을 확인하고 그룹화를 다시 계산합니다.

1. 이제 방금 만든 “일반” 및 동일한 수정 수준을 가진 “그룹화되지 않은 디바이스(기본값)”의 두 가지 디바이스 그룹을 포함하려고 합니다.

<!--- 
## Deploy sample alerts for Demo in Module 3

In this task, you will load sample security alerts and review the alert details.

1. In the Edge browser, open the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Defender*, then select **Microsoft Defender for Cloud**.

1. In the **Getting Started** menu the default selection is **Upgrade**, select or **Skip** for now.

1. Select **Security alerts** in the portal menu.

1. Select **Sample Alerts** from the command bar.

1. In the Create sample alerts (Preview) pane make sure your subscription is selected.  Make sure all sample alerts are selected and select **Create sample alerts**.  

**Note** This may take a few minutes to complete. --->

## 모듈 4에서 데모용 Microsoft Sentinel 작업 영역 배포

이 작업에서는 Microsoft Sentinel 작업 영역을 만듭니다.

 >**참고:** 다음 데모를 위해서는 Azure Pass 또는 기타 Azure 구독이 활성화되어 있어야 합니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. **+ 만들기**를 선택합니다.

1. 그런 다음 **+ 새 작업 영역 만들기**를 선택합니다.

**참고** 먼저 새 Log Analytics 작업 영역을 만듭니다.

1. 적절한 구독을 선택합니다.

1. 리소스 그룹에서 **새로 만들기** 링크를 선택하고 원하는 새 리소스 그룹 이름을 입력합니다.

1. 이름 필드의 인스턴스 정보 아래에 원하는 Log Analytics 작업 영역 이름을 입력합니다.

**참고:** 이 이름은 고유해야 하며 Microsoft Sentinel 작업 영역 이름이기도 합니다.

1. 적절한 지역을 선택합니다.  적절한 지역이 기본값으로 설정되어 있을 수도 있고, 강사가 선택해야 하는 지역을 구체적으로 알려 줄 수도 있습니다.  

1. **검토 + 생성**를 선택합니다.

1. **만들기**를 선택합니다. 작업 영역에 Microsoft Sentinel 추가 페이지에 있는 목록에 새 Log Analytics 작업 영역이 표시될 때까지 기다립니다.  1분 정도 걸릴 수 있습니다.

1. 새로 만든 작업 영역이 표시되면 선택하고 **추가**를 선택합니다.

## Microsoft Sentinel용 콘텐츠 허브 솔루션 및 데이터 커넥터 배포

### 작업 1: Microsoft Sentinel 작업 영역에 액세스

이 작업에서는 Microsoft Sentinel 작업 영역에 액세스합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 브라우저를 열고 Microsoft Edge 브라우저를 검색하여 다운로드한 후 새로 설치합니다. 새 Edge 브라우저를 시작합니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 이전 랩에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

### 작업 2: Azure 활동 데이터 커넥터를 연결합니다.

이 작업에서는 *Azure Activity* 데이터 커넥터를 연결합니다.

1. Microsoft Sentinel 왼쪽 메뉴에서 *콘텐츠 관리* 섹션까지 아래로 스크롤하고 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **Azure Activity** 솔루션을 검색하고 목록에서 선택합니다.

1. *클라우드용 Microsoft Defender* 솔루션 페이지에서 **설치**를 선택합니다.

1. 설치가 완료되면 **관리**를 선택합니다.

    >**참고:** *Azure Activity* 솔루션은 *Azure Activity* 데이터 커넥터, 12개의 분석 규칙, 14개의 헌팅 쿼리 및 1개의 통합 문서를 설치합니다.

1. *Azure Activity* 데이터 커넥터를 선택하고 **커넥터 페이지 열기**를 선택합니다.

1. *지침* 탭 아래의 *구성* 영역에서 "2. 구독 연결..."까지 아래로 스크롤하고 **Azure Policy 할당 마법사 시작>** 을 선택합니다.

1. **기본 사항** 탭의 **범위** 아래에서 줄임표 단추(...)를 선택하고, 드롭다운 목록에서 “Azure Pass - 스폰서쉽” 구독을 선택하고, **선택**을 클릭합니다.

1. **매개 변수** 탭을 선택하고 **기본 Log Analytics 작업 영역** 드롭다운 목록에서 작업 영역을 선택합니다. 이 작업은 구독 구성을 적용하여 Log Analytics 작업 영역에 정보를 보냅니다.

1. **수정** 탭에서 **수정 작업 만들기** 확인란을 선택합니다. 이 작업은 기존 Azure 리소스에 정책을 적용합니다.

1. **검토 + 만들기** 단추를 선택하여 구성을 검토합니다.

1. **만들기**를 선택하여 완료합니다.

### 작업 3: Azure에서 Windows 가상 머신 만들기

이 작업에서는 Azure에서 Windows 가상 머신을 만듭니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저에서 https://portal.azure.com의 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. 
          **+ 리소스 만들기**를 선택합니다. **힌트:** 이미 Azure Portal에 있는 경우 위쪽 막대에서 *Microsoft Azure*를 선택하여 홈으로 이동해야 할 수 있습니다.

1. **서비스 및 마켓플레이스 검색** 상자에 *Windows 10*을 입력하고 드롭다운 목록에서 **Microsoft Window 10**을 선택합니다.

1. **Microsoft Window 10** 상자를 선택합니다.

1. *플랜* 드롭다운 목록을 열고 **Windows 10 Enterprise 버전 22H2**를 선택합니다.

1. **미리 설정된 구성으로 시작**을 선택하여 계속 진행합니다.

1. **개발/테스트**를 선택한 다음, **VM 계속 만들기**를 선택합니다.

1. *리소스 그룹*에 대해 **새로 만들기**를 선택하고 이름으로 `RG-AZWIN01`을 입력한 후 **확인**을 선택합니다.

    >**참고:** 이는 추적을 위한 새 리소스 그룹입니다. 

1. *가상 머신 이름*에 `AZWIN01`을 입력합니다.

1. 지역 기본값으로 **미국 동부**를 그대로 둡니다.**

1. 아래로 스크롤하여 가상 머신의 *이미지*를 검토합니다. 비어 있는 경우 **Windows 10 Enterprise, 버전 22H2**를 선택합니다.

1. 가상 머신의 *크기*를 검토합니다. 비어 있는 것 같은 경우 **모든 크기 보기**를 선택하고 *Azure 사용자들이 가장 많이 사용함*에서 첫 번째 VM 크기를 선택하고 **선택**을 선택합니다.

    >**참고:** 다음 메시지가 표시되면: *이 이미지는 Azure Automanage에서 지원되지 않습니다. 이 기능을 사용하지 않도록 설정하려면 관리 탭으로 이동합니다. 그렇지 않은 경우 지원되는 이미지를 선택합니다.* 관리 탭으로 이동하여 "Automanage"를 사용하지 않도록 설정합니다. 나중에 만들기 프로세스가 성공합니다.

1. 아래로 스크롤하여 선택한 *사용자 이름*을 입력합니다. **힌트:** admin 또는 root 같은 예약어를 사용하지 마세요.

1. 선택한 암호를 입력합니다.** **힌트:** 테넌트 암호를 다시 사용하는 것이 더 간편할 수 있습니다. {b>리소스<b} 탭에서 찾을 수 있습니다.

1. 페이지 아래쪽으로 스크롤하고 라이선스 아래 확인란을 선택하여 적격 라이선스가 있는지 확인합니다.**

1. **검토 + 만들기**를 선택하고 유효성 검사를 통과할 때까지 기다립니다.

    >**참고:** *네트워킹* 유효성 검사에 실패한 경우 해당 탭을 선택하고 콘텐츠를 검토한 다음 다시 **검토 + 만들기**를 선택합니다.

1. **만들기**를 실행합니다. 리소스가 작성될 때까지 기다립니다. 몇 분 정도 걸릴 수 있습니다.

### 작업 4: Azure Windows 가상 머신을 연결합니다.

이 작업에서는 Microsoft Sentinel에 Azure Windows 가상 머신을 연결합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 1. Microsoft Sentinel 왼쪽 메뉴에서 *콘텐츠 관리* 섹션까지 아래로 스크롤하고 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **Windows 보안 이벤트** 솔루션을 검색하고 목록에서 선택합니다.

1. *Windows 보안 이벤트* 솔루션 페이지에서 **설치**를 선택합니다.

1. 설치가 완료되면 **관리**를 선택합니다.

    >**참고:** *Windows 보안 이벤트* 솔루션은 *AMA를 통한 Windows 보안 이벤트*와 *레거시 에이전트를 통한 보안 이벤트* 데이터 커넥터를 모두 설치합니다. 또한 2개의 통합 문서, 20개의 분석 규칙 및 43개의 헌팅 쿼리가 포함되어 있습니다.

1. *AMA를 통한 Windows 보안 이벤트* 데이터 커넥터를 선택하고 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

1. *구성* 섹션의 *지침* 탭에서 **데이터 수집 규칙 만들기**를 선택합니다.

1. 규칙 이름에 **AZWINDCR**을 입력하고 **다음: 리소스**를 선택합니다.

1. **+리소스 추가**를 선택하여 앞서 만든 가상 머신을 선택합니다.

1. **RG-AZWIN01**을 확장한 다음, **AZWIN01**을 선택합니다.

1. **적용**을 선택한 후 **다음: 수집**을 선택합니다.

1. 다양한 보안 이벤트 컬렉션 옵션을 검토합니다. *모든 보안 이벤트*를 유지하고 **다음: 검토 + 만들기**를 선택합니다.

1. 데이터 수집 규칙을 저장하려면 **만들기**를 선택합니다.

1. 잠시 기다린 다음, **새로 고침**을 선택하여 나열된 새 데이터 수집 규칙을 확인합니다.

### 작업 5: Azure Arc 설치 및 온-프레미스 서버 연결

이 작업에서는 더 쉽게 온보딩할 수 있도록 온-프레미스 서버에 Azure Arc를 설치합니다.

>**중요:** 다음 단계는 이전에 작업한 컴퓨터와는 다른 컴퓨터에서 수행합니다. 가상 머신 이름 참조를 찾습니다.

1. **WINServer** 가상 머신에 Administrator로 로그인합니다. 암호로는 **Passw0rd!** 를 사용합니다. 사용합니다(필요한 경우).  

1. Microsoft Edge 브라우저를 열고 https://portal.azure.com에 있는 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Arc*를 입력하고 **Azure Arc**를 선택합니다.

1. **인프라** 아래 탐색 창에서 **컴퓨터**를 선택합니다.

1. **+ 추가/만들기**를 선택한 다음 **컴퓨터 추가**를 선택합니다.

1. "단일 서버 추가" 섹션에서 **스크립트 생성**을 선택합니다.

1. *필수 조건* 탭을 읽은 후 **다음**을 선택하여 계속합니다.

1. *Azure Arc를 사용하여 서버 추가* 페이지의 *프로젝트 세부 정보*에서 이전에 만든 리소스 그룹을 선택합니다. **힌트:** *RG-Defender*

    >**참고:** 리소스 그룹을 아직 만들지 않은 경우 다른 탭을 열고, 리소스 그룹을 만들고, 다시 시작합니다.

1. 서버 세부 정보 및 연결 방법 옵션을 검토합니다.**** 기본값을 유지하고 **다음**을 선택하여 태그 탭으로 이동합니다.

1. 사용 가능한 기본 태그를 검토합니다. **다음**을 선택하여 스크립트 다운로드 및 실행 탭으로 이동합니다.

1. 아래로 스크롤하여 **다운로드** 단추를 선택합니다. **힌트:** 브라우저에서 다운로드를 차단하는 경우 브라우저에서 다운로드를 허용하도록 설정합니다. Edge 브라우저에서 필요한 경우 줄임표 단추(...)를 선택한 다음, **유지**를 선택합니다.

1. Windows 시작 단추를 마우스 오른쪽 단추로 클릭하고 **Windows PowerShell(관리자)** 을 선택합니다.

1. UAC 프롬프트가 표시되면 “사용자 이름”으로 *Administrator*를 입력하고 “암호”로 *Passw0rd*를 입력합니다.

1. 입력: cd C:\Users\Administrator\Downloads

    >**중요:** 이 디렉터리가 없는 경우에는 잘못된 머신에서 수행하고 있을 가능성이 큽니다. 작업 4의 시작 부분으로 돌아가서 WINServer로 변경하고 다시 시작합니다.

1. *Set-ExecutionPolicy -ExecutionPolicy Unrestricted*를 입력하고 Enter 키를 누릅니다.

1. 모두 예에 해당하는 **A** 키를 누른 다음 Enter 키를 누릅니다.

1. *.\OnboardingScript.ps1*을 입력하고 Enter 키를 누릅니다.  

    >**중요:** “.\OnboardingScript.ps1 용어가 인식되지 않음...”이라는 오류가 표시되는 경우 WINServer 가상 머신에서 작업 4에 대한 단계를 수행하고 있는지 확인합니다.** 여러 다운로드로 인해 파일 이름이 변경되는 다른 문제가 있을 수 있습니다. 실행 중인 디렉터리에서 *“.\OnboardingScript (1).ps1”* 또는 다른 파일 번호를 검색합니다.

1. **R** 키를 눌러 한 번 실행하고 Enter 키를 누릅니다(몇 분 정도 걸릴 수 있음).

1. 설정 프로세스에서 새 Edge 브라우저 탭을 열어 Azure Arc 에이전트를 인증합니다. 관리자 계정을 선택하고 "인증 완료" 메시지가 표시되기를 기다린 후 Windows PowerShell 창으로 돌아갑니다.

1. 설치가 완료되면 스크립트를 다운로드한 Azure Portal 페이지로 돌아가서 **닫기**를 선택합니다. **Azure Arc를 사용하여 서버 추가**를 닫고 Azure Arc **컴퓨터** 페이지로 돌아갑니다.

1. WINServer 서버 이름이 표시되고 상태가 연결될 때까지**새로 고침**을 선택합니다.**

    >**참고:** 이 과정은 몇 분 정도 걸릴 수 있습니다.


### 작업 6: 온-프레미스 서버 보호

이 작업에서는 Azure Arc에 연결된 비 Azure Windows 가상 머신을 Microsoft Sentinel에 추가합니다.  

   >**참고:** AMA를 통한 Windows 보안 이벤트 데이터 커넥터는 비 Azure 디바이스에 대한 Azure Arc가 필요합니다.**

1. Microsoft Sentinel 작업 영역의 *AMA를 통한 Windows 보안 이벤트* 데이터 커넥터 구성에 있어야 합니다.

1. **지침** 탭의 *구성* 섹션에서 *연필* 아이콘을 선택하여 **AZWINDCR** *데이터 수집 규칙*을 편집합니다.

1. **다음: 리소스** 및 **+리소스 추가**.

1. 만든 리소스 그룹을 확장한 다음 **WINServer**를 선택합니다.

    >**중요:** WINServer가 표시되지 않으면 이 서버에 Azure Arc를 설치한 학습 경로 3, 연습 1, 작업 4를 참조하세요.

1. **적용**을 선택합니다.

1. **다음: 수집**을 선택하고 **다음: 검토 + 만들기**를 선택합니다.

1. *유효성 검사 통과*가 표시되면 **만들기**를 선택합니다.


<!--- ### Task 4: Connect the Microsoft Defender for Cloud connector.

In this task, you will connect the Microsoft Defender for Cloud connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Cloud** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 5: Connect the Microsoft Defender for Cloud Apps connector.

In this task, you will connect theMicrosoft Defender for Cloud Apps connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Cloud Apps** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the **Instructions** tab in the **Configuration** section, select **Alerts** and then select **Apply Changes**.

### Task 6: Connect the Microsoft Defender for Office 365 connector.

In this task, you will connect the Microsoft Defender for Office 365 connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Office 365** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select **Connect**.

### Task 7: Connect the Microsoft Defender for Identity connector.

In this task, you will connect the Microsoft Defender for Identity connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Identity** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 8: Connect the Microsoft Defender for Endpoint connector.

In this task, you will connect the Microsoft Defender for Endpoint connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Endpoint** connector from the list.

1. Select Open connector page on the connector information blade.

1. Select **Connect**.

### Task 9: Connect the Microsoft 365 Defender connector.

In this task, you will connect the Microsoft 365 Defender connector.

1. From the Data Connectors Tab, select the **Microsoft 365 Defender** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select all the checkboxes for Microsoft Defender for Endpoint.

1. Select **Apply Changes**. 

### Task 3: Connect a non-Azure Windows Machine.

In this task, you will connect a non-Azure Windows virtual machine to Microsoft Sentinel.

1. Login to WIN2 virtual machine as Admin with the password: **Pa55w.rd**.  

1. Open the browser, search for, download, and install the new Microsoft Edge browser. Start the new Edge browser.

1. Open a browser and log into the Azure Portal at https://portal.azure.com with your credentials.

1. In the Search bar of the Azure Portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace.

1. From the Data Connectors tab, select the **Security Events via Legacy Agent** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the Select which events to stream area, select **All Events**, then select **Apply Changes**.

1. Select the **Install agent on a non-Azure Windows  Machine**.

**Note:** The instructions for Install agent on a Windows Virtual Machine and Install agent on a non-Azure Windows Machine may be reversed. The links take you to the proper location even with the reversed text.

1. Select **Download & install agent for non-Azure Windows machines**. 

1. Select the link for **Download Windows Agent (64 bit)**.

1. Run the .exe file that is downloaded and confirm and User Account Control prompt that may appear.

1. Select **Next** on the Welcome dialog.

1. Select **I Agree** on the Microsoft Software License Terms page.  On the Destination prompt select **Next**.

1. On the Agent Setup Options prompt, select **Connect the agent to Azure Log Analytics (OMS)** option, then select **Next**.

1. In the browser, copy the **Workspace ID** from the Agents Management page and paste into the Workspace ID in the dialog. 

1. In the browser, copy the **Primary key** from the Agents Management page and paste into the Primary key in the dialog. 

1. Select **Next**.

1. Select **Next** on the Microsoft Update page.

2. Then select **Install**.

### Task 4: Install and collect Sysmon logs.

In this task, you will install and collect Sysmon logs.

You should still be connected to the WIN2 virtual machine.  The following instructions will install Sysmon with the default configuration.  You should research community based configurations for Sysmon to be used on production machines.

1. In the browser, go to https://docs.microsoft.com/sysinternals/downloads/sysmon

1. Download Sysmon from the page by select **Download Sysmon**.

1. Open the downloaded file and extract the files to a new directory c:\sysmon

1. In the Windows Taskbar for WIN2 search box, enter *command*.  The search results will show command prompt app.  Right-click on the command prompt app and select **Run as Administrator**.  Confirm any User Account Control prompts that appear.

1. Enter *cd \sysmon*

1. type *notepad sysmon.xml* to create a new file.

1. Open a tab in the browser and navigate to: https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

1. Copy the contents of that file from Github to the sysmon.xml notepad file you just created and save the file.

1. In the command prompt type the following and press enter:
    sysmon.exe -accepteula -i sysmon.xml

1. In the browser, navigate to the Azure portal at https://portal.azure.com 

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. In Microsoft Sentinel, select **Settings** from the Configuration area and then select **Workspace settings** tab.

1. Make sure your Microsoft Sentinel Workspace is selected.

1. Select **Agents configuration** in Settings.

1. Select the **Windows Event logs** tab.

1. Select **Add windows event log** button.

1. Enter **Microsoft-Windows-Sysmon/Operational** in the Log name field.

1. Select **Apply**. --->

## 공격 실시

### 작업 1: 엔드포인트용 Defender를 사용하여 구성된 Windows 공격

이 작업에서는 엔드포인트용 Microsoft Defender가 구성되어 있는 호스트에서 공격을 수행합니다.

1. 암호를 사용하여 관리자로 `WIN1` 가상 머신에 로그인합니다. **Pa55w.rd**를 사용하여 로그인합니다.  

1. 작업 표시줄의 검색 창에 *명령*을 입력합니다.  검색 결과에 명령 프롬프트가 표시됩니다.  명령 프롬프트를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 사용자 계정 컨트롤 메시지가 표시되면 실행을 확인합니다.

1. 명령 프롬프트의 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.

    ```CommandPrompt
    cd \
    mkdir temp
    cd temp
    ```

1. 다음 명령을 복사하여 실행합니다.

    ```CommandPrompt
    REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
    ```

### 작업 2: C2(명령 및 제어) 공격 만들기

1. 암호를 사용하여 관리자로 `WIN1` 가상 머신에 로그인합니다. **Pa55w.rd**를 사용하여 로그인합니다.  

1. 작업 표시줄의 검색 창에 *명령*을 입력합니다.  검색 결과에 명령 프롬프트가 표시됩니다.  명령 프롬프트를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 사용자 계정 컨트롤 메시지가 표시되면 실행을 확인합니다.

1. 공격 2 - 다음 명령을 복사하여 실행합니다.

    ```CommandPrompt
    notepad c2.ps1
    ```

**예**를 선택하여 새 파일을 만든 후 아래 PowerShell 스크립트를 c2.ps1에 복사하고 **저장**을 선택합니다.

>**참고:** Virtual Machine에 스크립트를 붙여넣을 때는 길이가 제한될 수 있습니다.  전체 스크립트를 가상 머신에 붙여넣으려면 3개 섹션으로 나눠서 붙여넣으세요.  메모장에서 연 c2.ps1 파일 내에서 스크립트가 여기에 나와 있는 지침과 동일하게 표시되는지 확인합니다.

    ```PowerShell
    
    param(
        [string]$Domain = "microsoft.com",
        [string]$Subdomain = "subdomain",
        [string]$Sub2domain = "sub2domain",
        [string]$Sub3domain = "sub3domain",
        [string]$QueryType = "TXT",
            [int]$C2Interval = 8,
            [int]$C2Jitter = 20,
            [int]$RunTime = 240
    )
    
    
    $RunStart = Get-Date
    $RunEnd = $RunStart.addminutes($RunTime)
    
    $x2 = 1
    $x3 = 1 
    Do {
        $TimeNow = Get-Date
        Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
    
        if ($x2 -eq 3 )
        {
            Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
            
            $x2 = 1
    
        }
        else
        {
            $x2 = $x2 + 1
        }
        
        if ($x3 -eq 7 )
        {
    
            Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
    
            $x3 = 1
            
        }
        else
        {
            $x3 = $x3 + 1
        }
    
    
        $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
        Start-Sleep -Seconds $Jitter
    }
    Until ($TimeNow -ge $RunEnd)
    ```

명령 프롬프트의 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.

    ```PowerShell
    .\c2.ps1
    ```

>**참고:** 오류를 해결하라는 메시지가 표시됩니다. 이 대화 상자의 표시는 예상된 결과입니다.
이 명령/PowerShell 스크립트를 백그라운드에서 실행하고 창을 닫지 마세요.  명령이 몇 시간 동안 로그 항목을 생성해야 합니다.  이 스크립트가 실행되는 동안 다음 작업과 다음 연습을 진행해도 됩니다.  이 작업에서 생성되는 데이터를 나중에 위협 헌팅 랩에서 사용합니다.  이 프로세스에서 대량의 데이터가 작성되거나 처리되지는 않습니다.

### 작업 2: AMA(Azure Monitor 에이전트)로 구성된 공격 창

이 작업에서는 보안 이벤트 커넥터와 Sysmon이 구성되어 있는 호스트에서 공격을 수행합니다.

1. 이전에 만든 `AZWIN01` 가상 머신을 선택합니다.  

1. 왼쪽 메뉴에서 **작업**까지 아래로 스크롤하고 **명령 실행**을 선택합니다.

1. **명령 실행** 창에서 **RunPowerShellScript**를 선택합니다.

1. 아래 명령을 복사하여 관리자 계정 만들기를 `PowerShell Script` 양식으로 시뮬레이션하고 **실행**을 선택합니다.

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

    >**참고**: 한 줄에 하나의 명령만 있는지 확인하고 사용자 이름을 변경하여 명령을 다시 실행할 수 있습니다.

1. `Output` 창에 `The command completed successfully`가 세 번 표시되어야 합니다.
