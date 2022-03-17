---
lab:
  title: 연습 3 - 예약된 쿼리 만들기
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
ms.openlocfilehash: c76ba6f5bdd5c1f380393b3f0ebbdb16c85626c1
ms.sourcegitcommit: 175df7de88c9a609f8caf39840664bf992c5b6dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2022
ms.locfileid: "138025479"
---
# <a name="module-7---lab-1---exercise-3---create-a-scheduled-query"></a>모듈 7 - 랩 1 - 연습 3 - 예약된 쿼리 만들기

## <a name="lab-scenario"></a>랩 시나리오

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel을 사용하여 위협을 검색하고 완화하는 방법을 파악해야 합니다. 데이터 원본을 Microsoft Sentinel에 연결한 후, 사용자 환경에서 위협 및 비정상적인 동작을 검색하는 데 도움이 되는 사용자 지정 분석 규칙을 만듭니다.

분석 규칙은 사용자 환경에서 특정 이벤트 또는 이벤트 집합을 검색하고, 특정 이벤트 임계값 또는 조건에 도달하면 경고를 생성하고, SOC에서 심사 및 조사를 위해 인시던트를 생성하고, 자동화된 추적 및 수정 프로세스를 통해 위협에 대응합니다.


### <a name="task-1-create-a-scheduled-query"></a>작업 1: 예약된 쿼리 만들기

이 작업에서는 예약된 쿼리를 만들고 이를 이전 연습에서 만든 Teams 채널에 연결합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd** 를 사용하여 로그인합니다.  

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음** 을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호** 를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인** 을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel* 을 입력하고 **Microsoft Sentinel** 을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. 구성 영역에서 **분석** 을 선택합니다.

1. **+ 만들기** 단추를 선택하고 **예약된 쿼리 규칙** 을 선택합니다.

1. 분석 규칙 마법사의 일반 탭에서 Azure AD 역할 할당 감사 내역 이름을 입력합니다.

1. 전술의 경우 **지속성** 을 선택합니다.

1. 심각도는 **낮음** 을 선택합니다.

1. **다음: 규칙 논리 설정 >** 단추를 선택합니다.

1. 규칙 쿼리에 다음 KQL 문을 붙여넣습니다.

    >**경고:** 가상 머신에 붙여넣기 함수를 사용하는 경우 추가(파이프) 문자를 추가할 수 있습니다. 먼저 메모장 사용하여 다음 쿼리를 붙여넣는지 확인합니다.

    ```KQL
    AuditLogs  
    | where isnotempty(InitiatedBy.user.userPrincipalName) and Result == 'success' and OperationName contains "member to role" and AADOperationType startswith "Assign"
    | extend InitiatedByUPN = tostring(InitiatedBy.user.userPrincipalName)
    | extend InitiatedFromIP = iff(tostring(AdditionalDetails.[7].value) == '', tostring(AdditionalDetails.[6].value), tostring(AdditionalDetails.[7].value))
    | extend TargetUser = tostring(TargetResources.[2].displayName)
    | extend TargetRoleName = tostring(TargetResources.[0].displayName)
    | project TimeGenerated, InitiatedByUPN, InitiatedFromIP, TargetUser, TargetRoleName, AADOperationType, OperationName
    ```

1. **쿼리 결과 보기** 를 선택합니다. 결과나 오류를 수신해서는 안 됩니다. 오류가 발생하면 쿼리가 이전 KQL 문과 같이 표시되는지 검토하세요. 오른쪽 위 **X** 를 선택하여 로그 창을 닫고 **확인** 을 선택하여 취소하고 변경 내용을 저장하여 마법사로 돌아갑니다.

1. “분석 규칙 마법사 - 예약된 새 규칙 만들기” 블레이드의 *경고 보강* 영역에서 **엔터티 매핑** 을 선택하고 다음 값을 선택합니다. 

    - 엔터티 유형 드롭다운 목록에서 **Account** 를 선택합니다.
    - 식별자 드롭다운 목록에서 **FullName** 을 선택합니다.
    - 값 드롭다운 목록에서 **InitiatedByUPN** 을 선택합니다.

1. 그런 다음, **새 엔터티 추가** 를 선택하고 다음 값을 선택합니다.

    - 엔터티 유형 드롭다운 목록에서 **IP** 를 선택합니다.
    - 식별자 드롭다운 목록에서 **Address** 를 선택합니다.
    - 값 드롭다운 목록에서 **InitiatedFromIP** 를 선택합니다.

