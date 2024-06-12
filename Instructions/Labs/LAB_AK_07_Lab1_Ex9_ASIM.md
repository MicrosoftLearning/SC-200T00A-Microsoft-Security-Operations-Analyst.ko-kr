---
lab:
  title: 연습 9 - ASIM 파서 만들기
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# 학습 경로 7 - 랩 1 - 연습 9 - ASIM 파서 배포

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. 특정 Windows 레지스트리 이벤트에 대한 ASIM 파서를 모델링해야 합니다. 이러한 파서는 나중에 [ASIM(고급 보안 정보 모델) 레지스트리 이벤트 정규화 스키마 참조](https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema)에 따라 완성될 예정입니다.

>**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20Advanced%20Security%20Information%20Model%20Parsers)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 

### 작업 1: 레지스트리 스키마 ASIM 파서 배포

이 작업에서는 Microsoft Sentinel 배포에 포함된 레지스트리 스키마 파서를 검토합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저에서 https://portal.azure.com의 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

<!--- 1. In the Edge browser, open a new tab (Ctrl+T) and navigate to the Microsoft Sentinel GitHub ASIM page <https://github.com/Azure/Azure-Sentinel/tree/master/ASIM>.

 1. On the right pane, select the **Onboard community content** link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel).

    >**Note:** In the **ASIM** folder you can deploy templates that contain all ASIM parsers, but we will only focus on the Registry Schema.

<!--- 1. Scroll down and next to **Registry Event**, select the **Deploy to Azure** button.

1. For *Resource Group*, select **RG-Defender** where your Sentinel workspace resides.

1. For *Workspace*, type your Sentinel workspace name, like *uniquenameDefender*.

1. Leave the other default values and select **Review + create**.

1. Select **Create** to deploy the template. Notice the Names of the different resources. 

1. After the deployment completes return to the *Microsoft Sentinel* tab. --->

1. *일반* 왼쪽 메뉴에서 **로그**를 선택합니다.

1. 필요한 경우 **>>** 를 선택하여 *스키마 및 필터* 블레이드를 엽니다.

1. **함수** 탭(테이블 및 쿼리 탭 옆)을 선택합니다. **힌트:** 탭을 선택하려면 줄임표 아이콘 **(...)** 을 선택해야 할 수도 있습니다.

1. *검색* 표시줄에서 **레지스트리**를 입력하고 *Microsoft Sentinel* 제목 아래에 Microsoft Windows에 대한 다음 *_Im_RegistryEvent_MicrosoftWindowsEventxxx*가 보일 때까지 ASIM 파서 함수를 아래로 스크롤합니다.

    >**참고:** 버전 변경을 설명하기 위해 ASIM 파서 함수 이름에 xxx를 사용합니다. 이 랩이 업데이트되었을 때 함수는 _Im_RegistryEvent_MicrosoftWindowsEvent*V02*였습니다.

1. **_Im_RegistryEvent_MicrosoftWindowsEventxxx** ASIM 함수 위에 커서를 올린 다음 팝업 창에서 **함수 코드 로드**를 선택합니다.

1. Microsoft Sentinel 작업 영역에서 데이터 분석을 간소화하기 위해 이벤트 ID 4657을 구문 분석하는 KQL을 검토합니다.

    >**힌트:** 코드 창에서 ctrl+f를 입력하면 *찾기*가 표시되어 *EventID: 4657*을 찾기가 훨씬 쉬워집니다.

1. *스키마 및 필터* 블레이드로 돌아가서 이제 **_Im_RegistryEvent_MicrosoftWindowsEventxxx** *Microsoft Windows 이벤트 및 보안 이벤트에 대한 레지스트리 이벤트 ASIM 필터링 파서*에 커서를 올린 다음 **편집기에서 사용**을 선택합니다.

1. ASIM 함수 쿼리를 **실행**합니다. 결과나 오류를 가져와서는 안 되며, 유효성 검사 목적으로만 사용해야 합니다.

## 연습 10 계속 진행