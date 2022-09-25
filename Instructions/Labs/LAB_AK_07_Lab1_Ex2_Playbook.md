---
lab:
  title: 연습 2 - 플레이북 만들기
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-2---create-a-playbook"></a>모듈 7 - 랩 1 - 연습 2 - 플레이북 만들기

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex2.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. Now, you want to respond and reMediate actions that can be run from Microsoft Sentinel as a routine.

플레이북을 사용하면 위협 대응을 자동화 및 오케스트레이션하고, 내부 및 외부의 다른 시스템과 통합할 수 있으며, 분석 규칙 또는 자동화 규칙에 의해 트리거될 때 특정 경고 또는 인시던트에 대응하여 자동으로 실행되도록 설정할 수 있습니다. 


### <a name="task-1-create-a-security-operations-center-team-in-microsoft-teams"></a>작업 1: Microsoft Teams에서 보안 운영 센터 팀 만들기

이 작업에서는 랩에 사용할 Microsoft Teams 팀을 만듭니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 새 탭을 열고 Microsoft Teams 포털(https://teams.microsoft.com) )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Teams 팝업이 표시되면 닫습니다.

1. 아직 선택하지 않은 경우 왼쪽 메뉴에서 **Teams**를 선택한 다음, 아래쪽에서 **참가 또는 팀 만들기**를 선택합니다.

1. 기본 창에서 **팀 만들기** 단추를 선택합니다.

1. **처음부터** 단추를 선택합니다.

1. **프라이빗** 단추를 선택합니다.

1. 팀 이름을 지정합니다. **SOC**를 입력하고 **만들기** 단추를 선택합니다.

1. SOC 화면에 구성원을 추가하고 **건너뛰기** 단추를 선택합니다. 

1. Teams 블레이드를 아래로 스크롤하여 새로 만든 SOC 팀을 찾고, 이름 오른쪽에서 줄임표 **(...)** 를 선택하고, **채널 추가**를 선택합니다.

1. 채널 이름을 *New Alerts*로 입력하고 **추가** 단추를 선택합니다.


### <a name="task-2-create-a-playbook-in-microsoft-sentinel"></a>작업 2: Microsoft Sentinel 플레이북 만들기

이 작업에서는 Microsoft Sentinel에서 플레이북으로 사용할 논리 앱을 만듭니다.

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 페이지 왼쪽의 콘텐츠 관리 영역에서 **커뮤니티** 페이지를 선택합니다.

1. On the right pane, select the <bpt id="p1">**</bpt>Onboard community content<ept id="p1">**</ept> link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content.

1. **Solutions** 폴더를 선택합니다.

1. **Teams** 폴더를 선택하고 **Playbooks** 폴더를 선택합니다.

1. **Post-Message-Teams** 폴더를 선택합니다.

1. readme.md 상자에서 두 번째 빠른 배포 옵션, **경고 트리거를 사용하여 배포**로 아래로 스크롤하고 **Azure에 배포** 단추를 선택합니다.  

    ><bpt id="p1">**</bpt>VERY IMPORTANT<ept id="p1">**</ept>: Be aware that they are two different Microsoft Sentinel triggers to use, Incident and Alert. Make sure you are selecting the Alert (second) one.

1. Azure 구독이 선택되어 있는지 확인합니다.

1. 리소스 그룹에서 **새로 만들기**를 선택하고, *RG-Playbooks*를 입력한 후, **확인**을 선택합니다.

1. 지역 기본값으로 **미국 동부**를 그대로 둡니다.

1. Make sure the <bpt id="p1">*</bpt>Playbook Name<ept id="p1">*</ept> is "PostMessageTeams-OnAlert" and select <bpt id="p2">**</bpt>Review + create<ept id="p2">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If the name is different, go back to GitHub and select the <bpt id="p2">**</bpt>Deploy with alert trigger<ept id="p2">**</ept> playbook.

1. 이제 **만들기**를 선택합니다. 

    >**참고:** 다음 작업으로 진행하기 전에 배포가 완료될 때까지 기다립니다.


### <a name="task-3-update-a-playbook-in-microsoft-sentinel"></a>작업 3: Microsoft Sentinel에서 플레이북 업데이트

이 작업에서는 만든 새 플레이북을 적절한 연결 정보로 업데이트합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. 구성 영역에서 **자동화**를 선택하고 **활성 플레이북** 탭을 선택합니다.

1. Select the <bpt id="p1">**</bpt>PostMessageTeams-OnAlert<ept id="p1">**</ept> playbook. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you do not see the playbook, refresh the Azure portal page by pressing Ctrl+F5.

1. 명령 메뉴의 *PostMessageTeams-OnAlert*의 논리 앱 페이지에서 **편집**을 선택합니다.

1. 첫 번째 블록 **Microsoft Sentinel 경고**를 선택합니다.

1. **연결 변경** 링크를 선택합니다.

1. 당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다.

1. 이제 두 번째 블록인 **경고 - 인시던트 가져오기**를 선택합니다.

1. **연결 변경** 링크를 선택합니다.

1. Microsoft Sentinel을 사용하여 위협을 검색하고 완화하는 방법을 파악해야 합니다.

1. 이제 세 번째 블록인 **연결**을 선택합니다.

1. 이제 Microsoft Sentinel에서 루틴으로 실행할 수 있는 작업에 응답하고 이를 수정하려고 합니다.

1. The block has now been renamed to <bpt id="p1">**</bpt>Post a message (V3)<ept id="p1">**</ept>, at the end of the <bpt id="p2">*</bpt>Team<ept id="p2">*</ept> field, select the <bpt id="p3">**</bpt>X<ept id="p3">**</ept> to clear the contents. The field will be changed to a drop-down with a listing of the available Teams from Microsoft Teams. Select <bpt id="p1">**</bpt>SOC<ept id="p1">**</ept>.

1. Do the same for the <bpt id="p1">*</bpt>Channel<ept id="p1">*</ept> field, select the <bpt id="p2">**</bpt>X<ept id="p2">**</ept> at the end of the field to clear the contents. The field will be changed to a drop-down with a listing of the Channels of the SOC Teams. Select <bpt id="p1">**</bpt>New Alerts<ept id="p1">**</ept>.

1. 명령 모음에서 **저장**을 선택합니다.

이후의 랩에서 이 논리 앱을 사용할 예정입니다.

## <a name="proceed-to-exercise-3"></a>연습 3 계속 진행
