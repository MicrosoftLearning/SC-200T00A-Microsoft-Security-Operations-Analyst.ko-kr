---
lab:
  title: 연습 8 - 인시던트 조사
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-8---investigate-incidents"></a>모듈 7 - 랩 1 - 연습 8 - 인시던트 조사

## <a name="lab-scenario"></a>랩 시나리오


You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You already created Scheduled and Microsoft Security Analytics rules. The Fusion and Anomalies Analytics rules are also enabled in your environment. Now is the time to investigate the Incidents created by them.

An incident can include multiple alerts. It is an aggregation of all the relevant evidence for a specific investigation. The properties related to the alerts, such as severity and status, are set at the incident level. After you let Microsoft Sentinel know what kinds of threats you are looking for and how to find them, you can monitor detected threats by investigating incidents.


### <a name="task-1-investigate-an-incident"></a>작업 1: 인시던트 조사

이 작업에서는 인시던트를 조사합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. **인시던트** 페이지를 선택합니다.

1. 인시던트 목록을 검토합니다.

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The Analytics rules are generating alerts and incidents on the same specific log entry. Remember that this was done in the <bpt id="p1">*</bpt>Query scheduling<ept id="p1">*</ept> configuration to generate more alerts and incidents to be utilized in the lab.
  
1. *MDE Startup RegKey* 인시던트 중 하나를 선택합니다.

1. Review the incident details on the right blade that opened. Scroll down and select the <bpt id="p1">**</bpt>View full details<ept id="p1">**</ept> button.

1. 인시던트 왼쪽 블레이드에서 상태를 **활성**으로 변경한 다음, **적용**을 선택합니다.

1. 태그 영역까지 아래로 스크롤하여 **+** 를 선택하고, **RegKey**를 입력하고, **확인**을 선택합니다.

1. 가운데 창에서 **설명** 탭을 선택합니다.

1. 설명 상자에 조사할 내용입니다.를 입력하고 **설명** 단추를 선택하여 새 설명을 제출합니다.

1. 당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다.

1. 예약됨 및 Microsoft 보안 분석 규칙을 이미 만들었습니다.

1. 퓨전 및 변칙 분석 규칙도 환경에서 사용할 수 있습니다.

1. 이제 규칙에 따라 만들어진 인시던트를 조사하겠습니다.

1.  When you select an entity, a window on the right opens for more detailed information. Review the <bpt id="p1">**</bpt>Info<ept id="p1">**</ept> page.

1. 인시던트는 여러 경고를 포함할 수 있습니다.

1. **엔터티** 단추를 선택하고 *WIN1*과 관련된 엔터티 및 경고를 검토합니다. 

1. 페이지 오른쪽 위에 있는 **X**를 선택하여 조사 그래프를 닫습니다.

1. 이는 특정 조사에 대한 모든 관련 증거를 집계한 것입니다.

1. 심각도 및 상태와 같은 경고와 관련된 속성은 인시던트 수준에서 설정됩니다.

## <a name="proceed-to-exercise-9"></a>연습 9 계속 진행
