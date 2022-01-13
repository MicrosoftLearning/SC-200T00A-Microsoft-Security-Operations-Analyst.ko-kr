
# Microsoft 보안 작업 분석가
트레이너 준비 가이드

## 목적 

이 문서의 목적은 발표자가 Microsoft Security Virtual Training Day에 "보안 현대화 및 위협으로부터 보호"라는 주제로 교육을 실시하는 것을 지원하는 것입니다. 이 자료는 SC-200: Microsoft 보안 작업 분석가 인증 시험의 일부입니다.

## 데모 필수 구성 요소

이 과정의 랩을 진행하려면 Microsoft 365 E5 사용 허가를 받은 테넌트와 Azure 구독이 필요합니다.
* 자신을 위해 Microsoft Learning Azure Pass를 요청할 수 있습니다.
* 데모를 수행하기 최소 2주 전에 이러한 패스를 요청해야 합니다. 패스를 받으면 해당 패스를 활성화해야 합니다. 
* ?? Azure Pass는 공개적으로 사용할 수 있는 Microsoft Azure 평가판 구독과 동일한 방식으로 효과적으로 작동합니다. 즉, 패스를 사용하여 수행할 수 있는 작업이 제한됩니다.
* 랩 지침은 [SC-200 Microsoft Learning GitHub 리포지토리](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/)에 있습니다.
* 데모에 사용할 컴퓨터에는 최신 Microsoft Edge 브라우저가 설치되어 있어야 합니다.

## Azure Pass 활성화

## 엔드포인트용 Defender 배포

### Microsoft 365 자격 증명 받기

랩을 시작하면 Microsoft Virtual Lab 환경에서 액세스할 수 있도록 무료 평가판 테넌트가 제공됩니다. 이 테넌트에는 고유한 사용자 이름과 암호가 자동으로 할당됩니다. Microsoft Virtual Lab 환경 내에서 Azure와 Microsoft 365에 로그인할 수 있도록 이 사용자 이름과 암호를 검색해야 합니다. 

이 과정은 학습 파트너가 여러 승인된 랩 호스팅 공급자 중 하나를 통해 제공하는 것입니다. 따라서 테넌트와 연결된 테넌트 ID를 검색하는 실제 단계는 랩 호스팅 공급자별로 다를 수 있습니다. 그러므로 과정을 진행할 수 있도록 이 정보를 검색하는 방법과 관련된 필요한 지침은 강사가 제공합니다. 나중에 사용할 수 있도록 기록해 두어야 하는 정보는 다음과 같습니다.

	- **테넌트 접미사 ID.** 랩 전반에서 Microsoft 365에 로그인하는 데 사용할 onmicrosoft.com 계정용 ID입니다. 이 ID의 형식은 **{username}@M365xZZZZZZ.onmicrosoft.com** 입니다. 여기서 ZZZZZZ는 랩 호스팅 공급자가 제공한 고유 테넌트 접미사 ID입니다. 나중에 사용할 수 있도록 이 ZZZZZZ 부분의 내용을 기록해 둡니다. 랩 단계를 진행할 때 Microsoft 365 포털에 로그인하라는 메시지가 표시되면 여기서 적어 둔 ZZZZZZ 값을 입력해야 합니다.
	- **테넌트 암호.** 랩 호스팅 공급자가 제공한 관리자 계정의 암호입니다.
	

### 엔드포인트용 Microsoft Defender 초기화

이 작업에서는 엔드포인트용 Microsoft Defender 포털 초기화를 수행합니다.


1.  WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2.  Microsoft Edge 브라우저를 열고 "edge 브라우저 업데이트"를 검색하여 새 Microsoft Edge 브라우저를 다운로드한 후 설치합니다. 호스트된 가상 머신에서 Microsoft Edge의 최신 버전을 실행하려면 이 단계를 수행해야 합니다. 새 Edge 브라우저를 시작합니다.

