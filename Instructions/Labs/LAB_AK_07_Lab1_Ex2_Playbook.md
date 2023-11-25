---
lab:
  title: 연습 2 - 플레이북 만들기
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 7 - 랩 1 - 연습 2 - 플레이북 만들기

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex2.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel을 사용하여 위협을 검색하고 완화하는 방법을 파악해야 합니다. 이제 Microsoft Sentinel에서 루틴으로 실행할 수 있는 작업에 응답하고 이를 수정하려고 합니다.

플레이북을 사용하면 위협 대응을 자동화 및 오케스트레이션하고, 내부 및 외부의 다른 시스템과 통합할 수 있으며, 분석 규칙 또는 자동화 규칙에 의해 트리거될 때 특정 경고 또는 인시던트에 대응하여 자동으로 실행되도록 설정할 수 있습니다. 

>**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20a%20playbook)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다.

### 작업 1: Microsoft Teams에서 보안 운영 센터 팀 만들기

이 작업에서는 랩에서 사용할 Microsoft Teams 팀을 만듭니다.

1. 암호를 사용하여 관리 WIN1 가상 머신에 로그인합니다 **. Pa55w.rd**.  

1. Microsoft Edge 브라우저에서 새 탭을 열고 (https://teams.microsoft.com)에서) Microsoft Teams 포털로 이동합니다.

1. **로그인 대화 상자에서** 랩 호스팅 공급자가 **제공한 테넌트 전자 메일** 계정을 복사하여 붙여넣은 다음을 선택합니다****.

1. **암호** 입력 대화 상자에서 랩 호스팅 공급자가 **제공한 테넌트 암호를** 복사하여 붙여넣은 다음, 로그인을** 선택합니다**.

1. 나타날 수 있는 Teams 팝업을 닫습니다.

1. 아직 선택하지 않은 경우 왼쪽 메뉴에서 Teams**를 선택한 **다음 맨 위에서 더하기 기호 아이콘 아이콘](../Media/plus-sign-icon-lab.png)을 ![선택합니다.

1. **팀** 만들기 옵션을 선택합니다.

1. 처음부터 시작 **** 단추를 선택합니다.

1. **프라이빗** 단추를 선택합니다.

1. 팀 이름을 지정합니다. **SOC**를 입력하고 **만들기** 단추를 선택합니다.

1. SOC에 멤버 추가 화면에서 건너뛰**기 **단추를 선택합니다. 

1. Teams 블레이드를 아래로 스크롤하여 새로 만든 SOC 팀을 찾고, 이름 오른쪽에서 줄임표 **(...)** 를 선택하고, **채널 추가**를 선택합니다.

1. 새 경고의 *채널 이름을 입력한* 다음 추가** 단추를 선택합니다**.


### 작업 2: Microsoft Sentinel에서 플레이북 만들기

이 작업에서는 Microsoft Sentinel에서 플레이북으로 사용되는 논리 앱을 만듭니다.

1. Microsoft Edge 브라우저에서 GitHub[의 ](https://github.com/Azure/Azure-Sentinel)Microsoft Sentinel로 이동합니다.

<!--- the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace you created earlier.

1. Select the **Community** page under the *Content management* area on the left side of the page.

1. On the right pane, select the **Onboard community content** link. This opens a new tab in the Microsoft Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel). --->

1. 아래로 스크롤하여 솔루션 폴더를 **** 선택합니다.

1. 이제 **SentinelSOARessentials** 폴더를 선택하고, **Playbooks** 폴더를 선택합니다.

1. **메시지 후 Teams** 폴더를 선택합니다.

1. readme.md 상자에서 빠른 배포 섹션으로 스크롤하여 *인시던트 트리거를 사용하여 배포(권장)**하고 Azure**에 배포 단추를 선택합니다**. ***   

1. Azure 구독이 선택되어 있는지 확인합니다.

1. 리소스 그룹에서 **새로 만들기**를 선택하고, *RG-Playbooks*를 입력한 후, **확인**을 선택합니다.

1. (미국) 미국** 동부를 지역의* 기본값*으로 둡**니다.

1. *플레이북 이름을* "PostMessageTeams-OnIncident"로 바꾸고 검토 + 만들기**를 선택합니다**.

1. 이제 **만들기**를 선택합니다. 

    >**참고:** 다음 작업으로 진행하기 전에 배포가 완료되기를 기다립니다.

### 작업 3: Microsoft Sentinel에서 플레이북 업데이트

이 작업에서는 적절한 연결 정보로 만든 새 플레이북을 업데이트합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. **구성* 영역에서 자동화**를 *선택한 다음, 활성 플레이북 탭을** 선택합니다**.

1. 플레이북이 표시되지 않는 경우 명령 모음에서 새로 고침**을 선택합니다**. Microsoft Sentinel 인시 *** 던트 트리거 종류를* 사용하여 이전 단계에서 만든 플레이북이 **표시됩니다.

1. **PostMessageTeams-OnIncident** 플레이북 이름을 선택합니다.

1. PostMessageTeams-OnIncident에 대한 *논리 앱 페이지의 명령 메뉴에서 편집**을 선택합니다**.*

    >**참고:** 페이지를 새로 고쳐야 할 수 있습니다.

1. 첫 번째* 블록인 ***Microsoft Sentinel 인시던트(미리 보기)** 를 선택합니다.

1. **연결 변경** 링크를 선택합니다.

1. **새로 추가**를 선택하고 **로그인**을 선택합니다. 새 창에서 메시지가 표시되면 Azure 구독 관리자 자격 증명을 선택합니다. 이제 블록의 마지막 줄에 “관리자-사용자-이름에 연결됨”이 표시되어야 합니다.

1. 이제 두 번째 블록 커넥트 **선택합니다***.*

1. **새로 추가**를 선택하고 메시지가 표시되면 Azure 관리자 자격 증명을 선택합니다. 이제 블록의 마지막 줄에 “관리자-사용자-이름에 연결됨”이 표시되어야 합니다.

1. 이제 블록 이름이 메시지 게시(V3)(미리 보기)로 바뀌었**습니다. 팀* 필드의 *끝에서 X**를 선택하여 **내용을 지웁**니다. Microsoft Teams의 사용 가능한 Teams 목록이 포함된 드롭다운으로 필드가 변경됩니다. **SOC**를 선택합니다.

1. 채널 필드에 대해 *동일한 작업을 수행합니다. 필드 끝에 있는 X**를 선택하여 **내용을 지웁*니다. SOC Teams 채널 목록이 포함된 드롭다운으로 필드가 변경됩니다. 새 경고를** 선택합니다**.

1. 명령 모음에서 **저장**을 선택합니다. 논리 앱은 향후 랩에서 사용됩니다.

## 연습 3 계속 진행
