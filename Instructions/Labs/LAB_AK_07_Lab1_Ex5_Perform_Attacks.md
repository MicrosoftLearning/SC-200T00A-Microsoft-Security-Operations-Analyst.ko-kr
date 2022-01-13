---
lab:
    title: '연습 5 - 공격 수행'
    module: '모듈 7 - Microsoft Sentinel을 사용하여 검색 만들기 및 조사 수행'
---

# 모듈 7 - 랩 1 - 연습 5 - 공격 수행


### 작업 1: 엔드포인트용 Defender를 사용하여 구성된 Windows 공격

이 작업에서는 엔드포인트용 Microsoft Defender가 구성되어 있는 호스트에서 공격을 수행합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 작업 표시줄의 검색 창에 *명령*을 입력합니다.  검색 결과에 명령 프롬프트가 표시됩니다.  명령 프롬프트를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 사용자 계정 컨트롤 창이 표시되면 **예**를 선택하여 앱을 실행하도록 허용합니다.

3. 명령 프롬프트의 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.

```Command
cd \
mkdir temp
cd temp
```
4. 공격 1 - 다음 명령을 명령 프롬프트 앱에 복사하여 실행합니다.

```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 공격 3 - 다음 명령을 복사하여 실행합니다.

```Command
notepad c2.ps1
```
**예**를 선택하여 새 파일을 만든 후 아래 PowerShell 스크립트를 *c2.ps1*에 복사합니다.

>**참고:** 가상 머신에 붙여 넣을 때는 길이 제한이 있을 수 있습니다. 명령을 바로 붙여 넣을 수 없는 경우 이 코드를 3개 섹션으로 나눠서 모든 스크립트를 가상 머신에 붙여 넣으세요.  메모장에서 연 *c2.ps1* 파일 내에서 스크립트가 여기에 나와 있는 명령과 동일하게 표시되는지 확인합니다.

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

메모장 메뉴에서 **파일**을 선택한 후 **저장**을 선택합니다. 명령 프롬프트 창에서 한 행에 명령을 하나 입력하고 Enter 키를 눌러 한 행에 하나씩 다음 명령을 입력합니다. **참고:** 오류를 해결하라는 메시지가 표시됩니다. 정상적인 현상이므로 무시하세요.

```Command
powershell
.\c2.ps1
```

>**중요:** 창을 닫지 마세요. 이 명령/PowerShell 스크립트를 백그라운드에서 실행하고 명령이 몇 시간 동안 로그 항목을 생성해야 합니다. 이 스크립트가 실행되는 동안 다음 작업과 다음 연습을 진행해도 됩니다. 이 작업에서 생성되는 데이터를 나중에 위협 헌팅 랩에서 사용합니다. 이 프로세스에서 대량의 데이터가 작성되거나 처리되지는 않습니다.


### 작업 2: Sysmon을 사용하여 구성된 Windows 공격

이 작업에서는 보안 이벤트 커넥터와 Sysmon이 구성되어 있는 호스트에서 공격을 수행합니다.

1. WIN2 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 작업 표시줄의 검색 창에 *CMD*를 입력합니다.  검색 결과에 명령 프롬프트가 표시됩니다.  명령 프롬프트를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.  사용자 계정 컨트롤 메시지가 표시되면 수락합니다.

3. 명령 프롬프트의 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.

```Command
cd \
mkdir temp
cd \temp
```

4. 공격 1 - 다음 명령을 명령 프롬프트 앱에 복사하여 실행합니다.

```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

>**참고:** WIN1에서와 동일한 *지속성* 전술을 사용하지만 다음 연습에서는 다른 검색을 사용할 것입니다.

5. 공격 2 - 다음 명령을 복사하여 실행합니다. 각 행에 다음 명령을 입력하고 각 행의 끝에서 Enter 키를 누릅니다.

```Command
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

## 연습 6 계속 진행
