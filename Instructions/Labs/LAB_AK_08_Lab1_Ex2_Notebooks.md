---
lab:
  title: 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅
  module: Learning Path 8 - Perform threat hunting in Microsoft Sentinel
---

# 학습 경로 8 - 랩 1 - 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅

## 랩 시나리오

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel Notebooks를 사용하는 위협 헌팅의 이점을 파악해야 합니다. Notebook을 사용하여 다음을 수행할 수 있습니다.

- 일부 Python 기계 학습 기능과 같이 Microsoft Sentinel에서 기본 제공되지 않는 분석을 수행합니다.
- 사용자 지정 타임라인 및 프로세스 트리와 같이 Microsoft Sentinel에서 기본 제공되지 않는 데이터 시각화를 만듭니다.
- Microsoft Sentinel 외부의 데이터 원본(예: 온-프레미스 데이터 세트)을 통합합니다.

>**참고:** **[대화형 랩 시뮬레이션](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Hunt%20for%20threats%20using%20notebooks%20in%20Microsoft%20Sentinel)** 을 사용하여 이 랩을 원하는 속도로 클릭할 수 있습니다. 대화형 시뮬레이션과 호스트된 랩 간에 약간의 차이가 있을 수 있지만 보여주는 핵심 개념과 아이디어는 동일합니다. 

### 작업 1: Notebook 탐색

이 작업에서는 Microsoft Sentinel에서 Notebooks를 사용하는 방법을 살펴봅니다.

1. 암호를 사용하여 관리 WIN1 가상 머신에 로그인합니다 **. Pa55w.rd**.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. **로그인 대화 상자에서** 랩 호스팅 공급자가 **제공한 테넌트 전자 메일** 계정을 복사하여 붙여넣은 다음을 선택합니다****.

1. **암호** 입력 대화 상자에서 랩 호스팅 공급자가 **제공한 테넌트 암호를** 복사하여 붙여넣은 다음, 로그인을** 선택합니다**.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. Microsoft Sentinel 작업 영역에서 위협 관리* 영역에서 Notebook을 *** 선택합니다**.

1. 다음으로, AzureML 작업 영역을 만들어야 합니다. **Azure Machine Learning 구성**을 선택한 다음, 명령 모음에서 **새 Azure ML 작업 영역 만들기** 단추를 선택합니다.

1. 구독 상자에서 구독을 선택합니다.

1. 리소스 그룹에 대해 **새로 만들기**를 선택하고, 이름에 *RG-MachineLearning*을 입력하고, **확인**을 선택합니다. 

1. 작업 영역 세부 정보 섹션에서 다음을 수행합니다.

     - 작업 영역에 고유한 이름을 지정합니다.
     - 미국** 동부를 지역의* 기본값*으로 둡**니다.
     - 기본 Storage 계정, Key Vault 및 Application Insights 정보를 유지합니다.
     - 컨테이너 레지스트리 옵션은 None**으로 **다시 기본 수 있습니다.

1. 페이지의 아래쪽에서 **검토 + 생성**를 선택합니다. "유효성 검사 통과" 메시지가 표시*되면 만들기**를 선택합니다**.* 

     >**참고:** Machine Learning 작업 영역을 배포하는 데 몇 분 정도 걸릴 수 있습니다.

1. *배포가 완료*된 후 메시지가 나타나면 Microsoft Sentinel 포털로 돌아갑니다.

1. 전자 필기장을 다시 선택한 **다음 가운데 명령 모음에서 서식 파일** 탭을 선택합니다**.** 

1. **Microsoft Sentinel ML Notebooks에 대한 시작 가이드**를 선택합니다. 

1. 오른쪽 창에서 아래로 스크롤하고 **템플릿에서 만들기** 단추를 선택합니다. 기본 옵션을 검토한 다음 저장**을 선택합니다**.

1. 저장이 완료되면 **Notebook 시작** 단추를 선택합니다. 그러면 Microsoft Azure Machine Learning Studio로 연결됩니다.

1. Microsoft Azure Machine Learning Studio에 정보 창이 나타나면 **닫기**를 선택합니다.

1. 명령 모음의 Compute 인스턴스 오른쪽에** 있는 **선택기에서 기호를 **+** 선택하여 새 컴퓨팅 인스턴스를 만듭니다. **힌트:** 줄임표 아이콘 **(...)** 내부에 숨겨져 있을 수 있습니다.

     >**참고:** 왼쪽 위에 있는 3줄과 아이콘을 선택하는 Notebooks 파일을 **<<** 선택하여 Azure ML Studio 왼쪽 블레이드를 숨김으로써 더 많은 화면 공간을 가질 수 있습니다.

1. 컴퓨팅 이름 필드에 고유한 이름을 ** 입력합니다. 그러면 컴퓨팅 인스턴스가 식별됩니다.

1. 아래로 스크롤하여 사용 가능한 첫 번째 옵션을 선택합니다. **힌트:** 워크로드 유형: Notebook 개발 및 경량 테스트.

1. 화면 아래에서 **만들기** 단추를 선택합니다. 표시할 수 있는 피드백 창을 닫습니다. 이 작업을 완료하면 알림(벨 아이콘)이 표시되고 *컴퓨팅 인스턴스* 왼쪽 아이콘이 파란색에서 녹색으로 바뀝니다.

1. 컴퓨팅이 만들어지고 실행되면 사용할 커널이 *Python 3.8 - AzureML*인지 확인합니다. **힌트:** 명령 모음의 오른쪽에 표시됩니다.

1. **인증** 단추를 선택하고 인증이 완료되기를 기다립니다.

1. 명령 모음에서 모든 출력** 지우기를 선택하여 **Notebook의 모든 결과를 지우고 시작* 자습서를 *따릅니다. **힌트:** 명령 모음에서 줄임표(...)를 선택하여 찾을 수 있습니다.

>**참고:** Notebook에 액세스하기 위해 위의 단계를 완료할 수 없는 경우 대신 GitHub 뷰워 페이지에서 이를 따를 수 있습니다. [Azure ML Notebook 및 Microsoft Sentinel 시작](https://nbviewer.org/github/Azure/Azure-Sentinel-Notebooks/blob/master/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## 랩을 완료했습니다.
