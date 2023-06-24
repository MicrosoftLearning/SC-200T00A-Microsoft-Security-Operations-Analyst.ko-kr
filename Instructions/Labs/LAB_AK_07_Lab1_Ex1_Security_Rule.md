---
lab:
  title: 연습 1 - Microsoft 보안 규칙 수정
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 7 - 랩 1 - 연습 1 - Microsoft 보안 규칙 수정

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel을 사용하여 위협을 검색하고 완화하는 방법을 파악해야 합니다. 먼저 클라우드용 Defender에서 Microsoft Sentinel로 들어오는 경고를 심각도별로 필터링해야 합니다. 

>                **참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Modify%20a%20Microsoft%20Security%20rule)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 


### 작업 1: Microsoft 보안 규칙 활성화

이 작업에서는 Microsoft 보안 규칙을 활성화합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com) )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 이전 랩에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 구성 영역에서 **분석**을 선택합니다. 기본적으로 활성 규칙이 표시됩니다.

1. **클라우드용 Microsoft Defender 기반으로 인시던트 만들기를 확인합니다**. 이 규칙은 “모듈 6 - 연습 1 - 작업 4”에서 구성한 클라우드용 Defender 커넥터에 의해 활성화되었습니다.

1. 명령 모음에서 **+ 만들기** 단추를 클릭하고 **Microsoft 인시던트 생성 규칙을** 선택합니다.

1. *이름* 아래에서 **엔드포인트용 Defender를 기반으로 인시던트 만들기를** 기록합니다.

1. 아래로 스크롤하고 *Microsoft 보안 서비스* 아래에서 **엔드포인트용 Microsoft Defender** 선택합니다.

1. *심각도로 필터링*에서 *사용자 지정* 옵션을 선택하고 심각도 수준에 대해 **낮음**, **보통** 및 **높음** 을 선택하고 규칙으로 돌아갑니다.

1. 하단에서 **다음: 자동화된 응답** 단추를 선택한 후, **다음: 검토** 단추를 클릭합니다.

1. 변경 내용을 검토하고 **만들기** 단추를 선택합니다. 분석 규칙이 저장되고 엔드포인트용 Defender에 경고가 있는 경우 인시던트가 생성됩니다.

1. 이제 Fusion 1개와 Microsoft 보안 경고 유형 2개가 있습니다.


## 연습 2 계속 진행
