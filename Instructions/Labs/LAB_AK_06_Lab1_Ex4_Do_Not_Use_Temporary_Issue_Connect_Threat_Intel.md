---
lab - Do not use. Temporarily not operational!:
  title: 연습 4 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 위협 인텔리전스 연결
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-4---connect-threat-intelligence-to-microsoft-sentinel-using-data-connectors"></a>모듈 6 - 랩 1 - 연습 4 - 데이터 커넥터를 사용하여 Microsoft Sentinel에 위협 인텔리전스 연결

## <a name="lab-scenario"></a>랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex4.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. Finally, you connect a threat intelligence feed to enhance your ability to detect and prioritize known threats.

### <a name="task-1-connect-threat-intelligence"></a>작업 1: 위협 인텔리전스 연결

이 작업에서는 위협 인텔리전스 - TAXII 커넥터를 사용하여 위협 인텔리전스 공급자를 연결합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(<https://portal.azure.com>)로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 데이터 커넥터 탭에서 **위협 인텔리전스 - TAXII** 커넥터를 선택합니다.

1. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

1. 구성 영역에서 **식별 이름(서버용)** 으로 *PhishURLs*를 입력합니다.

1. API 루트 URL에 대해 <https://limo.anomali.com/api/v1/taxii2/feeds/> 를 입력합니다.

1. 컬렉션 ID로는 **107**을 입력합니다.

1. 사용자 이름으로는 **guest**를 입력합니다.

1. 암호로는 **guest**를 입력합니다.

1. Now select the <bpt id="p1">**</bpt>Add<ept id="p1">**</ept> button.  Phishing URLs will be pulled and populate the ThreatIntelligenceIndicator table.

>**참고:** 다른 컬렉션을 추가하려면 Edge 브라우저에서 <https://limo.anomali.com/api/v1/taxii2/feeds/collections/> 를 열고 게스트 사용자 이름과 암호를 사용하여 사용 가능한 다른 ID를 검토합니다.

## <a name="you-have-completed-the-lab"></a>이 랩을 완료했습니다.
