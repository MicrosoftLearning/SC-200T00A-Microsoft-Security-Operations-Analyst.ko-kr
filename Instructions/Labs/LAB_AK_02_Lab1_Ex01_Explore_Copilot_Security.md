---
lab:
  title: 연습 1 - Microsoft Security Copilot 사용 사례 살펴보기
  module: Learning Path 2 - Mitigate threats using Microsoft Security Copilot
---

# 학습 경로 2 - 랩 1 - 연습 1 - Microsoft Security Copilot 살펴보기

## 랩 시나리오

근무하는 조직에서 보안 운영 분석가의 효율성과 역량을 높여 보안 결과를 개선하려고 합니다. 해당 목표를 지원하기 위해 CISO 사무실에서는 Microsoft Security Copilot 배포가 해당 목표를 향한 핵심 단계라고 판단했습니다. 조직의 보안 관리자로서 사용자는 Copilot을 설정하는 임무를 맡고 있습니다.

이 연습에서는 Microsoft Security Copilot의 *첫 번째 실행 환경*을 살펴보고 하나의 SCU(보안 컴퓨팅 단위)로 Copilot을 프로비전합니다.

>**참고:** 이 연습의 환경은 제품에서 생성된 시뮬레이션입니다. 제한된 시뮬레이션으로 페이지의 링크가 사용하도록 설정되지 않을 수 있으며 지정된 스크립트를 벗어나는 텍스트 기반 입력은 지원되지 않을 수 있습니다. "이 기능은 시뮬레이션 내에서 사용할 수 없습니다."라는 팝업 메시지가 표시됩니다. 이 경우 확인을 선택하고 연습 단계를 계속합니다.  
> :::image type="content" source="../media/simulation-pop-up-error.png" alt-text="시뮬레이션 내에서 이 기능을 사용할 수 없음을 나타내는 팝업 화면의 스크린샷.":::

### 이 랩의 예상 완료 시간은 45분입니다.

### 작업 1: Microsoft Security Copilot 프로비전

이 연습에서는 Avery Howard로 로그인했으며 Microsoft Entra에서 전역 관리자 역할이 있습니다. Azure Portal과 Microsoft Security Copilot 모두에서 작업합니다.

이 연습을 완료하는 데 약 **15**분 정도 소요됩니다.

>**참고:** 랩 지침에서 시뮬레이션 환경에 대한 링크를 열어야 하는 경우 일반적으로 지침과 연습 환경을 동시에 볼 수 있도록 새 브라우저 창에서 링크를 여는 것이 좋습니다. 이렇게 하려면 마우스 오른쪽 키를 선택하고 옵션을 선택합니다.

사용자가 Copilot 사용을 시작하기 전에 관리자는 용량을 프로비전하고 할당해야 합니다. 용량을 프로비전하려면 다음을 수행합니다.

- Azure 구독이 있어야 합니다.
- 최소한 리소스 그룹 수준에서 Azure 소유자 또는 Azure 기여자여야 합니다.

이 작업에서는 적절한 역할 권한이 있는지 확인하는 프로세스를 안내합니다. 이는 Azure 리소스에 대한 액세스 관리를 사용하도록 설정하는 것부터 시작됩니다.

Azure에서 사용자 액세스 관리자 역할이 할당되면 사용자에게 Copilot용 SCU를 프로비전하는 데 필요한 액세스 권한을 할당할 수 있습니다.  관련 단계를 보여주기 위한 이 연습의 용도로만 필요한 액세스 권한을 자신에게 할당하게 됩니다.  다음 단계는 프로세스를 안내합니다.

