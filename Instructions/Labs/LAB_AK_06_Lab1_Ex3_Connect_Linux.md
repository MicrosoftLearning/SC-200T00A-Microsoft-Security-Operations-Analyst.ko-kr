---
lab:
    title: '연습 3 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트 연결'
    module: '모듈 6 - Microsoft Sentinel에 로그 연결'
---

# 모듈 6 - 랩 1 - 연습 3 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트 연결


### 작업 1: Microsoft Sentinel 작업 영역 액세스

이 작업에서는 Microsoft Sentinel 작업 영역에 액세스합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 새 Microsoft Edge 브라우저를 시작합니다.

3. Edge 브라우저에서 Azure Portal https://portal.azure.com 으로 이동합니다.

4. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

5. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

6. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

7. 이전 랩에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.


### 작업 2: Common Event Format 커넥터를 사용하여 Linux 호스트 연결

이 작업에서는 CEF(Common Event Format) 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트를 연결합니다.

1. Microsoft Sentinel의 구성 영역에서 **데이터 커넥터**를 선택합니다.  데이터 커넥터 탭에서 **CEF(Common Event Format)** 커넥터를 검색하고 목록에서 선택합니다.

2. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

3. *1.2 Linux 컴퓨터에 CEF 수집기 설치*에 표시된 명령을 클립보드에 복사합니다.

4. LIN1 가상 머신을 시작하고 랩 호스터가 제공한 사용자 이름과 암호를 사용하여 로그인합니다. LIN1 서버의 IP 주소를 적어 둡니다. 아래 스크린샷을 예제로 참조하세요.

   ![linux 로그인](../Media/LinuxLoginExample.png)

5. WIN1 가상 머신으로 돌아가 시작 메뉴 아이콘을 마우스 오른쪽 단추로 클릭하고 **Windows PowerShell(관리자)** 을 선택하여 관리자 권한으로 Windows PowerShell을 시작합니다. **예**를 선택하여 표시되는 사용자 계정 컨트롤 창에서 앱을 실행하도록 허용합니다.

6. 구체적인 Linux 서버 정보에 맞게 다음 PowerShell 명령을 수정하여 입력하고 Enter 키를 누릅니다.

```PowerShell
ssh <insert your linux IP address here> -l <insert linux user name here>
```

7. *yes*를 입력하여 연결을 확인한 후 사용자의 암호를 입력하고 Enter 키를 누릅니다. 화면이 이제 다음과 같이 표시됩니다.

   ![linux 로그인](../Media/PSconnectLinux.png)

8. 이제 이전 단계의 *1.2 Linux 컴퓨터에 CEF 수집기 설치*를 붙여넣을 준비가 되었습니다. Azure의 스크립트가 클립보드에 있는지 확인합니다. PowerShell에서 상단 표시줄을 마우스 오른쪽 단추로 클릭하고 **편집**, **붙여넣기**를 차례로 선택합니다. 붙여넣은 후에는 아래와 같이 **3**을 *python*에 추가합니다.

   ![ConnectorScript](../Media/ConnectorScript.png)


9. 스크립트를 붙여넣고 조정한 후에 Enter 키를 누릅니다. 스크립트가 Linux 서버에 대해 원격으로 실행됩니다. 스크립트가 올바르게 처리되면 이 화면과 비슷하게 됩니다.

   ![ConnectorScript](../Media/LinuxConnected.png)


### 작업 3: Syslog 커넥터를 사용하여 Linux 호스트 연결

이 작업에서는 Syslog 커넥터를 사용하여 Microsoft Sentinel에 Linux 호스트를 연결합니다.

1. WIN1(작업 영역에 대한 Microsoft Sentinel 포털에 이미 있어야 함)에 연결합니다.  

2. 데이터 커넥터 탭에서 **Syslog** 커넥터를 검색하고 목록에서 선택합니다.

3. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

4. **Azure 이외의 Linux 컴퓨터에 에이전트 설치** 섹션을 엽니다.

5. **Azure 외 Linux 컴퓨터용 에이전트 다운로드 및 설치** 링크를 선택합니다. 

6. **Linux 서버** 탭을 선택합니다.

7. *Linux용 에이전트 다운로드 및 설치* 영역의 명령을 클립보드에 복사합니다.

8. LIN2 가상 머신을 시작하고 랩 호스터가 제공한 사용자 이름과 암호를 사용하여 로그인합니다. LIN2 서버의 IP 주소를 적어 둡니다. 아래 스크린샷을 예제로 참조하세요.

   ![linux 로그인](../Media/LinuxLoginExample.png)

9. WIN1 가상 머신으로 돌아가 시작 메뉴 아이콘을 마우스 오른쪽 단추로 클릭하고 **Windows PowerShell(관리자)** 을 선택하여 관리자 권한으로 새 Windows PowerShell을 시작합니다. **예**를 선택하여 표시되는 사용자 계정 컨트롤 창에서 앱을 실행하도록 허용합니다.

   >**참고:** 마지막 작업에 대해 *설치가 완료*된 경우 *exit*를 입력하여 LIN1에 대한 연결을 닫고 Windows PowerShell을 재사용할 수 있습니다.

10. 구체적인 Linux 서버 정보에 맞게 다음 PowerShell 명령을 수정하여 입력하고 Enter 키를 누릅니다.

```PowerShell
ssh <insert your linux IP address here> -l <insert linux user name here>
```

11. *yes*를 입력하여 연결을 확인한 후 사용자의 암호를 입력하고 Enter 키를 누릅니다. 화면이 이제 다음과 같이 표시됩니다.

   ![linux 로그인](../Media/PSconnectLinux.png)

12. 이제 이전 단계의 *Linux용 에이전트 다운로드 및 설치*를 붙여넣을 준비가 되었습니다. Azure의 스크립트가 클립보드에 있는지 확인합니다. PowerShell에서 상단 표시줄을 마우스 오른쪽 단추로 클릭하고 **편집**, **붙여넣기**를 차례로 선택합니다.

13. 스크립트를 붙여넣은 후에 Enter 키를 누릅니다. 스크립트가 Linux 서버에 대해 원격으로 실행됩니다. 이 작업을 완료했습니다. 이 과정에는 이 연결을 사용하는 추가 랩이 없습니다.


### 작업 4: Syslog 커넥터용으로 수집할 기능 및 해당 심각도 구성

이 작업에서는 Syslog 수집 기능을 구성합니다.

1. WIN1 가상 머신에 연결합니다.

2. Microsoft Sentinel 포털에서 **설정**을 선택하고 설정 블레이드에서 **작업 영역 설정**을 선택합니다.

3. **설정** 영역에서 **에이전트 구성**을 선택합니다.

4. **Syslog** 탭을 선택합니다.

5. **+ 기능 추가** 단추를 선택합니다.

6. *기능 이름* 드롭다운 메뉴에서 **인증**을 선택합니다.

7. **+ 기능 추가** 단추를 다시 선택합니다.

8. *기능 이름* 드롭다운 메뉴에서 **authpriv**를 선택합니다.

9. **적용**을 선택합니다.  이 작업을 완료했습니다.

## 연습 4 계속 진행
