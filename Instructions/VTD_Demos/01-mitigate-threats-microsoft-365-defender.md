# <a name="module-1---mitigate-threats-using-microsoft-365-defender"></a>모듈 1 – Microsoft 365 Defender를 사용하여 위협 완화

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## <a name="use-the-microsoft-365-defender-portal"></a>Microsoft 365 Defender 포털 사용

이 작업에서는 Microsoft 365 Defender 포털 기능을 숙지합니다.

- 홈(대시보드)
- 인시던트 및 경고
- 사냥
- 알림 센터
- 위협 분석
- 보안 점수
- 엔드포인트
- 취약점 관리
- 전자 메일 및 공동 작업
- 클라우드 앱
- 보고서
- 설정
- 사용 권한

1. 브라우저에 Microsoft Defender 보안 센터가 아직 열려 있지 않으면 Microsoft Defender 보안 센터(https://security.microsoft.com) )로 이동하여 테넌트 관리자로 로그인합니다.

1. In the <bpt id="p1">**</bpt>Home<ept id="p1">**</ept> dashboard you can overall view of your secure status. You can customize the view by <bpt id="p1">**</bpt>Add cards<ept id="p1">**</ept> or removing cards. To remove a card, select the ellipsis (...) on a card.
1. Next select <bpt id="p1">**</bpt>Incidents &amp; Alerts<ept id="p1">**</ept>. This will expand the menu choices below. This is where investigations are performed.
1. **헌팅**과 동일한 작업을 수행하여 **고급 헌팅** 쿼리 페이지를 노출합니다. 
    1. 여기서 KQL 쿼리를 실행할 수 있습니다.
1. **작업 및 제출**을 선택하면 **알림 센터** 및 **제출**이 노출됩니다
1. Select <bpt id="p1">**</bpt>Threat analytics<ept id="p1">**</ept>. This page provides insights into the Common Vulnerabilities and Exposures (CVE) you need to track
1. Select the <bpt id="p1">**</bpt>Secure Score<ept id="p1">**</ept> and explore the tabs. Take a look at <bpt id="p1">**</bpt>Recommendations<ept id="p1">**</ept> here.
1. Select <bpt id="p1">**</bpt>Endpoints<ept id="p1">**</ept> and <bpt id="p2">**</bpt>Device Inventory<ept id="p2">**</ept> options are available. You can onboard devices here or work with an existing inventory.
1. Also in the <bpt id="p1">**</bpt>Endpoints<ept id="p1">**</ept> section is <bpt id="p2">**</bpt>Vulnerability management<ept id="p2">**</ept>. Vulnerability management has a Dashboard where yu can look review your Exposure score.
1. Another capability within <bpt id="p1">**</bpt>Endpoints<ept id="p1">**</ept> is <bpt id="p2">**</bpt>Evaluations &amp; simulations<ept id="p2">**</ept>. The <bpt id="p1">**</bpt>Evaluation lab<ept id="p1">**</ept> allows you to setup isolated devices for exploring malware.
1. In the <bpt id="p1">**</bpt>Email &amp; collaboration<ept id="p1">**</ept> section are the Defender for Office 365 capabilities. <bpt id="p1">**</bpt>Investigations<ept id="p1">**</ept> is where you see results of Automated investigation and Response (AIR) threat investigations.
1. Also in <bpt id="p1">**</bpt>Email &amp; collaboration<ept id="p1">**</ept> are <bpt id="p2">**</bpt>Polices &amp; rules<ept id="p2">**</ept>. You will configure <bpt id="p1">**</bpt>Threat &amp; Alert<ept id="p1">**</ept> polices here.
1. Scroll down to <bpt id="p1">**</bpt>Cloud apps<ept id="p1">**</ept>. This the <bpt id="p1">**</bpt>Microsoft Defender for Cloud Apps<ept id="p1">**</ept> service section. Under <bpt id="p1">**</bpt>App governance<ept id="p1">**</ept> is where you set app policies.
1. 다음 섹션에는 Microsoft 365 Defender 서비스용 **보고서**, 관리자 작업 추적을 사용하도록 설정할 수 있는 **AUdit**, **권한** 및 **설정**이 있습니다.
1. **권한**에서 **Azure AD** 및 **엔드포인트** 역할을 구성할 수 있습니다.
1. **설정**은 표준 시간대 및 이메일 알림과 같은 일반 구성과 엔드포인트, ID 및 디바이스 검색에 대한 세분화된 설정을 입력하는 위치입니다.
1. Select <bpt id="p1">**</bpt>Settings<ept id="p1">**</ept>, then <bpt id="p2">**</bpt>Endpoints<ept id="p2">**</ept>. You can view and add <bpt id="p1">**</bpt>Licenses<ept id="p1">**</ept> here. Next select <bpt id="p1">**</bpt>Advanced features<ept id="p1">**</ept>. Scroll thorough the list of features, but don't make any changes now.
1. Lastly, leave <bpt id="p1">**</bpt>Settings<ept id="p1">**</ept> and on the main, left menu list select <bpt id="p2">**</bpt>More resources<ept id="p2">**</ept>. You should see cards or tiles with links for <bpt id="p1">**</bpt>Microsoft Purview Compliance<ept id="p1">**</ept>, <bpt id="p2">**</bpt>Azure Active Directory<ept id="p2">**</ept> and other capabilities not directly part of <bpt id="p3">**</bpt>Microsoft 365 Defender<ept id="p3">**</ept>. Select the <bpt id="p1">**</bpt>Open<ept id="p1">**</ept> button for <bpt id="p2">**</bpt>Microsoft Purview Compliance<ept id="p2">**</ept>. This will open the compliance portal.

## <a name="you-have-completed-the-lab"></a>이 랩을 완료했습니다.