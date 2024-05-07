---
lab:
  title: 연습 4 - 데이터 커넥터를 사용하여 Defender XDR을 Microsoft Sentinel에 연결
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# 학습 경로 6 - 랩 1 - 연습 4 - 데이터 커넥터를 사용하여 Defender XDR을 Microsoft Sentinel에 연결

## 랩 시나리오

![랩 개요입니다.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex4.png)

Microsoft Defender XDR과 Microsoft Sentinel을 모두 배포한 회사에서 근무하는 보안 운영 분석가라고 가정합니다. Microsoft Sentinel을 Defender XDR에 연결하는 통합 보안 운영 플랫폼을 준비해야 합니다. 다음 단계는 Defender XDR Content Hub 솔루션을 설치하고 Defender XDR 데이터 커넥터를 Microsoft Sentinel에 배포하는 것입니다.

### 작업 1: Defender XDR 연결

이 작업에서는 Microsoft Defender XDR 커넥터를 배포합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저에서(<https://portal.azure.com>)의 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

1. Microsoft Sentinel 왼쪽 메뉴에서 **콘텐츠 관리** 섹션까지 아래로 스크롤하고 **콘텐츠 허브**를 선택합니다.

1. *콘텐츠 허브*에서 **Microsoft Defender XDR** 솔루션을 검색하고 목록에서 선택합니다.

1. *Microsoft Defender XDR* 솔루션 세부 정보 페이지에서 **설치**를 선택합니다.

1. 설치가 완료되면 **Microsoft Defender XDR** 솔루션을 검색하여 선택합니다.

1. *Microsoft Defender XDR* 솔루션 세부 정보 페이지에서 **관리** 선택

>**참고:** *Microsoft Defender XDR* 솔루션은 *Microsoft Defender XDR* 데이터 커넥터, 헌팅 쿼리, Workbooks 및 분석 규칙을 설치합니다.

1. *Microsoft Defender XDR* 데이터 커넥터 확인란을 선택하고 **커넥터 페이지 열기**를 선택합니다.

1. *구성* 섹션의 *지침* 탭에서 다음 확인란을 **선택 해제**합니다. *이 제품에 대한 모든 Microsoft 인시던트 만들기 규칙을 해제합니다. 권장*. 그리고 **인시던트 및 경고 연결** 단추를 선택합니다.

1. 연결이 성공했다는 메시지가 표시됩니다.

## 이 랩을 완료했습니다.
