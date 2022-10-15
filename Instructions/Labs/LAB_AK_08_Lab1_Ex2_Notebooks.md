---
lab:
  title: 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-2---threat-hunting-using-notebooks-with-microsoft-sentinel"></a>모듈 8 - 랩 1 - 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅

## <a name="lab-scenario"></a>랩 시나리오



당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel Notebooks를 사용하는 위협 헌팅의 이점을 파악해야 합니다. Notebook을 사용하여 다음을 수행할 수 있습니다.

- 일부 Python 기계 학습 기능과 같이 Microsoft Sentinel에서 기본 제공되지 않는 분석을 수행합니다.
- 사용자 지정 타임라인 및 프로세스 트리와 같이 Microsoft Sentinel에서 기본 제공되지 않는 데이터 시각화를 만듭니다.
- Microsoft Sentinel 외부의 데이터 원본(예: 온-프레미스 데이터 세트)을 통합합니다.


### <a name="task-1-explore-notebooks"></a>작업 1: Notebooks 살펴보기

이 작업에서는 Microsoft Sentinel에서 Notebooks를 사용하는 방법을 살펴봅니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel 작업 영역을 선택합니다.

1. Microsoft Sentinel 작업 영역에서 **Notebooks**를 선택합니다.

1. 다음으로, AzureML 작업 영역을 만들어야 합니다. **Azure Machine Learning 구성**을 선택한 다음, 명령 모음에서 **새 Azure ML 작업 영역 만들기** 단추를 선택합니다.

1. 구독 상자에서 구독을 선택합니다.

1. 리소스 그룹에 대해 **새로 만들기**를 선택하고, 이름에 *RG-MachineLearning*을 입력하고, **확인**을 선택합니다. 

1. 작업 영역 정보 섹션에서 다음 작업을 수행합니다.

     - 작업 영역에 고유한 이름을 지정합니다.
     - 지역 기본값으로 **미국 동부**를 그대로 둡니다.
     - 기본 스토리지 계정, 키 자격 증명 모음 및 애플리케이션 인사이트 정보는 그대로 유지합니다.
     - Container Registry 옵션은 **없음**으로 유지하면 됩니다.

1. 페이지의 아래쪽에서 **검토 + 생성**를 선택합니다. “유효성 검사 통과” 메시지가 표시되면 **만들기**를 선택합니다. 

     >**참고:** Machine Learning 작업 영역을 배포하는 데 몇 분 정도 걸릴 수 있습니다.

1. 배포가 완료됨 메시지가 나타난 후 Microsoft Sentinel 포털로 돌아갑니다.

1. **Notebooks**를 선택한 다음, 가운데 명령 모음에서 **템플릿** 탭을 선택합니다. 

1. **Microsoft Sentinel ML Notebooks에 대한 시작 가이드**를 선택합니다. 

1. 오른쪽 창에서 아래로 스크롤하고 **템플릿에서 만들기** 단추를 선택합니다. 기본 옵션을 검토하고 **저장**을 선택합니다.

1. 저장이 완료되면 **Notebook 시작** 단추를 선택합니다. 그러면 Microsoft Azure Machine Learning Studio로 연결됩니다.

1. Microsoft Azure Machine Learning Studio에 정보 창이 나타나면 **닫기**를 선택합니다.

1. 명령 모음의 **Compute:** 인스턴스 선택기 오른쪽에 있는 **+** 기호를 선택하여 새 컴퓨팅 인스턴스를 만듭니다.

1. 컴퓨팅 이름 필드에 고유한 이름을 입력합니다. 그러면 컴퓨팅 인스턴스가 식별됩니다.

1. 아래로 스크롤하여 사용 가능한 첫 번째 옵션을 선택합니다. **힌트:** 워크로드 유형: Notebooks에서 개발 및 경량 테스트.

1. 화면 아래쪽에서 **만들기** 단추를 선택합니다. 표시할 수 있는 피드백 창을 닫습니다. 이 작업은 몇 분 정도 걸립니다. 완료되면 알림(벨 아이콘)이 표시됩니다.

1. 컴퓨팅이 만들어지고 실행되면 사용할 커널이 *Python 3.8 - AzureML*인지 확인합니다. **힌트:** 명령 모음의 오른쪽에 표시됩니다. *Notebooks* 메뉴에서 **<<** 을 선택하여 화면 크기를 늘릴 수도 있습니다.

1. 명령 모음에서 **지우개** 아이콘을 선택하여 Notebook의 모든 결과를 지우고 시작 자습서를 따릅니다.

>**참고:** 위 단계를 완료하여 Notebook에 액세스할 수 없는 경우에는 대신 GitHub 페이지에서 수행할 수 있습니다. 다음 페이지의 Notebook을 참조하세요. [GitHub의 Microsoft Sentinel Notebooks](https://github.com/Azure/Azure-Sentinel-Notebooks/blob/8122bca32387d60a8ee9c058ead9d3ab8f4d61e6/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## <a name="you-have-completed-the-lab"></a>이 랩을 완료했습니다.
