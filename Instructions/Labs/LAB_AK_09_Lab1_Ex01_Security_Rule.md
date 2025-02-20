---
lab:
  title: 연습 1 - Microsoft 보안 규칙 수정
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 9 - 랩 1 - 연습 1 - Microsoft 보안 규칙 수정

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel을 사용하여 위협을 검색하고 완화하는 방법을 파악해야 합니다. 먼저 클라우드용 Defender에서 Microsoft Sentinel로 들어오는 경고를 심각도별로 필터링해야 합니다.

>**중요:** 학습 경로 #9에 대한 랩 연습은 *독립 실행형* 환경에 있습니다. 완료하기 전에 랩을 종료하면 구성을 다시 실행해야 합니다.

### 이 랩의 예상 완료 시간은 10분입니다.

### 작업 1: Microsoft 보안 규칙 활성화

이 작업에서는 Microsoft 보안 규칙을 활성화합니다.

>**참고:** Microsoft Sentinel이 Azure 구독에 **defenderWorkspace**라는 이름으로 사전 배포되었으며 필요한 *콘텐츠 허브* 솔루션이 설치되어 있습니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저에서 <https://portal.azure.com>의 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel **defenderWorkspace**을 선택합니다.

1. 구성 영역에서 **분석**을 선택합니다.

1. 명령 모음에서 **+ 만들기** 단추를 선택하고 **Microsoft 인시던트 만들기 규칙**을 선택합니다.

1. *이름* 아래에 **클라우드용 Defender를 기반으로 인시던트 만들기**를 입력합니다.

1. 아래로 스크롤하여 *Microsoft 보안 서비스*에서 **클라우드용 Microsoft Defender**를 선택합니다.

1. *심각도별 필터링*에서 *사용자 지정* 옵션을 선택하고 심각도 수준을 **낮음**, **보통** 및 **높음**으로 선택한 다음 규칙으로 돌아옵니다.

1. 하단에서 **다음: 자동 응답** 단추를 클릭한 후 **다음: 검토 및 만들기** 단추를 선택합니다.

1. 변경 내용을 검토하고 **저장** 단추를 선택합니다. 클라우드용 Defender에 경고가 있는 경우 분석 규칙이 저장되고 인시던트가 만들어집니다.

1. 이제 하나의 *Fusion* 경고 유형과 두 개의 *Microsoft 보안* 경고 유형이 제공됩니다.

## 연습 2 계속 진행
