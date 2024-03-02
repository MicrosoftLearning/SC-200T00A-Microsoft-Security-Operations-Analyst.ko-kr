---
lab:
  title: 연습 9 - ASIM 파서 만들기
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 7 - 랩 1 - 연습 9 - ASIM 파서 배포

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 특정 Windows 레지스트리 이벤트에 대한 ASIM 파서를 모델링해야 합니다. 이러한 간소화된 파서는 나중에 [ASIM(고급 보안 정보 모델) 레지스트리 이벤트 정규화 스키마 참조](https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema)에 따라 완성될 예정입니다.

>**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20Advanced%20Security%20Information%20Model%20Parsers)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 

### 작업 1: 레지스트리 스키마 ASIM 파서 배포

이 작업에서는 Microsoft Sentinel GitHub 리포지토리에서 레지스트리 스키마 파서를 배포합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 이메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. Edge 브라우저에서 새 탭(Ctrl+T)을 열고 Microsoft Sentinel GitHub ASIM 페이지 <https://github.com/Azure/Azure-Sentinel/tree/master/ASIM>으로 이동합니다.

    <!--- 1. On the right pane, select the **Onboard community content** link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel). --->

    >**참고:** **ASIM** 폴더에서는 모든 ASIM 파서를 포함하는 템플릿을 배포할 수 있지만 여기서는 레지스트리 스키마에만 중점을 둘 것입니다.

1. 아래로 스크롤하여 **레지스트리** 옆에 있는 **Azure에 배포** 단추를 선택합니다.

1. *리소스 그룹*의 경우 Sentinel 작업 영역이 있는 **RG-Defender**를 선택합니다.

1. *작업 영역*에 *uniquenameDefender*와 같은 Sentinel 작업 영역 이름을 입력합니다.

1. 다른 기본값은 그대로 두고 **검토 + 만들기**를 선택합니다.

1. **만들기**를 선택하여 템플릿을 배포합니다. 다양한 리소스의 이름을 확인합니다.

1. 배포가 완료되면 *Microsoft Sentinel* 탭으로 돌아갑니다.

1. *일반* 왼쪽 메뉴에서 **로그**를 선택합니다.

1. 필요한 경우 **>>** 를 선택하여 *스키마 및 필터* 블레이드를 엽니다.

1. **함수** 탭(테이블 및 쿼리 탭 옆)을 선택합니다. **힌트:** 탭을 선택하려면 줄임표 아이콘 **(...)** 을 선택해야 할 수도 있습니다.

1. **작업 영역 함수**을 확장합니다. 이름은 방금 배포한 템플릿과 일치합니다.

1. **vimRegistryEventMicrosoftSecurityEvents** *작업 영역 파서* 위로 마우스를 가져간 다음 팝업 창에서 **함수 코드 로드**를 선택합니다.

1. Microsoft Sentinel 작업 영역에서 데이터 분석을 간소화하기 위해 이벤트 ID 4657을 구문 분석하는 KQL을 검토합니다.

1. 쿼리를 **실행**합니다. 결과나 오류를 가져와서는 안 되며 유효성 검사 목적으로만 사용됩니다.

1. *스키마 및 필터* 블레이드로 돌아가서 이제 **inRegistry** *통합 파서* 위로 마우스를 가져간 다음 **함수 코드 로드**를 선택합니다.

1. 공용 구조체 파서는 *union* 연산자를 사용하여 모든 작업 영역 파서를 한 번에 실행합니다. 레지스트리 스키마용 파서를 개발하는 경우 여기에 추가해야 합니다.

1. 쿼리를 **실행**합니다. 결과나 오류를 가져와서는 안 되며 유효성 검사 목적으로만 사용됩니다.

1. 이제 이 통합 파서는 분석 규칙이나 헌팅 쿼리에 사용할 수 있습니다.

## 연습 10 계속 진행