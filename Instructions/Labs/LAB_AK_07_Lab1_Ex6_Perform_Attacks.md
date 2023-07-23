---
lab:
  title: 연습 6 - 공격 수행
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 7 - 랩 1 - 연습 6 - 공격 수행

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex5.png)

나중에 Microsoft Sentinel에서 검색하고 조사하는 데 사용할 공격을 시뮬레이션하려고 합니다.


>                **참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Perform%20simulated%20attacks)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 


### 작업 1: 레지스트리 키 추가를 통한 지속성 공격

>**중요:** 다음 단계는 이전에 작업한 컴퓨터와는 다른 컴퓨터에서 수행합니다. 가상 머신 이름 참조를 찾습니다.

이 작업에서는 Azure Arc와 연결된 호스트와 Azure Monitor 에이전트가 구성된 호스트에 대한 공격을 수행합니다.

1. 암호를 사용하여 WINServer 가상 머신에 관리 로그인합니다. **Pa55w.rd**.  

    >**중요:** 랩 *SAVE* 기능을 사용하면 WINServer가 Azure Arc에서 연결이 끊어질 수 있습니다. 다시 부팅하면 문제가 해결됩니다.  

1. Windows에서 **시작**을 선택합니다. 그런 다음, **전원**과 **다시 시작**을 차례로 선택합니다.

1. 지침에 따라 WINServer에 다시 로그인합니다.

1. 작업 표시줄의 검색 창에 *명령*을 입력합니다. 검색 결과에 명령 프롬프트가 표시됩니다. 명령 프롬프트를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 표시되는 사용자 계정 컨트롤 창에서 **예**를 선택하여 앱을 실행할 수 있도록 합니다.

1. 명령 프롬프트에서 루트 디렉터리에 Temp 폴더를 만듭니다. 마지막 행 후에 Enter 키를 눌러야 합니다.

    ```CommandPrompt
    cd \
    mkdir temp
    cd temp
    ```

1. 이 명령을 복사하고 실행하여 프로그램 지속성을 시뮬레이션합니다.

    ```CommandPrompt
    REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
    ```


### 작업 2: 사용자 추가를 통한 권한 상승 공격

1. 이 명령을 복사하고 실행하여 관리자 계정 만들기를 시뮬레이션합니다. 마지막 행 후에 Enter 키를 눌러야 합니다.

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```


### 작업 3: DNS를 사용하여 명령 및 제어 공격

1. 이 명령을 복사하고 실행하여 C2 서버에 대한 DNS 쿼리를 시뮬레이션하는 스크립트를 만듭니다.

    ```CommandPrompt
    notepad c2.ps1
    ```

1. **예**를 선택하여 새 파일을 만든 후 아래 PowerShell 스크립트를 *c2.ps1*에 복사합니다.

    >**참고:** 가상 머신에 스크립트를 붙여넣을 때는 길이가 제한될 수 있습니다. *c2.ps1* 파일 내에서 스크립트가 여기에 나와 있는 지침과 동일하게 표시되는지 확인합니다.

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

1. 메모장 메뉴에서 **파일**, **저장**을 차례로 선택합니다. 

1. 명령 프롬프트 창으로 돌아가서 다음 명령을 입력하고 Enter 키를 누릅니다. 

    >**참고:** DNS resolve 오류가 표시됩니다. 예상된 동작입니다.

    ```CommandPrompt
    Start PowerShell.exe -file c2.ps1
    ```

>**중요:** 이 창을 닫지 마세요. 이 PowerShell 스크립트를 백그라운드에서 실행하겠습니다. 명령이 몇 시간 동안 로그 항목을 생성해야 합니다. 이 스크립트가 실행되는 동안 다음 작업과 다음 연습을 진행해도 됩니다. 이 작업에서 생성되는 데이터를 나중에 위협 헌팅 랩에서 사용합니다. 이 프로세스에서 대량의 데이터가 작성되거나 처리되지는 않습니다.


## 연습 7 계속 진행
