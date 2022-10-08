---
lab:
  title: 연습 1 - Microsoft 보안 규칙 수정
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-1---modify-a-microsoft-security-rule"></a>모듈 7 - 랩 1 - 연습 1 - Microsoft 보안 규칙 수정

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. First, you need to filter the alerts coming from Defender for Cloud into Microsoft Sentinel, by Severity. 


### <a name="task-1-activate-a-microsoft-security-rule"></a>작업 1: Microsoft 보안 규칙 활성화

이 작업에서는 Microsoft 보안 규칙을 활성화합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com) )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 이전 랩에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. Select <bpt id="p1">**</bpt>Analytics<ept id="p1">**</ept> from the Configuration area. By default, you will see the <bpt id="p1">*</bpt>Active rules<ept id="p1">*</ept>. Click on <bpt id="p1">*</bpt>Rule templates<ept id="p1">*</ept>.

1. Search for and select <bpt id="p1">**</bpt>Create incidents based on Microsoft Defender for Cloud<ept id="p1">**</ept>. This rule was activated by the Defender for Cloud connector we configured in "Module 6 - Exercise 1 - Task 4". 

1. 오른쪽 블레이드에서 **편집** 단추를 선택합니다.

1. 페이지를 아래로 스크롤하고 “분석 규칙 논리 - 심각도로 필터링”에서 사용자 지정 드롭다운 목록을 선택합니다.

1. 심각도 수준에 대해 **낮음**의 선택을 취소하고 규칙으로 돌아갑니다.

1. 하단에서 **다음: 자동화된 응답** 단추를 선택한 후, **다음: 검토** 단추를 클릭합니다.

1. Review the changes made and select the <bpt id="p1">**</bpt>Save<ept id="p1">**</ept> button. The Analytics rule will be saved.

## <a name="proceed-to-exercise-2"></a>연습 2 계속 진행
