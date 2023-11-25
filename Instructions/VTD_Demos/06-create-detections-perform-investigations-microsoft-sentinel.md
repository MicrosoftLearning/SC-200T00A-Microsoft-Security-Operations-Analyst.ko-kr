# 모듈 6 Microsoft Sentinel을 사용하여 탐지 만들기 및 조사 수행

**참고** 이 데모의 성공적인 완료는 필수 구성 요소 문서의[ 모든 단계를 ](00-prerequisites.md)완료하는 데 따라 달라집니다. 

## AMA(Azure Monitor 에이전트)를 사용하여 구성된 공격 검색 Windows

이 작업에서는 

1. 암호를 사용하여 관리 WIN1 가상 머신에 로그인합니다 **. Pa55w.rd**.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. **로그인 대화 상자에서** 랩 호스팅 공급자가 **제공한 관리자의 테넌트 전자 메일** 계정을 복사하여 붙여넣은 다음, 다음**을 선택합니다**.

1. **암호** 입력 대화 상자에서 랩 호스팅 공급자가 **제공한 관리자의 테넌트 암호를** 복사하여 붙여넣은 다음, 로그인을** 선택합니다**.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. 에서 `Microsoft Sentinel`메뉴 섹션으로 `Threat management` 이동하여 인시던트 선택 ****

1. 만든 규칙에서 구성한 인시던트와 `Title` 일치하는 `Severity` 인시던트가 `NRT` 표시됩니다.

1. `Incident` 선택하고 창이 `detail` 열립니다.

1. 할당은 Operator1**이어야 **하며`Tactics and techniques`, 규칙에서 `NRT` `Automation rule`권한 에스컬레이션**이어야 **합니다.`Owner`

1. 전체 세부 정보** 보기를 선택하여 **모든 `Incident management` 기능을 확인하고`Incident actions`

## 데모를 완료했습니다.