3.  Edge 브라우저에서 Microsoft Defender 보안 센터(https://securitycenter.microsoft.com)로 이동합니다.

4. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

5. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

**참고**: "이 섹션에 액세스할 수 없습니다."라는 메시지가 표시되면 5 분 동안 기다렸다가 다시 시도합니다.  액세스 규칙이 테넌트를 전파해야 하는 경우도 있기 때문입니다.  

6. **Microsoft 보안 센터** 설정 2단계에서 **다음**을 선택합니다.

7. 3단계 **기본 설정 지정**에서 이 교육 테넌트를 관리하는 데 적합한 데이터 스토리지 위치를 선택합니다.  과정 강사에게 해당 위치를 확인하는 것이 좋습니다.

8. 미리 보기 기능이 **켜기** 상태인지 확인합니다.

9. **다음**을 선택합니다.  

10. **클라우드 인스턴스 만들기**에서 계속을 선택합니다.

11. **엔드포인트용 Microsoft Defender 계정을 만드는 중** 진행률 표시줄이 끝까지 다 차면 4 단계 옵션이 표시됩니다.  **엔드포인트용 Microsoft Defender 사용 시작**을 선택합니다.

12. 설정 완료 안 됨 대화 상자에서 **진행**을 선택합니다.

**참고**: 설정이 **완료**되었습니다.  다음 작업에서는 디바이스를 온보딩합니다.  

### 디바이스 온보딩

이 작업에서는 엔드포인트용 Microsoft Defender에 디바이스를 온보딩합니다.

1. Microsoft Defender 보안 센터(https://securitycenter.microsoft.com)로 이동한 후 현재 포털이 표시되어 있지 않으면 **테넌트 전자 메일** 자격 증명을 사용하여 로그인합니다.

2. 왼쪽 메뉴 모음에서 **설정**을 선택합니다.

3. 디바이스 관리 섹션에서 **온보딩**을 선택합니다.

4. 디바이스 온보딩 영역에서 **패키지 다운로드** 단추를 선택합니다.

5. Documents 폴더 등의 로컬 폴더에 다운로드한 zip 파일의 압축을 풉니다.

6. 압축을 푼 WindowsDefenderATPLocalOnboardingScript.cmd 파일을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.  Windows SmartScreen이 표시되면 실행을 선택합니다.

**참고** 이 파일의 기본 위치는 c:\users\admin\downloads 디렉터리입니다.
    
7. 스크립트에서 표시되는 질문에 답변으로 **Y** 키를 누릅니다. 스크립트 실행이 완료되면 "Successfully onboarded machine..."과 같은 메시지가 명령 화면에 표시됩니다. 

8. 포털의 온보딩 페이지에서 검색 테스트 스크립트를 복사한 다음 열린 명령 창에서 실행합니다.  새 **관리자: 명령 프롬프트** 창을 열어야 할 수도 있습니다. 이 창을 열려면 Windows 검색 창에 *CMD*를 입력하고 **관리자 권한으로 실행**을 선택합니다.

9. Microsoft Defender 보안 센터 포털 메뉴에서 **디바이스 인벤토리**를 선택합니다. 이제 목록에 디바이스가 표시됩니다.

**참고** 디바이스가 포털에 표시되려면 최대 5분이 걸릴 수 있습니다.


### 역할 구성

이 작업에서는 디바이스 그룹에 사용할 역할을 구성합니다.

1. Microsoft Defender 보안 센터 포털의 왼쪽 메뉴 모음에서 **디바이스 인벤토리**를 선택합니다. 

2. 권한 영역에서 **역할**을 선택합니다.

3. **역할 켜기** 단추를 선택합니다.

4. **항목 추가**를 선택합니다.

5. 역할뷰 추가 대화 상자에서 다음 정보를 입력합니다.
    역할 이름: 계층
    라이브 응답 기능: 체크박스 선택
    고급: 선택

6. **다음**을 선택합니다.

7. 할당된 사용자 그룹 탭에서 **sg-IT**를 선택하고 **선택한 그룹 추가**를 선택합니다.

8. **저장**을 선택합니다.


### 디바이스 그룹 구성

이 작업에서는 액세스 제어 및 자동화 구성이 가능하도록 디바이스 그룹을 구성합니다.

1. 왼쪽 메뉴 모음에서 **설정**을 선택합니다. 

2. 권한 영역에서 **디바이스 그룹**을 선택합니다.

3. **디바이스 그룹 추가**를 선택합니다.

4. 일반 탭에서 다음 정보를 입력합니다.

- 디바이스 그룹 이름: 일반
- 자동화 수준: 전체 - 자동으로 위협 수정
- 구성원: 이름 = TESTLAB

5. **다음**을 선택합니다.

6. 사용자 액세스 탭에서 **sg-IT** 를 선택하고 **선택한 그룹 추가**를 선택합니다.

7. **완료**를 선택합니다.

8. 디바이스 그룹 구성이 변경되었습니다. 변경 내용을 적용하여 일치 여부를 확인하고 그룹을 다시 계산합니다.


## 모듈 2에서 데모용 샘플 경고 배포

이 작업에서는 샘플 보안 경고를 로드하여 경고 세부 정보를 검토합니다.

2. Edge 브라우저에서 Azure Portal https://portal.azure.com을 엽니다.

3. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

4. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

5. Azure Portal의 검색 창에 *보안*을 입력하고 **보안 센터**를 선택합니다.

1. 보안 센터를 업그레이드하라는 메시지가 표시되면 맨 아래에 있는 **건너뛰기**를 클릭합니다.

6. 포털 메뉴에서 **보안 경고**를 선택합니다.

7. 명령 모음에서 **샘플 경고**를 선택합니다.

8. 샘플 경고 만들기(미리 보기) 창에서 구독이 선택되어 있는지 확인합니다.  모든 샘플 경고가 선택되었는지 확인하고 **샘플 경고 만들기**를 선택합니다.  

**참고** 이 작업을 완료하는 데 몇 분 정도 걸릴 수 있습니다.

## 모듈 4에서 데모용 Azure Sentinel 작업 영역 배포

이 작업에서는 Azure Sentinel 작업 영역을 만듭니다.

3.  Edge 브라우저에서 Azure Portal https://portal.azure.com으로 이동합니다.

4. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

5. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

6. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Azure Sentinel**을 선택합니다.

7. **+ 만들기**를 선택합니다.

8. 그런 다음 **+ 새 작업 영역 만들기**를 선택합니다.

**참고** 먼저 새 Log Analytics 작업 영역을 만듭니다.

9. 적절한 구독을 선택합니다.

10. 리소스 그룹에서 **새로 만들기** 링크를 선택하고 원하는 새 리소스 그룹 이름을 입력합니다.

11. 이름 필드의 인스턴스 정보 아래에 원하는 Log Analytics 작업 영역 이름을 입력합니다.

**참고:** 이 이름은 Azure Sentinel 작업 영역 이름으로도 사용됩니다.

12. 적절한 지역을 선택합니다.  적절한 지역이 기본값으로 설정되어 있을 수도 있고, 강사가 선택해야 하는 지역을 구체적으로 알려 줄 수도 있습니다.  

13. **검토 + 만들기** 를 선택합니다.

14. **만들기**를 선택합니다. 작업 영역에 Azure Sentinel 추가 페이지의 목록에 새 Log Analytics 작업 영역이 표시될 때까지 기다립니다.  1분 정도 걸릴 수 있습니다.

16. 새로 만든 작업 영역이 표시되면 선택하고 **추가**를 선택합니다.

## Azure Sentinel용 데이터 커넥터 만들기

### 작업 1: Azure Sentinel 작업 영역 액세스

이 작업에서는 Azure Sentinel 작업 영역에 액세스합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 브라우저를 열고 Microsoft Edge 브라우저를 검색하여 다운로드한 후 새로 설치합니다. 새 Edge 브라우저를 시작합니다.

3. Edge 브라우저에서 Azure Portal https://portal.azure.com으로 이동합니다.

4. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

5. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

6. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Azure Sentinel**을 선택합니다.

7. 이전 랩에서 만든 Azure Sentinel 작업 영역을 선택합니다.

### 작업 2: Azure Active Directory 커넥터 연결

이 작업에서는 Azure Active Directory 커넥터를 연결합니다.

1. 구성 영역에서 **데이터 커넥터**를 선택합니다.  데이터 커넥터 페이지의 목록에서 **Azure Active Directory** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. 구성 영역에서 **로그인 로그** 및 **감사 로그** 옵션을 선택하고 **변경 내용 적용**을 선택합니다.

### 작업 3: Azure Active Directory ID 보호 커넥터 연결

이 작업에서는 Azure Active Directory ID 보호 넥터를 연결합니다.

1. 데이터 커넥터 탭의 목록에서 **Azure Active Directory ID 보호** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. **연결** 단추를 선택합니다.

### 작업 4: Azure Defender 커넥터 연결

이 작업에서는 Azure Defender 커넥터를 연결합니다.

1. 데이터 커넥터 탭의 목록에서 **Azure Defender** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. 연결 옵션을 검토합니다. 옵션을 검토만 하고 연결하지는 마세요. 연결 정보만 파악하면 됩니다.

### 작업 5: Microsoft Cloud App Security 커넥터 연결

이 작업에서는 Microsoft Cloud App Security 커넥터를 연결합니다.

1. 데이터 커넥터 탭의 목록에서 **Microsoft Cloud App Security** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. **경고**, **변경 내용 적용**을 차례로 선택합니다.

### 작업 6: Office 365용 Microsoft Defender 커넥터 연결

이 작업에서는 Office 365용 Microsoft Defender 커넥터를 연결합니다.

1. 데이터 커넥터 탭의 목록에서 **Office 365용 Microsoft Defender** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. **연결**을 선택합니다.

### 작업 7: Microsoft Defender for Identity 커넥터 연결

이 작업에서는 Microsoft Defender for Identity 커넥터를 연결합니다.

1. 데이터 커넥터 탭의 목록에서 **Microsoft Defender for Identity** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. 연결 옵션을 검토합니다. 옵션을 검토만 하고 연결하지는 마세요. 연결 정보만 파악하면 됩니다.

### 작업 8: 엔드포인트용 Microsoft Defender 커넥터 연결

이 작업에서는 엔드포인트용 Microsoft Defender 커넥터를 연결합니다.

1. 데이터 커넥터 탭의 목록에서 **엔드포인트용 Microsoft Defender** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 커넥터 페이지 열기를 선택합니다.

3. **연결**을 선택합니다.

### 작업 9: Microsoft 365 Defender 커넥터 연결

이 작업에서는 Microsoft 365 Defender 커넥터를 연결합니다.

1. 데이터 커넥터 탭의 목록에서 **Microsoft 365 Defender** 커넥터를 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. 엔드포인트용 Microsoft Defender의 체크박스를 모두 선택합니다.

4. **변경 내용 적용**을 선택합니다.

### 작업 3: Azure 이외의 Windows 컴퓨터 연결

이 작업에서는 Azure Sentinel에 Azure 이외의 Windows 가상 머신을 연결합니다.

1. WIN2 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 브라우저를 열고 Microsoft Edge 브라우저를 검색하여 다운로드한 후 새로 설치합니다. 새 Edge 브라우저를 시작합니다.

3. 브라우저를 열고 사용자 자격 증명을 사용하여 Azure Portal https://portal.azure.com에 로그인합니다.

4. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Azure Sentinel**을 선택합니다.

5. Azure Sentinel 작업 영역을 선택합니다.

6. 데이터 커넥터 탭의 목록에서 **보안 이벤트** 커넥터를 선택합니다.

7. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

8. 스트리밍할 이벤트 선택 영역에서 **모든 이벤트**를 선택하고 **변경 내용 적용**을 선택합니다.

9. **Azure 이외의 Windows 가상 머신에 에이전트 설치**를 선택합니다.

**참고:** Windows 가상 머신과 Azure 이외의 Windows 컴퓨터에 에이전트를 설치하는 지침이 반대로 제공될 수도 있습니다. 텍스트는 반대로 표시되지만 링크를 클릭하면 적절한 위치로 이동할 수 있습니다.

10. **Azure 외 Windows 가상 머신용 에이전트 다운로드 및 설치**를 선택합니다. 

11. **Windows 에이전트 다운로드(64비트)** 링크를 선택합니다.

12. 다운로드된 .exe 파일을 실행합니다. 사용자 계정 컨트롤 메시지가 표시될 수 있습니다. 해당 메시지에서 실행을 확인합니다.

13. 시작 대화 상자에서 **다음**을 선택합니다.

14. Microsoft 소프트웨어 사용 조건 페이지에서 **동의**를 선택합니다.  대상 선택 메시지에서 **다음**을 선택합니다.

15. 에이전트 설치 옵션 메시지에서 **Azure Log Analytics(OMS)에 에이전트 연결** 옵션을 선택한 후 **다음**을 선택합니다.

16. 브라우저의 에이전트 관리 페이지에서 **작업 영역 ID**를 복사한 다음 대화 상자의 작업 영역 ID 입력란에 붙여넣습니다. 

17. 브라우저의 에이전트 관리 페이지에서 **기본 키**를 복사한 다음 대화 상자의 기본 키 ID 입력란에 붙여넣습니다. 

18. **다음**을 선택합니다.

19. Microsoft 업데이트 페이지에서 **다음**을 선택합니다.

20. 그런 다음 **설치**를 선택합니다.

### 작업 4: Sysmon 설치 및 로그 수집

이 작업에서는 Sysmon을 설치하여 Sysmon 로그를 수집합니다.

WIN2 가상 머신에 연결되어 있어야 합니다.  다음 지침에 따라 작업을 수행하면 기본 구성으로 Sysmon이 설치됩니다.  프로덕션 컴퓨터에서 Sysmon을 사용하려면 커뮤니티에서 제공되는 구성을 조사해야 합니다.

1. 브라우저에서 https://docs.microsoft.com/sysinternals/downloads/sysmon으로 이동합니다.

2. **Download Sysmon**을 선택하여 해당 페이지에서 Sysmon을 다운로드합니다.

3. 다운로드한 파일을 열어 새 디렉터리 c:\sysmon에 파일 압축을 풉니다.

4. WIN2의 Windows 작업 표시줄 검색 창에 *명령*을 입력합니다.  검색 결과에 명령 프롬프트 앱이 표시됩니다.  명령 프롬프트 앱을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.  사용자 계정 컨트롤 메시지가 표시되면 실행을 확인합니다.

5. *cd \sysmon* 을 입력합니다.

6. *notepad sysmon.xml* 을 입력하여 새 파일을 만듭니다.

7. 브라우저에서 탭을 열고 https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml로 이동합니다.

8. Github의 해당 파일 내용을 방금 만든 sysmon.xml 메모장 파일에 복사한 후 파일을 저장합니다.

9. 명령 프롬프트에 다음 명령을 입력하고 Enter 키를 누릅니다.
    sysmon.exe -accepteula -i sysmon.xml

10. 브라우저에서 Azure Portal https://portal.azure.com으로 이동합니다. 

11. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Azure Sentinel**을 선택합니다.

12. Azure Sentinel의 구성 영역에서 **설정**을 선택하고 **작업 영역 설정** 탭을 선택합니다.

13. Azure Sentinel 작업 영역이 선택되어 있는지 확인합니다.

14. 설정에서 **에이전트 구성**을 선택합니다.

15. **Windows 이벤트 로그** 탭을 선택합니다.

16. **Windows 이벤트 로그 추가** 단추를 선택합니다.

17. 로그 이름 필드에 **Microsoft-Windows-Sysmon/Operational** 을 입력합니다.

18. **적용**을 선택합니다.

## 공격 수행

### 작업 1: 엔드포인트용 Defender를 사용하여 구성된 Windows 공격

이 작업에서는 엔드포인트용 Microsoft Defender가 구성되어 있는 호스트에서 공격을 수행합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 작업 표시줄의 검색 창에 *명령*을 입력합니다.  검색 결과에 명령 프롬프트가 표시됩니다.  명령 프롬프트를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 사용자 계정 컨트롤 메시지가 표시되면 실행을 확인합니다.

3. 명령 프롬프트의 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.
```
cd \
mkdir temp
cd temp
```
4. 공격 1 - 다음 명령을 복사하여 실행합니다.

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 공격 3 - 다음 명령을 복사하여 실행합니다.

```
notepad c2.ps1
```
**예**를 선택하여 새 파일을 만든 후 아래 PowerShell 스크립트를 c2.ps1에 복사하고 **저장**을 선택합니다.

**참고** 가상 머신에 스크립트를 붙여넣을 때는 길이가 제한될 수 있습니다.  전체 스크립트를 가상 머신에 붙여넣으려면 3개 섹션으로 나눠서 붙여넣으세요.  메모장에서 연 c2.ps1 파일 내에서 스크립트가 여기에 나와 있는 지침과 동일하게 표시되는지 확인합니다.

```


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
```
powershell
.\c2.ps1
```
**참고:** 오류를 해결하라는 메시지가 표시됩니다. 정상적인 현상이므로
이 명령/PowerShell 스크립트를 백그라운드에서 실행하고 창을 닫지 마세요.  명령이 몇 시간 동안 로그 항목을 생성해야 합니다.  이 스크립트가 실행되는 동안 다음 작업과 다음 연습을 진행해도 됩니다.  이 작업에서 생성되는 데이터를 나중에 위협 헌팅 랩에서 사용합니다.  이 프로세스에서 대량의 데이터가 작성되거나 처리되지는 않습니다.

### 작업 2: Sysmon을 사용하여 구성된 Windows 공격

이 작업에서는 보안 이벤트 커넥터와 Sysmon이 구성되어 있는 호스트에서 공격을 수행합니다.

1. WIN2 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 작업 표시줄의 검색 창에 *CMD*를 입력합니다.  검색 결과에 명령 프롬프트가 표시됩니다.  명령 프롬프트를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.

3. 명령 프롬프트의 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.
```
cd \
mkdir temp
cd \temp
```

4. 공격 1 - 다음 명령을 복사하여 실행합니다.

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 공격 2 - 다음 명령을 복사하여 실행합니다. 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```