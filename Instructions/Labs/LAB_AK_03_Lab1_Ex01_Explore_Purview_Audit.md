---
lab:
  title: 연습 1 - Microsoft Purview 감사 로그 탐색
  module: Learning Path 3 - Mitigate threats using Microsoft Purview
---

# 학습 경로 3 - 랩 1 - 연습 1 - Microsoft Purview 감사 살펴보기

## 랩 시나리오

여러분은 Microsoft Defender XDR 및 Microsoft Purview를 구현하는 회사에서 근무하는 보안 운영 분석가입니다. Purview 감사(표준) 및 감사(프리미엄)를 모두 구성하여 IT 규정 준수 팀의 동료를 지원하고 있습니다. 이들의 목표는 환자 데이터에 대한 모든 액세스 및 수정 사항이 의료 데이터 보호 규정을 충족하도록 정확하게 기록되도록 하는 것입니다.

### 이 랩의 예상 완료 시간은 15분입니다.

### 작업 1: Purview 감사 로그 사용

이 작업에서는 Microsoft 365 보안 포털에서 EOP(Exchange Online Protection) 및 Office 365용 Microsoft Defender에 대해 미리 설정된 보안 정책을 할당합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. 새 Microsoft Edge 브라우저를 시작합니다.

1. Microsoft Edge 브라우저에서 Microsoft Defender XDR 포털(<https://security.microsoft.com>)로 이동합니다.

1. 랩 호스팅 공급자가 제공한 관리자 사용자 이름용 테넌트 전자 메일 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 관리자의 테넌트 암호를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. 탐색 메뉴에서 *운영 기술*을 확장하고 **추가 리소스**를 선택합니다.

1. **기타 리소스** 창에서 *Microsoft Purview 포털* 타일의 **열기** 단추를 선택합니다.

1. Microsoft Purview 포털이 열리면 *새 Microsoft Purview 포털*에 대한 메시지가 화면에 표시됩니다. 데이터 흐름 공개 약관 및 개인정보처리방침에 동의하는 옵션을 선택한 다음 **지금 사용**을 선택합니다.

    ![새 Microsoft Purview 포털의 시작 화면을 보여주는 스크린샷.](../Media/welcome-purview-portal.png)

1. 왼쪽 사이드바에서 **솔루션**을 선택한 다음 **감사**을 선택합니다.

1. **검색** 페이지에서 **사용자 및 관리자 활동 기록 시작** 표시줄을 선택하여 감사 로깅을 활성화합니다.

    ![사용자 및 관리자 활동 기록 시작 단추를 보여 주는 스크린샷.](../Media/enable-audit-button.png)

1. 이 옵션을 선택하면 이 페이지에서 파란색 표시줄이 사라집니다.

    >**참고:** 활동 기록을 시작하는 데 60분이 걸릴 수 있습니다.

## 이 랩을 완료했습니다.
