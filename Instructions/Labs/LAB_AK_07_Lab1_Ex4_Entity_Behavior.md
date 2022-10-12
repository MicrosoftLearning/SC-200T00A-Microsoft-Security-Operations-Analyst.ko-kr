---
lab:
  title: 연습 4 -엔터티 동작 분석 살펴보기
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-4---explore-entity-behavior-analytics"></a>모듈 7 - 랩 1 - 연습 4 - 엔터티 동작 분석 살펴보기

## <a name="lab-scenario"></a>랩 시나리오

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 예약됨 및 Microsoft 보안 분석 규칙을 이미 만들었습니다. 


엔터티 동작 분석을 수행하여 변칙을 검색하고 엔터티 분석 페이지를 제공하도록 Microsoft Sentinel을 구성해야 합니다.


### <a name="task-1-enable-entity-behavior"></a>작업 1: 엔터티 동작 사용 

이 작업에서는 Microsoft Sentinel에서 엔터티 동작 분석을 사용하도록 설정합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. **엔터티 동작** 페이지를 선택합니다.
1. 엔터티 동작 설정의 팝업에서 **EUBA 설정**을 선택합니다.
1. 다음 페이지에서 **UEBA 설정**을 선택합니다.
1. 엔터티 동작 구성 페이지에서 1번의 기능을 **켜기**로 토글합니다. 
1. *2.* 의 경우, **Azure Active Directory**를 선택합니다. 그런 다음, **적용**을 선택합니다.
1. *3.* 의 경우 **감사 로그**, **Azure 활동**, **보안 이벤트** 및 **로그인 로그**를 선택합니다. 
1. 그런 다음, **적용**을 선택합니다.
1. 수집된 로그 데이터와 생성된 경고를 기반으로 채워진 엔터티를 보려면 랩 중에 이 페이지로 자주 돌아갑니다.


### <a name="task-2-confirm-and-review-anomalies-rules"></a>작업 2: 변칙 규칙 확인 및 검토

이 작업에서는 변칙 분석 규칙이 사용하도록 설정되어 있는지 확인합니다.

1. **분석** 페이지를 선택합니다.
1. **변칙** 페이지를 선택합니다.
1. 규칙의 상태 열이 사용인지 확인합니다.
1. 규칙을 선택합니다. 그런 다음, 규칙 블레이드에서 **편집**을 선택합니다.
1. 일반 탭 정보를 검토합니다. 그런 다음, 페이지 아래쪽의 **다음: 구성** 클릭
1. 구성 탭 정보를 검토합니다. 그런 다음, 오른쪽 위 모서리에서 **X**를 선택하여 분석 규칙 마법사를 종료합니다.


## <a name="proceed-to-exercise-5"></a>연습 5 계속 진행
