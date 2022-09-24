---
lab:
  title: 연습 6 - 공격 수행
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-6---conduct-attacks"></a>모듈 7 - 랩 1 - 연습 6 - 공격 수행

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex5.png)

나중에 Microsoft Sentinel에서 검색하고 조사하는 데 사용할 공격을 시뮬레이션하려고 합니다.


### <a name="task-1-attack-windows-configured-with-defender-for-endpoint"></a>작업 1: 엔드포인트용 Defender를 사용하여 구성된 Windows 공격

이 작업에서는 엔드포인트용 Microsoft Defender가 구성되어 있는 호스트에서 공격을 수행합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. In the search of the task bar, enter <bpt id="p1">*</bpt>Command<ept id="p1">*</ept>. Command Prompt will be displayed in the search results. Right-click on the Command Prompt and select <bpt id="p1">**</bpt>Run as Administrator<ept id="p1">**</ept>. Select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> in the User Account Control window that appears to allow the app to run.

1. In the Command Prompt, create a Temp folder in the root directory. Remember to press Enter after the last row:

    ```CommandPrompt
    cd \
    mkdir temp
    cd temp
    ```

#### <a name="attack-1---persistence-with-registry-key-add"></a>공격 1 - 레지스트리 키 추가를 통한 지속성

1. 이 명령을 복사하고 실행하여 프로그램 지속성을 시뮬레이션합니다.

    ```CommandPrompt
    REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
    ```

#### <a name="attack-3---dns--c2"></a>공격 3 - DNS/C2 

1. 이 명령을 복사하고 실행하여 C2 서버에 대한 DNS 쿼리를 시뮬레이션하는 스크립트를 만듭니다.

    ```CommandPrompt
    notepad c2.ps1
    ```

1. **예**를 선택하여 새 파일을 만든 후 아래 PowerShell 스크립트를 *c2.ps1*에 복사합니다.

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> Paste into the virtual machine might have a limited length. Make sure the script looks as it does in these instructions within the <bpt id="p1">*</bpt>c2.ps1<ept id="p1">*</ept> file.

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

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> A new PowerShell window will open and you will see resolve errors. This is expected.

    ```CommandPrompt
    Start PowerShell.exe -file c2.ps1
    ```

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> Do not close these windows. Let this PowerShell script run in the background. The command needs to generate log entries for some hours. You can proceed to the next task and next exercises while this script runs. The data created by this task will be used in the Threat Hunting lab later. This process will not create substantial amounts of data or processing.


### <a name="task-2-attack-windows-configured-with-microsoft-sentinel-connector"></a>작업 2: Microsoft Sentinel 커넥터로 구성된 Windows 공격

이 작업에서는 Microsoft Sentinel의 보안 이벤트 커넥터가 있는 호스트에서 공격을 수행합니다.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. WIN2 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

>**중요:** 랩 저장 기능으로 인해 Azure Arc에서 Win2가 분리될 수 있습니다.  재부팅하면 문제가 해결됩니다.  

1. Select <bpt id="p1">**</bpt>Start<ept id="p1">**</ept> in Windows. Then <bpt id="p1">**</bpt>Power<ept id="p1">**</ept>, next <bpt id="p2">**</bpt>Restart<ept id="p2">**</ept>
1. 지침에 따라 WIN2에 다시 로그인합니다.


1. In the search of the task bar, enter <bpt id="p1">*</bpt>Command<ept id="p1">*</ept>. Command Prompt will be displayed in the search results. Right-click on the Command Prompt and select <bpt id="p1">**</bpt>Run as Administrator<ept id="p1">**</ept>. Select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> in the User Account Control window that appears to allow the app to run. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might have a Command Prompt as Administrator open from a previous exercise.

1. In the Command Prompt, create a Temp folder in the root directory. Remember to press Enter after the last row:

    ```CommandPrompt
    cd \
    mkdir temp
    cd \temp
    ```

#### <a name="attack-2---user-add-and-elevate-privilege"></a>공격 2 - 사용자 추가 및 권한 상승

1. 작업 표시줄의 검색 창에 *명령*을 입력합니다.

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

## <a name="proceed-to-exercise-7"></a>연습 7 계속 진행