1. 다음 링크를 선택하여 시뮬레이션 환경을 엽니다. **[Azure Portal](https://app.highlights.guide/start/6373500f-1f10-4584-a14e-ca0b4aa7399f?link=1&token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)**.

1. Azure 리소스에 대한 액세스 관리를 사용하도록 설정하는 것부터 시작합니다. 이 설정에 액세스하려면
    1. Azure Portal에서 **Microsoft Entra ID**를 선택합니다.
    1. 왼쪽 탐색 패널에서 **관리**를 확장합니다.
    1. 왼쪽 탐색 패널에서 아래로 스크롤하여 **속성**을 선택합니다.
    1. **Azure 리소스에 대한 액세스 관리**에 대한 토글 스위치를 사용하도록 설정한 다음 **저장**을 선택합니다.

1. 이제 모든 리소스를 보고 디렉터리의 모든 구독 또는 관리 그룹에 대한 액세스 권한을 할당할 수 있으므로 자신에게 Azure 구독에 대한 소유자 역할을 할당합니다.
    1. 페이지 상단의 파란색 배너에서 **Microsoft Azure**를 선택하여 Azure Portal의 방문 페이지로 돌아갑니다.
    1. **구독**을 선택한 다음 **Woodgrove - GTP 데모(외부/후원)** 에 나열된 구독을 선택합니다.
    1. **액세스 제어(IAM)** 를 선택합니다.
    1. **추가**를 선택한 다음 **역할 할당 추가**를 선택합니다.
    1. 역할 탭에서 **권한이 있는 관리자 역할**을 선택합니다.
    1. **소유자**를 선택한 다음, **다음**을 선택합니다.
    1. **+ 구성원 선택**을 선택합니다.
    1. Avery Howard는 이 목록의 첫 번째 이름이며, 이름 오른쪽에 있는 **+** 을(를) 선택합니다.  이제 Avery Howard가 선택된 구성원 아래에 나열됩니다. **선택** 단추를 선택한 다음, **다음**을 선택합니다.
    1. **사용자가 권한 있는 관리자 역할, 소유자, UAA, RBAC를 제외한 모든 역할을 할당하도록 허용(권장)** 을 선택합니다.
    1. **검토 + 할당**을 선택한 다음, 마지막으로 **검토 + 할당**을 선택합니다.

Azure 구독의 소유자로서 이제 Copilot 내에서 용량을 프로비전할 수 있습니다.

#### 하위 작업 1: 용량 프로비전

이 작업에서는 조직의 용량을 프로비전하는 단계를 수행합니다. 용량 프로비전에는 두 가지 옵션이 있습니다.

- Security Copilot 내 용량 프로비전(권장)
- Azure를 통해 용량 프로비전

이 연습에서는 Security Copilot을 ​​통해 용량을 프로비전합니다. Security Copilot을 ​​처음 열면 마법사가 조직의 용량 설정 단계를 안내합니다.

1. 다음 링크를 선택하여 시뮬레이션 환경을 엽니다. **[Microsoft Security Copilot](https://app.highlights.guide/start/6373500f-1f10-4584-a14e-ca0b4aa7399f?link=0&token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)**.

1. 마법사의 단계에 따라 **시작**을 선택합니다.
1. 이 페이지에서 보안 용량을 설정합니다. 아래 나열된 필드에 대해 정보 아이콘을 선택하면 자세한 내용을 확인할 수 있습니다.
    1. Azure 구독: 드롭다운에서 **Woodgrove - GTP 데모(외부/후원)** 를 선택합니다.
    1. 리소스 그룹: 드롭다운에서 **RG-1**을 선택합니다.
    1. 용량 이름: 용량 이름을 입력합니다.
    1. 프롬프트 평가 위치 [지역]: 드롭다운에서 지역을 선택합니다.
    1. "이 위치에 트래픽이 너무 많은 경우 Copilot이 전 세계 어디에서나 프롬프트를 평가하도록 허용(최적의 성능을 위해 권장됨)" 옵션을 선택할지 여부를 선택할 수 있습니다.
    1. 용량 지역은 선택한 위치를 기준으로 설정됩니다.
    1. 보안 컴퓨팅: 이 필드는 최소 필수 SCU 단위인 1로 자동으로 채워집니다. 필드를 **1** 값으로 둡니다.
    1. **"사용 약관을 읽고 이해했으며 이에 동의합니다** 상자를 선택합니다.
    1. 페이지 오른쪽 하단에서 **계속**을 선택합니다.

1. 마법사는 고객 데이터가 저장될 위치에 대한 정보를 표시합니다. 표시되는 지역은 프롬프트 평가 필드에서 선택한 지역을 기반으로 합니다. **계속**을 선택합니다.

1. Copilot을 개선하는 데 도움이 되는 옵션을 선택할 수 있습니다. 기본 설정에 따라 토글을 선택할 수 있습니다.  **계속**을 선택합니다.

1. 초기 설정의 일환으로 Copilot은 기본적으로 모든 사용자에게 기여자 액세스 권한을 제공하고 전역 관리자 및 보안 관리자를 Copilot 소유자로 포함합니다. 프로덕션 환경에서 초기 설정을 완료한 후 Copilot에 액세스할 수 있는 사용자를 변경할 수 있습니다. **계속**을 선택합니다.
1. 모두 설정되었습니다! **마침**을 선택합니다.
1. 다음 연습에서는 랩 환경에 대한 별도의 링크를 사용하므로 브라우저 탭을 닫습니다.

### 작업 2: Microsoft Security Copilot 독립 실행형 환경 살펴보기

조직의 보안 관리자가 Copilot을 프로비전했습니다. 관리자가 팀의 선임 분석가를 Copilot 소유자로 추가하고 솔루션에 익숙해지도록 요청했습니다.

이 연습에서는 Microsoft Security Copilot 독립 실행형 환경의 랜딩 페이지에서 모든 주요 랜드마크를 살펴봅니다.

Avery Howard로 로그인했으며 Copilot 소유자 역할이 있습니다. Microsoft Security Copilot의 독립 실행형 환경에서 작업하게 됩니다.

이 연습을 완료하는 데 약 **15**분 정도 소요됩니다.

#### 하위 작업 1: 메뉴 옵션 살펴보기

이 작업에서는 홈 메뉴에서 탐색을 시작합니다.

1. 다음 링크를 선택하여 시뮬레이션 환경을 엽니다. **[Microsoft Security Copilot](https://app.highlights.guide/start/2cac767e-42c4-4058-afbb-a9413aac461d?link=0&token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)**.

1. 햄버거 아이콘이라고도 하는 **메뉴** 아이콘![홈 메뉴 아이콘](../media/home-menu-icon.png)을 선택합니다.

1. **내 세션**을 선택하고 사용 가능한 옵션을 확인합니다.
    1. 최근 세션을 보려면 최근 선택
    1. 필터를 선택하고 사용 가능한 옵션을 확인한 다음 파일러를 닫습니다.
    1. 홈 메뉴 아이콘을 선택하여 홈 메뉴를 엽니다.

1. **프롬프트북 라이브러리**를 선택합니다.
    1. 내 프롬프트북을 선택합니다. 후속 작업에서는 프롬프트북에 대해 더 자세히 알아봅니다.
    1. Woodgrove를 선택합니다.
    1. Microsoft를 선택합니다.
    1. 필터를 선택하여 사용 가능한 옵션을 확인한 다음 X를 선택하여 닫습니다.
    1. 홈 메뉴 아이콘을 선택하여 홈 메뉴를 엽니다.

1. **소유자 설정**을 선택합니다. Copilot 소유자는 이러한 설정을 사용할 수 있습니다. Copilot 기여자는 이러한 메뉴 옵션에 액세스할 수 없습니다.
    1. Security Copilot 플러그 인의 경우 누가 자신의 사용자 지정 플러그 인을 추가하고 관리할 수 있는지 드롭다운을 선택하여 사용 가능한 옵션을 확인합니다.
    1. 사용 가능한 옵션을 보려면 조직의 모든 사용자를 위한 사용자 지정 플러그 인을 추가하고 관리할 수 있는 사용자에 대한 드롭다운을 선택합니다. 자신의 사용자 지정 플러그 인을 추가하고 관리할 수 있는 사용자가 소유자로만 설정된 경우 이 옵션은 회색으로 표시됩니다.
    1. "Security Copilot이 Microsoft 365 서비스의 데이터에 액세스할 수 있도록 허용" 옆의 정보 아이콘을 선택합니다.  Microsoft Purview 플러그 인을 사용하려면 이 설정을 사용하도록 설정해야 합니다. 이후 연습에서 이 설정을 사용하게 됩니다.
    1. 사용 가능한 옵션을 보려면 파일을 업로드할 수 있는 사용자에 대한 드롭다운을 선택합니다.
    1. 홈 메뉴 아이콘을 선택하여 홈 메뉴를 엽니다.

1. **역할 할당**을 선택합니다.
    1. 멤버 추가를 선택한 다음 닫습니다.
    1. 소유자를 확장합니다.
    1. 기여자를 확장합니다.
    1. 홈 메뉴 아이콘을 선택하여 홈 메뉴를 엽니다.

1. **사용 모니터링**을 선택합니다.
    1. 사용 가능한 옵션을 보려면 날짜 필터를 선택합니다.
    1. 홈 메뉴 아이콘을 선택하여 홈 메뉴를 엽니다.

1. **설정**을 선택합니다.
    1. 기본 설정을 선택합니다. 아래로 스크롤하여 사용 가능한 옵션을 확인합니다.
    1. 데이터 및 개인 정보 보호를 선택합니다.
    1. 정보를 선택합니다.
    1. X를 선택하여 기본 설정 창을 닫습니다.

1. 홈 메뉴 왼쪽 하단에서 **Woodgrove**라고 표시된 위치를 선택합니다.
    1. 이 옵션을 선택하면 테넌트가 표시됩니다. 이를 테넌트 전환기라고 합니다. 이 경우에는 Woodgrove가 사용 가능한 유일한 테넌트입니다.
    1. 방문 페이지로 돌아가려면 **홈**을 선택합니다.

#### 하위 작업 2: 최근 세션에 대한 액세스 살펴보기

방문 페이지 중앙에는 최근 세션을 나타내는 카드가 있습니다.

1. 가장 큰 카드는 마지막 세션입니다. 세션 카드의 제목을 선택하면 해당 세션으로 이동합니다.
1. **모든 세션 보기**를 선택하여 내 세션 페이지로 이동합니다.
1. 홈 메뉴 아이콘 옆에 있는 **Microsoft Copilot for Security**를 선택하여 방문 페이지로 돌아갑니다.

#### 하위 작업 3: 프롬프트북에 대한 액세스 살펴보기

Copilot 방문 페이지의 다음 섹션은 프롬프트북을 중심으로 진행됩니다. 방문 페이지에는 일부 Microsoft 보안 프롬프트북에 대한 타일이 표시됩니다. 여기에서는 프롬프트북과 프롬프트북 라이브러리에 대한 액세스를 살펴봅니다. 후속 연습에서는 프롬프트북 만들기 및 실행을 살펴봅니다.

1. "이 프롬프트북 시작"라고 표시된 오른쪽에는 Microsoft 보안 프롬프트북 타일을 스크롤할 수 있는 왼쪽 및 오른쪽 화살표 키가 있습니다. **오른쪽 화살표 >** 를 선택합니다.

1. 각 타일에는 프롬프트북 제목, 간략한 설명, 프롬프트 수, 실행 아이콘이 표시됩니다. 해당 프롬프트북을 열려면 프롬프트북 타일의 제목을 선택합니다. 예를 들어, **취약성 영향 평가**를 선택합니다.
    1. 선택한 프롬프트북 창에는 프롬프트북을 만든 사용자, 태그, 간략한 설명, 프롬프트북 실행에 필요한 입력 사항, 프롬프트 목록 등의 정보가 제공됩니다.
    2. 프롬프트북과 사용 가능한 옵션에 대한 정보를 참고합니다. 이 시뮬레이션에서는 새 세션을 시작할 수 없으며 후속 연습에서 시작하게 됩니다. 
    1. **X**를 선택하여 창을 닫습니다.

1. **프롬프트북 라이브러리 보기**를 선택합니다.
    1. 자신이 소유한 프롬프트북을 보려면 내 프롬프트북을 선택합니다.
    1. Woodgrove를 선택하여 가상 조직의 이름인 Woodgrove가 소유한 프롬프트북 목록을 봅니다.
    1. 기본 제공된 Microsoft 소유/개발 프롬프트북을 보려면 Microsoft를 선택합니다.
    1. 필터 아이콘을 선택합니다. 여기서 통합 문서에 할당된 태그를 기준으로 필터링할 수 있습니다. 새 필터 탭에서 X를 선택하여 필터 창을 닫습니다.
    1. 홈 메뉴 아이콘 옆에 있는 **Microsoft Copilot for Security**를 선택하여 방문 페이지로 돌아갑니다.

#### 하위 작업 4: 프롬프트 에서 프롬프트 및 소스 아이콘 살펴보기

페이지 하단 중앙에는 프롬프트 표시줄이 있습니다. 프롬프트 표시줄에는 이 작업에서 탐색할 프롬프트와 원본 아이콘이 포함되어 있습니다. 후속 연습에서는 프롬프트 표시줄에 직접 입력하게 됩니다.

1. 프롬프트 표시줄에서 프롬프트 아이콘을 선택하여 기본 제공된 프롬프트 또는 프롬프트북을 선택할 수 있습니다. **프롬프트 아이콘**![프롬프트 아이콘](../media/prompt-icon.png)을 선택합니다.
    1. **모든 프롬프트북 보기** 선택
        1. 사용 가능한 모든 프롬프트북을 보려면 스크롤합니다.
        1. 뒤로 돌아가려면 검색 창 옆에 있는 **뒤로 화살표**를 선택합니다.
    1. **모든 시스템 기능 보기**를 선택합니다. 목록에는 사용 가능한 모든 시스템 기능이 표시됩니다. 이러한 기능은 실제로 실행할 수 있는 프롬프트입니다. 많은 시스템 기능은 특정 플러그 인과 연결되어 있으므로 해당 플러그 인이 사용하도록 설정된 경우에만 나열됩니다.
        1. 사용 가능한 모든 프롬프트북을 보려면 스크롤합니다.
        1. 뒤로 돌아가려면 검색 창 옆에 있는 **뒤로 화살표**를 선택합니다.

1. **원본 아이콘**![원본 아이콘](../media/sources-icon.png)을 선택합니다.
    1. 원본 아이콘은 원본 관리 창을 엽니다. 여기에서 플러그 인이나 파일에 액세스할 수 있습니다. 기본적으로 **플러그 인** 탭이 선택되어 있습니다.
        1. 모든 플러그 인을 볼 것인지 볼 것인지 선택합니다(사용하도록 설정된 플러그 인(켜기) 또는 사용하지 않도록 설정된 플러그 인(끄기)).
        1. Microsoft, 타사 및 사용자 지정 플러그 인 목록을 확장/축소합니다.
        1. 일부 플러그 인에는 매개 변수 구성이 필요합니다. Microsoft Sentinel 플러그 인의 **설정** 단추를 선택하여 설정 창을 확인합니다. 설정 창을 닫으려면 **취소**를 선택합니다. 별도의 연습에서는 플러그 인을 구성합니다.
    1. 여전히 원본 관리 창에 있어야 합니다. **파일**을 선택합니다.
        1. 설명을 검토합니다.
        1. Copilot에서는 파일을 업로드하고 기술 자료로 사용할 수 있습니다. 후속 연습에서는 파일 업로드 작업을 수행하게 됩니다.
        1. **X** 선택하여 원본 관리 창을 닫습니다.

#### 하위 작업 5: 도움말 기능 살펴보기

창 오른쪽 하단에는 설명서에 쉽게 액세스하고 일반적인 문제에 대한 솔루션을 찾을 수 있는 도움말 아이콘이 있습니다. 적절한 역할 권한이 있는 경우 도움말 아이콘을 통해 Microsoft 지원 팀에 지원 사례를 제출할 수도 있습니다.

1. **도움말(?)** 아이콘을 선택합니다.
    1. **설명서**를 선택합니다. 이렇게 선택하면 Microsoft Security Copilot 설명서에 대한 새 브라우저 탭이 열립니다. Microsoft Security Copilot 브라우저 탭으로 돌아갑니다.
    1. **도움말**을 선택합니다.
        1. Security Copilot에 액세스할 수 있는 사람은 누구나 도움말 아이콘을 선택한 다음 도움말 탭을 선택하여 자가 진단 위젯에 액세스할 수 있습니다. 여기에서 문제에 대한 내용을 입력하여 일반적인 문제에 대한 솔루션을 찾을 수 있습니다.
        1. 서비스 지원 관리자 또는 헬프 데스크 관리자 역할의 최소 역할을 가진 사용자는 Microsoft 지원 팀에 지원 사례를 제출할 수 있습니다. 이 역할이 있으면 헤드셋 아이콘이 표시됩니다. 연락처 지원 페이지를 닫습니다.

### 작업 3: Microsoft Security Copilot 포함된 환경 살펴보기

이 연습에서는 Microsoft Defender XDR의 인시던트를 조사합니다. 조사의 일환으로 인시던트 요약, 디바이스 요약, 스크립트 분석 등을 포함하여 Microsoft Defender XDR의 Microsoft Copilot의 주요 기능을 살펴봅니다. 또한 조사를 독립 실행형 환경으로 전환하고 조사 세부 정보를 동료와 공유하는 방법으로 핀 보드를 사용합니다.

Avery Howard로 로그인했으며 Copilot 소유자 역할이 있습니다. Microsoft Defender XDR의 포함된 Copilot 기능에 액세스하려면 새 통합 보안 운영 플랫폼을 사용하여 Microsoft Defender에서 작업합니다. 연습이 끝날 무렵에는 Microsoft Security Copilot의 독립 실행형 환경으로 전환합니다.

이 연습을 완료하는 데 약 **30**분 정도 소요됩니다.

#### 하위 작업 1: 인시던트 요약 및 단계별 대응 살펴보기

1. 다음 링크를 선택하여 시뮬레이션 환경을 엽니다. **[Microsoft Defender 포털](https://app.highlights.guide/start/f4f590f6-8937-40f9-91ec-632de546ab98?token=40f793d4-2956-40a4-b11a-6b3d4f92557f&azure-portal=true)**.

1. Microsoft Defender 포털에서:
    1. **조사 및 응답**을 확장합니다.
    1. **인시던트 및 경고**를 확장합니다.
    1. **인시던트**를 선택합니다.

1. 목록에서 첫 번째 인시던트(**인시던트 ID: 30342** 손상된 자산에서 사람이 운영하는 랜섬웨어 공격이 시작됨(공격 중단))를 선택합니다.

1. 이는 복잡한 인시던트입니다. Defender XDR은 많은 정보를 제공하지만 72개의 경고로 인해 어디에 집중해야 할지 아는 것이 어려울 수 있습니다. 인시던트 페이지 오른쪽에서 Copilot은 사용자의 집중과 대응을 안내하는 데 도움이 되는 **인시던트 요약**을 자동으로 생성합니다. **더 보기**를 선택합니다.
    1. Copilot의 요약은 초기 액세스, 횡적 이동, 수집, 자격 증명 액세스 및 반출을 포함하여 이 인시던트가 어떻게 발전했는지 설명합니다. 이는 특정 디바이스를 식별하고 PsExec 도구가 실행 파일을 시작하는 데 사용되었음을 나타냅니다.
    1. 이는 모두 추가 조사에 활용할 수 있는 항목입니다. 후속 작업에서 이들 중 일부를 살펴봅니다.

1. Copilot 패널에서 아래로 스크롤하면 요약 바로 아래에 **단계별 대응**이 있습니다. 단계별 대응에서는 심사, 포함, 조사 및 수정을 지원하는 작업을 권장합니다.
    1. 심사 범주의 첫 번째 항목은 이 인시던트를 심사하는 것입니다. 옵션을 보려면 **분류**를 선택합니다. 다른 범주의 단계별 대응을 검토합니다.
    1. 단계별 대응 섹션 상단에 있는 **상태** 단추를 선택하고 **완료됨**으로 필터링합니다. 두 가지 완료된 작업이 공격 중단으로 표시됩니다. 자동 공격 중단은 진행 중인 공격을 억제하고, 조직 자산에 대한 영향을 제한하며, 보안 팀이 공격을 완전히 수정할 수 있는 더 많은 시간을 제공하도록 설계되었습니다.
1. 인시던트 페이지를 열어 둡니다. 다음 작업에서 사용하게 됩니다.

#### 하위 작업 2: 디바이스 및 ID 요약 살펴보기

1. 인시던트 페이지에서 첫 번째 경고인 **의심스러운 URL이 클릭됨**을 선택합니다.

1. Copilot은 추가 분석을 위한 풍부한 정보를 제공하는 **경고 요약**을 자동으로 생성합니다. 예를 들어, 요약에서는 의심스러운 활동을 식별하고 데이터 수집 작업, 자격 증명 액세스, 맬웨어, 검색 작업 등을 식별합니다.

1. 페이지에는 많은 정보가 있으므로 이 경고를 자세히 보려면 ​​**경고 페이지 열기**를 선택합니다. 이는 경고 페이지의 세 번째 패널, 인시던트 그래프 옆의 경고 제목 아래에 있습니다.

1. 페이지 상단에는 parkcity-win10v 디바이스에 대한 카드가 있습니다. 타원을 선택하고 옵션을 확인합니다. **요약**을 선택합니다. Copilot은 **디바이스 요약**을 생성합니다. 디바이스 요약에 액세스할 수 있는 방법이 다양하다는 것은 아무 의미가 없으며, 이는 단지 하나의 편리한 방법일 뿐입니다. 요약에는 디바이스가 VM이고 디바이스 소유자를 식별하며 Intune 정책에 대한 준수 상태 등이 표시됩니다.

1. 디바이스 카드 옆에는 디바이스 소유자용 카드가 있습니다. **parkcity\jonaw**를 선택합니다. 페이지의 세 번째 패널은 경고 세부 정보 표시에서 Microsoft Entra ID 위험 및 내부 위험 심각도가 높음으로 분류된 계정 담당자인 Jonathan Wolcott 사용자에 대한 정보 제공으로 업데이트됩니다. Copilot 인시던트 및 경고 요약에서 배운 내용을 고려하면 이는 놀라운 일이 아닙니다. 줄임표를 선택한 다음 **요약**을 선택하면 Copilot에서 생성된 ID 요약을 가져올 수 있습니다.

1. 경고 페이지를 열어 둡니다. 다음 작업에서 사용하게 됩니다.

#### 하위 작업 3: 스크립트 분석 살펴보기

1. 경고 스토리에 집중해 보겠습니다 경고의 메인 패널에서 'partycity\jonaw'라는 카드 아래에 위치한 **최대화 ![최대화 아이콘](../media/maximize-icon.png)**을 선택하여 프로세스 트리를 더 잘 볼 수 있도록 합니다. 최대화된 보기에서 이 인시던트가 어떻게 발생했는지 더 명확하게 볼 수 있습니다. 많은 품목은 powershell.exe가 스크립트를 실행했음을 나타냅니다. 사용자 Jonathan Wolcott는 계정 관리자이므로, PowerShell 스크립트 실행은 이 사용자가 정기적으로 수행하는 작업이 아니라고 가정하는 것이 합리적입니다.

1. **powershell.exe 스크립트 실행**의 첫 번째 인스턴스를 확장하면 4:57:11 AM의 타임스탬프가 표시됩니다. Copilot에는 스크립트를 분석하는 기능이 있습니다. **분석**을 선택합니다.
    1. Copilot은 스크립트 분석을 생성하고 피싱 시도이거나 웹 기반 익스플로잇을 전달하는 데 사용될 수 있음을 제안합니다.
    1. **코드 표시**를 선택합니다. 코드에는 변형된 URL이 표시됩니다.

1. powershell.exe가 스크립트를 실행했음을 나타내는 몇 가지 다른 항목이 있습니다. 타임스탬프가 5:00:47 AM인 **powershell.exe -EncodedCommand...** 라고 레이블이 지정된 품목을 확장합니다. 원본 스크립트는 Base 64로 인코딩되었지만 Defender가 이를 디코딩했습니다. 디코딩된 버전의 경우 **분석**을 선택합니다. 분석은 이 공격에 사용된 스크립트의 정교함을 강조 표시합니다.

1. **X**(Copilot 패널 왼쪽에 있는 X)를 선택하여 경고 내용 페이지를 닫습니다. 이제 이동 경로를 사용하여 인시던트로 돌아갑니다. **손상된 자산에서 사람이 운영하는 랜섬웨어 공격이 시작됨(공격 중단)** 를 선택합니다.

#### 하위 작업 4: 파일 분석 살펴보기

1. 인시던트 페이지로 돌아왔습니다. 경고 요약에서 Copilot은 'Kekeo' 맬웨어와 관련된 Rubeus.exe 파일을 식별했습니다. Defender XDR의 파일 분석 기능을 사용하여 가져올 수 있는 다른 인사이트를 확인할 수 있습니다. 파일에 액세스하는 방법에는 여러 가지가 있습니다. 페이지 상단에서 **증거 및 응답** 탭을 선택합니다.

1. 화면 왼쪽에서 **파일**을 선택합니다.
1. 목록에서 **Rubeus.exe**라는 엔터티가 있는 첫 번째 항목을 선택합니다.
1. 열린 창에서 **분석**을 선택합니다. Copilot이 요약을 생성합니다.
1. Copilot이 생성하는 자세한 파일 분석을 검토합니다.
1. 파일 분석 창을 닫습니다.

#### 하위 과제 5: 독립 실행형 환경으로 피벗하기

이 작업은 복잡하며 더 많은 선임 분석가의 참여가 필요합니다. 이 작업에서는 조사를 중심으로 다른 분석가가 조사를 시작할 수 있도록 Defender 인시던트 프롬프트북을 실행합니다. 핀 보드에 ​​응답을 고정하고 조사에 도움을 주기 위해 팀의 고급 멤버와 공유할 수 있는 이 조사에 대한 링크를 생성합니다.

1. 페이지 상단에서 **공격 사례** 탭을 선택하여 인시던트 페이지로 돌아갑니다.

1. Copilot의 인시던트 요약 옆에 있는 줄임표를 선택하고 **Copilot for Security에서 열기**를 선택합니다.

1. Copilot은 독립 실행형 환경에서 열리고 인시던트 요약을 표시합니다. 더 많은 프롬프트를 실행할 수도 있습니다. 이 경우 인시던트에 대한 프롬프트북을 실행합니다. **프롬프트 아이콘**![프롬프트 아이콘](../media/prompt-icon.png)을 선택합니다. 
    1. **모든 프롬프트북 보기**를 선택합니다.
    1. **Microsoft 365 Defender 인시던트 조사**를 선택합니다.
    1. 프롬프트북 페이지가 열리고 Defender Incident ID를 묻습니다. **30342**를 입력한 다음 **실행**을 선택합니다.
    1. 제공된 정보를 검토하세요. 독립 실행형 환경으로 전환하고 프롬프트북을 실행함으로써 조사에서 사용하도록 설정된 플러그 인을 기반으로 Defender XDR을 넘어 더 광범위한 보안 솔루션의 기능을 호출할 수 있습니다.

1. 핀 아이콘 옆의 **상자 아이콘 ![상자 아이콘](../media/box-icon.png)**을 선택하여 모든 프롬프트와 해당 응답을 선택한 다음 **핀 아이콘 ![핀 아이콘](../media/pin-icon.png)**을 선택하여 해당 응답을 핀 보드에 저장합니다.

1. 핀 보드가 자동으로 열립니다. 핀 보드에는 저장된 프롬프트와 응답이 각각의 요약과 함께 보관됩니다. **핀 보드 아이콘![핀 보드 아이콘](../media/pinboard-icon.png)**을 선택하여 핀 보드를 열고 닫을 수 있습니다.

1. 페이지 상단에서 **공유**를 선택하여 옵션을 확인합니다. 링크나 이메일을 통해 인시던트를 공유하면 Copilot 액세스 권한이 있는 조직 내 사람들이 이 세션을 볼 수 있습니다. **X**를 선택하여 창을 닫습니다.

1. 이제 브라우저 탭을 닫아 시뮬레이션을 종료할 수 있습니다.

## 요약 및 추가 리소스

이 연습에서는 Microsoft Security Copilot의 첫 번째 실행 환경과 프로비전된 용량을 살펴보고 Copilot의 독립 실행형 및 포함된 환경을 탐색했습니다. Microsoft Defender XDR에서 인시던트를 조사하고 인시던트 요약, 디바이스 요약, 스크립트 분석 등을 탐색했습니다. 또한 조사를 독립 실행형 환경으로 피벗하고 핀 보드를 사용하여 동료와 조사 세부 정보를 공유했습니다.

추가 Microsoft Security Copilot 사용 사례 시뮬레이션을 실행하려면 [Microsoft Security Copilot 사용 사례 시뮬레이션 살펴보기](/training/modules/security-copilot-exercises/)로 이동합니다.