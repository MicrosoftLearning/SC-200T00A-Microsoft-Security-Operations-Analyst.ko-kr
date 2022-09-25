---
lab:
  title: 연습 1 - Microsoft 365 Defender 살펴보기
  module: Module 1 - Mitigate threats using Microsoft 365 Defender
---

# <a name="module-1---lab-1---exercise-1---explore-microsoft-365-defender"></a>모듈 1 - 랩 1 - 연습 1 - Microsoft 365 Defender 살펴보기 

## <a name="lab-scenario"></a>랩 시나리오

![M365 Defender](../Media/SC-200-Lab_M1_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft 365 Defender. You start by assigning preset security policies in EOP and Microsoft Defender for Office 365.


### <a name="task-1-obtain-your-microsoft-365-credentials"></a>작업 1: Microsoft 365 자격 증명 받기

Once you launch the lab, a free trial tenant will be made available to you to access in the Microsoft virtual Lab environment. This tenant will be automatically assigned a unique username and password. You must retrieve this username and password so that you can sign into Azure and Microsoft 365 within the Microsoft Virtual Lab environment. 

Because this course can be offered by learning partners using any one of several Authorized Lab Hosting (ALH) providers, the actual steps involved to retrieve the tenant ID associated with your tenant may vary by lab hosting provider. Therefore, your instructor will provide you with the necessary instructions for how to retrieve this information for your course. The information that you should note for later use includes:

- <bpt id="p1">**</bpt>Tenant suffix ID.<ept id="p1">**</ept> This ID is for the onmicrosoft.com accounts that you will use to sign into Microsoft 365 throughout the labs. This is in the format of <bpt id="p1">**</bpt>{username}<ph id="ph1">@ZZZZZZ.onmicrosoft.com</ph><ept id="p1">**</ept>, where ZZZZZZ is your unique tenant suffix ID provided by your lab hosting provider. Record this ZZZZZZ value for later use. When any of the lab steps direct you to sign into Microsoft 365 portals, you must enter the ZZZZZZ value that you obtained here.
- <bpt id="p1">**</bpt>Tenant password.<ept id="p1">**</ept> This is the password for the admin account provided by your lab hosting provider.


### <a name="task-2-apply-microsoft-defender-for-office-365-preset-security-policies"></a>작업 2: Office 365용 Microsoft Defender 미리 설정된 보안 정책 적용

이 작업에서는 Microsoft 365 보안 포털에서 EOP(Exchange Online Protection) 및 Office 365용 Microsoft Defender에 대한 미리 설정된 보안 정책을 할당합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 새 Microsoft Edge 브라우저를 시작합니다.

1. Edge 브라우저에서 Microsoft 365 Defender 포털(https://security.microsoft.com) )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

    >여러분은 Microsoft 365 Defender를 구현하고 있는 회사에서 일하는 보안 운영 분석자입니다.  

1. 표시된 경우 Microsoft 365 Defender 둘러보기를 닫습니다.

1. 탐색 메뉴의 메일 및 협업 영역에서 **정책 및 규칙**을 선택합니다.

1. 정책 및 규칙 대시보드에서 **위협 정책**을 선택합니다.

1. 위협 정책 대시보드에서 **미리 설정된 보안 정책**을 선택합니다.

    >먼저 EOP 및 Office 365용 Microsoft Defender에서 미리 설정된 보안 정책을 할당합니다.

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you receive the message <bpt id="p2">*</bpt>"Client Error - An error occurred when retrieving preset security policies. Please try again later."<ept id="p2">*</ept> select <bpt id="p1">**</bpt>OK<ept id="p1">**</ept> to continue. Refresh your browser using <bpt id="p1">**</bpt>Ctrl+F5<ept id="p1">**</ept>.

1. Under <bpt id="p1">*</bpt>Standard protection<ept id="p1">*</ept>, select <bpt id="p2">**</bpt>Manage protection settings<ept id="p2">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you see this option grayed out, refresh your browser using <bpt id="p2">**</bpt>Ctrl+F5<ept id="p2">**</ept>.

1. 랩을 시작하면 Microsoft Virtual Lab 환경에 액세스할 수 있는 무료 평가판 테넌트가 제공될 것입니다. 

1. 이 테넌트에는 고유한 사용자 이름과 암호가 자동으로 할당됩니다.

1. 가장 보호 섹션에서 **다음**을 4번 선택하여 계속합니다.

1. 정책 모드 섹션에서 **완료한 후 정책 켜기** 라디오 단추가 선택되었는지 확인한 다음, **다음**을 선택합니다.

1. 변경 내용 검토 및 확인 아래에서 콘텐츠를 읽고, **확인**을 선택하여 변경 내용을 적용하고, **완료**를 선택하여 완료합니다.

    >Microsoft 가상 랩 환경 내에서 Azure와 Microsoft 365에 로그인할 수 있도록 이 사용자 이름과 암호를 검색해야 합니다.

1. Under <bpt id="p1">*</bpt>Strict protection<ept id="p1">*</ept>, select <bpt id="p2">**</bpt>Manage protection settings<ept id="p2">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> <bpt id="p2">*</bpt>Strict protection<ept id="p2">*</ept> is found under "Email &amp; Collaboration - Policies &amp; rules - Threat policies - Preset security policies".

1. 이 과정은 학습 파트너가 여러 ALH(Authorized Lab Hosting) 공급자 중 하나를 사용하여 제공할 수 있기 때문에 귀하의 테넌트와 관련된 테넌트 ID 검색에 수반되는 실제 단계는 랩 호스팅 공급자에 따라 다를 수 있습니다.

1. 따라서 강사가 귀하의 과정에서 이 정보를 검색하는 방법에 대한 필수 지침을 제공할 것입니다.

1. 가장 보호 섹션에서 **다음**을 4번 선택하여 계속합니다.

1. 정책 모드 섹션에서 **완료한 후 정책 켜기** 라디오 단추가 선택되었는지 확인한 다음, **다음**을 선택합니다.

1. 변경 내용 검토 및 확인 아래에서 콘텐츠를 읽고, **확인**을 선택하여 변경 내용을 적용하고, **완료**를 선택하여 완료합니다.

    >나중에 사용할 수 있도록 기록해 두어야 하는 정보는 다음과 같습니다.

1. **Microsoft 365 Defender** 포털에 있는 탐색 메뉴의 왼쪽에서 **설정**을 선택합니다.

1. On the <bpt id="p1">**</bpt>Settings<ept id="p1">**</ept> page select <bpt id="p2">**</bpt>Microsoft 365 Defender<ept id="p2">**</ept>. You are going to see an image of a coffee mug and a message that reads: "Hang on! We're preparing new spaces for your data and connecting them". It will take several minutes to finish, so leave the page open until the next lab. 

    >**테넌트 접미사 ID.**

1. 새 공간이 성공적으로 완료되면 계정, 메일 알림, 미리 보기 기능 및 스트리밍 API에 대한 Microsoft 365 Defender 설정이 표시됩니다.

## <a name="you-have-completed-the-lab"></a>이 랩을 완료했습니다.