1. 아래로 스크롤하여 쿼리 예약에서 다음을 설정합니다.

    |설정|값|
    |---|---|
    |쿼리 실행 간격|5분|
    |마지막부터 데이터 보기|1일|

    >**참고:** 같은 데이터에 대해 의도적으로 여러 인시던트를 생성합니다. 그러면 랩에서 해당 경고를 사용할 수 있기 때문입니다.

1. 경고 임계값 영역에서 경고가 모든 이벤트를 등록하도록 하므로 값을 변경하지 않고 그대로 둡니다.

1. 쿼리가 위에 지정된 경고 임계값보다 더 많은 결과를 반환하는 한 이벤트 그룹화 영역에서는 실행될 때마다 단일 경고를 생성하려고 하므로 **모든 이벤트를 단일 경고로 그룹화** 합니다.

1. 하단에서 **다음: 인시던트 설정 >** 단추를 선택합니다. 

1. 인시던트 설정(미리 보기) 탭에서 기본 옵션을 검토합니다.

1. 하단에서 **다음: 자동화된 응답 >** 단추를 선택합니다.

1. 경고 자동화 영역의 자동화된 응답 탭에서 이전 연습에서 만든 *PostMessageTeams-OnAlert* 플레이북을 선택합니다.

1. 하단에서 **다음: 검토 >** 단추를 선택합니다.
  
1. **만들기** 를 선택합니다.


### <a name="task-2-test-our-new-rule"></a>작업 2: 새 규칙 테스트

이 작업에서는 새 예약된 쿼리 규칙을 테스트합니다.

1. Azure Portal의 검색 창에 *Azure Active Directory* 를 입력합니다. 그런 다음 **Azure Active Directory** 를 선택합니다.

1. “사용자 - 모든 사용자” 페이지가 표시되도록 관리 영역에서 **사용자** 를 선택합니다.

1. “Christie Cline - 프로필” 페이지가 표시되도록 목록에서 사용자 **Christie Cline** 을 선택합니다.

1. “Christie Cline - 할당된 역할” 페이지가 표시되도록 관리 영역에서 **할당된 역할** 을 선택합니다.

1. 명령 모음에서 **+ 할당 추가** 를 선택합니다.

1. 할당 추가 페이지의 멤버 자격 탭의 역할 선택에서 **사용자 관리자** 를 선택합니다.   그리고 **다음 >** 을 선택합니다.

1. 설정 탭에서 기본 할당 유형을 검토한 다음, **할당** 을 선택합니다.  할당이 완료되지 않으면 다시 시도합니다.

1. 오른쪽 위에 있는 ‘x’를 두 번 선택하여 “Christie Cline - 할당된 역할” 및 “사용자 - 모든 사용자” 페이지를 닫습니다.

1. “Contoso - 개요” Azure Active Directory 페이지의 *모니터링* 에서 **감사 로그** 를 선택합니다.

1. **데이터 내보내기 설정** 을 선택합니다. 진단 설정 정보를 검토하여 Microsoft Sentinel의 “Azure Active Directory” 데이터 커넥터가 Log Analytics 작업 영역으로 데이터를 전송하도록 구성을 올바르게 설정했는지 확인합니다.

1. 이전에 Sentinel용으로 만든 Log Analytics 작업 영역에 대한 진단 설정 항목이 있는지 검토합니다. 

1. 오른쪽 위에서 ‘x’를 선택하여 페이지를 닫습니다.

1. “Contoso - 감사 로그”로 돌아가서 이전에 수행한 역할의 변경을 나타내는 카테고리: RoleManagement에 대한 항목이 표시될 때까지 **새로 고침** 을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel* 을 입력하고 **Microsoft Sentinel** 을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. **인시던트** 메뉴 옵션을 선택합니다.

    >**참고:** 트리거된 경고를 처리하는 데 5분 정도 걸릴 수 있습니다. 다음 연습을 계속 진행하다가 나중에 이 지점으로 돌아와도 됩니다. 인시던트 페이지를 자동으로 업데이트하려면 **인시던트 자동 새로 고침** 토글을 선택합니다.

1. 새로 만든 인시던트가 표시됩니다. 인시던트를 선택하고 오른쪽 블레이드의 정보를 검토합니다.

1. Edge 브라우저에서 탭을 선택하여 Microsoft Teams로 돌아갑니다. 닫은 경우 새 탭을 열고 https://teams.microsoft.com 을 입력합니다. *SOC* Teams로 이동하여 새 경고 채널을 선택하고 인시던트에 대한 메시지 게시물을 확인합니다.

## <a name="proceed-to-exercise-4"></a>연습 4 계속 진행
