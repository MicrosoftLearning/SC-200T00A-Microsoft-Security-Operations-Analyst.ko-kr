---
lab:
  title: 연습 2 - 플레이북 만들기
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 9 - 랩 1 - 연습 2 - Microsoft Sentinel에서 플레이북 만들기

## 랩 시나리오

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel을 사용하여 위협을 검색하고 완화하는 방법을 파악해야 합니다. 이제 Microsoft Sentinel에서 루틴으로 실행할 수 있는 작업에 응답하고 이를 수정하려고 합니다.

플레이북을 사용하면 위협 대응을 자동화 및 오케스트레이션하고, 다른 내외부 시스템과 통합할 수 있으며, 분석 규칙 또는 자동화 규칙에 의해 트리거될 때 특정 경고 또는 인시던트에 대응하여 자동으로 실행되도록 설정할 수 있습니다.

>**중요:** 학습 경로 #9에 대한 랩 연습은 *독립 실행형* 환경에 있습니다. 완료하기 전에 랩을 종료하면 구성을 다시 실행해야 합니다.

### 작업 1: Microsoft Sentinel에서 플레이북 만들기

이 작업에서는 Microsoft Sentinel에서 플레이북으로 사용되는 논리 앱을 만듭니다.

>**참고:** Microsoft Sentinel이 Azure 구독에 **defenderWorkspace**라는 이름으로 사전 배포되었으며 필요한 *콘텐츠 허브* 솔루션이 설치되어 있습니다.

1. 비밀번호(**Pa55w.rd**)를 사용하여 WIN1 가상 머신에 관리자로 로그인합니다.  

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel **defenderWorkspace**을 선택합니다.

1. *Microsoft Sentinel*에서 **콘텐츠 허브**로 이동합니다.

1. 검색 창에서 **Sentinel SOAR Essential**을 검색합니다.

1. 결과에 표시되는 솔루션을 선택합니다.

1. 솔루션 세부 정보에서 **관리**를 선택합니다.

1. **Defender_XDR_Ransomware_Playbook_for_SecOps-Tasks** 플레이북을 찾아 이름을 선택합니다.

1. **인시던트 작업 - SecOps용 Microsoft Defender XDR 랜섬웨어 플레이북** 템플릿을 선택합니다.

1. 세부 정보 창에서 **플레이북 만들기**를 선택합니다.

1. 리소스 그룹에서 **새로 만들기**를 선택하고 **RG-Playbooks**를 입력한 다음 확인을 선택합니다.

1. 플레이북 이름에서 **for**와 추가 *밑줄*를 제거합니다(64자 제한을 초과하게 됩니다). **Defender_XDR_Ransomware_Playbook_SecOps_Tasks**으로 표시되어야 합니다.

1. **연결**을 선택합니다.

1. **다음: 검토 및 만들기**를 선택합니다.

1. 이제 **플레이북 만들기**를 선택합니다.

    >**참고:** 다음 작업으로 진행하기 전에 배포가 완료될 때까지 기다립니다.

### 작업 2: Microsoft Sentinel에서 플레이북 업데이트

이 작업에서는 적절한 연결 정보로 만든 새 플레이북을 업데이트합니다.

1. 이전 작업이 완료되면 *Defender_XDR_Ransomware_Playbook_SecOps-Tasks | Logic app designer* 페이지에 있어야 합니다. 그렇지 않은 경우 아래 1~5단계를 완료합니다.

1. Azure Portal의 검색 창에 Sentinel을 입력하고 Microsoft Sentinel을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. 구성 영역에서 자동화를 선택한 다음 *활성 플레이북* 탭을 선택합니다.

1. 플레이북이 표시되지 않는 경우 명령 모음에서 새로 고침을 선택합니다. 이전 단계에서 만들어진 플레이북이 표시됩니다.

1. **Defender_XDR_Ransomware_Playbook_SecOps_Tasks** 플레이북 이름 링크를 선택합니다.

1. **Defender_XDR_Ransomware_Playbook_SecOps_Tasks** 논리 앱 디자이너 페이지의 명령 메뉴에서 편집을 선택합니다.

    >**참고:** 브라우저를 새로 고쳐야 할 수도 있습니다.

1. 첫 번째 블록인 Microsoft Sentinel 인시던트를 선택합니다.

1. **연결 변경*** 링크를 선택합니다.

1. **새로 추가**를 선택하고 **로그인**을 선택합니다. 새 창에서 메시지가 표시되면 Azure 구독 관리자 자격 증명을 선택합니다. 이제 블록의 마지막 줄에 "관리자-사용자 이름에 연결됨"이라고 표시되어야 합니다.

<!--- 1. Below within the logic split (+ sign), select Add an action to incident.--->

1. 명령 모음에서 **저장**을 선택합니다.

1. 창에서 **X**를 선택하여 창을 닫습니다. 이후의 랩에서 이 논리 앱을 사용할 예정입니다.

### 작업 3: 자동화 규칙 만들기

1. Microsoft Sentinel 탐색 메뉴에서 *구성*을 확장하고 *자동화*를 선택합니다.

1. **+ 만들기**를 선택하고 **자동화 규칙**을 선택합니다.

1. 규칙 이름 지정

1. *트리거*를 **인시던트가 생성될 때**로 둡니다.

1. *조건*에서 인시던트 제공자를 *모두*로 둡니다.

1. *분석 규칙 이름*을 *모두*로 둡니다.

1. **연결 추가**를 선택하고 *조건 (및)* 을 선택합니다.

1. 드롭다운에서 **전술**을 선택합니다.

1. 드롭다운 목록에서 **Contains** 연산자를 선택합니다.

1. 다음 전술 *값*을 선택합니다.
    - 정찰
    - 실행
    - 지속성
    - 명령 및 제어
    - 반출
    - 사전 공격

1. 작업에서 **플레이북 실행**을 선택합니다.

1. **플레이북 권한 관리** 링크를 선택합니다.

1. *권한 관리* 페이지에서 이전 랩에서 만든 **RG-플레이북** 리소스 그룹을 선택하고 **적용**을 선택합니다.

1. 드롭다운 목록에서 **Defender_XDR_Ransomware_Playbook_SecOps_Tasks** 플레이북을 선택합니다.

1. 아래쪽에서 **적용**을 선택합니다.

1. *새 자동화 규칙 만들기* 창에서 **X**를 선택하고 닫습니다.

이제 Microsoft Sentinel에서 플레이북과 자동화 규칙을 만들었습니다.

## 연습 3 계속 진행
