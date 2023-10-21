# 모듈 6 Microsoft Sentinel을 사용하여 탐지 만들기 및 조사 수행

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## AMA(Azure Monitor 에이전트)로 구성된 공격 감지 Windows

이 작업에서는 

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자용 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자용 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 에서 `Microsoft Sentinel`메뉴 섹션으로 `Threat management` 이동하여 **인시던트** 선택

1. 만든 규칙에서 구성한 과 `Title` 일치하는 `Severity` 인시던트가 `NRT` 표시됩니다.

1. 를 `Incident` 선택하면 창이 `detail` 열립니다.

1. 할당은 `Owner` 에서 만든 `Automation rule`**Operator1**이어야 하며 `Tactics and techniques` 는 규칙에서 `NRT` **권한 에스컬레이션**이어야 합니다.

1. **전체 세부 정보 보기를** 선택하여 모든 `Incident management` 기능을 확인하고`Incident actions`

## 데모를 완료했습니다.
