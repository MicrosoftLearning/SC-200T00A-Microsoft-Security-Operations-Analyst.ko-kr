---
lab:
  title: 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-2---threat-hunting-using-notebooks-with-microsoft-sentinel"></a>모듈 8 - 랩 1 - 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅

## <a name="lab-scenario"></a>랩 시나리오



You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You need to explore the benefits of threat hunting with Microsoft Sentinel Notebooks. You can use notebooks to:

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

1. Next, you need to create an AzureML Workspace. Select <bpt id="p1">**</bpt>Configure Azure Machine Learning<ept id="p1">**</ept> and then select <bpt id="p2">**</bpt>Create new Azure ML workspace<ept id="p2">**</ept> button in the command bar.

1. 구독 상자에서 구독을 선택합니다.

1. 리소스 그룹에 대해 **새로 만들기**를 선택하고, 이름에 *RG-MachineLearning*을 입력하고, **확인**을 선택합니다. 

1. 작업 영역 정보 섹션에서 다음 작업을 수행합니다.

     - 작업 영역에 고유한 이름을 지정합니다.
     - 지역 기본값으로 **미국 동부**를 그대로 둡니다.
     - 기본 스토리지 계정, 키 자격 증명 모음 및 애플리케이션 인사이트 정보는 그대로 유지합니다.
     - Container Registry 옵션은 **없음**으로 유지하면 됩니다.

1. At the bottom of the page, select <bpt id="p1">**</bpt>Review + create<ept id="p1">**</ept>. When you see the <bpt id="p1">*</bpt>"Validation passed"<ept id="p1">*</ept> message, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>. 

     >**참고:** Machine Learning 작업 영역을 배포하는 데 몇 분 정도 걸릴 수 있습니다.

1. 배포가 완료됨 메시지가 나타난 후 Microsoft Sentinel 포털로 돌아갑니다.

1. **Notebooks**를 선택한 다음, 가운데 명령 모음에서 **템플릿** 탭을 선택합니다. 

1. **Microsoft Sentinel ML Notebooks에 대한 시작 가이드**를 선택합니다. 

1. On the right pane, scroll down and select <bpt id="p1">**</bpt>Create from template<ept id="p1">**</ept> button. Review the default option and select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.

1. 당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다.

1. Microsoft Azure Machine Learning Studio에 정보 창이 나타나면 **닫기**를 선택합니다.

1. 명령 모음의 **Compute:** 인스턴스 선택기 오른쪽에 있는 **+** 기호를 선택하여 새 컴퓨팅 인스턴스를 만듭니다.

1. Microsoft Sentinel Notebooks를 사용하는 위협 헌팅의 이점을 파악해야 합니다.

1. Notebook을 사용하여 다음을 수행할 수 있습니다.

1. Select the <bpt id="p1">**</bpt>Create<ept id="p1">**</ept> button at the bottom of the screen. Close any feedback window that may appear. This will take a few minutes, you will see a notification (bell icon) when it is done.

1. Once the Compute has been created and running, verify that the kernel to use is <bpt id="p1">*</bpt>Python 3.8 - AzureML<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> This is shown in the right of the command bar. You can also increase your screen size by selecting <bpt id="p1">**</bpt><ph id="ph1">&lt;&lt;</ph><ept id="p1">**</ept> under the <bpt id="p2">*</bpt>Notebooks<ept id="p2">*</ept> menu.

1. 명령 모음에서 **지우개** 아이콘을 선택하여 Notebook의 모든 결과를 지우고 시작 자습서를 따릅니다.

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you cannot complete the steps above to access the Notebook, you can follow it on its GitHub page instead. See the notebook file here: <bpt id="p1">[</bpt>Microsoft Sentinel Notebooks on GitHub<ept id="p1">](https://github.com/Azure/Azure-Sentinel-Notebooks/blob/8122bca32387d60a8ee9c058ead9d3ab8f4d61e6/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb)</ept> 

## <a name="you-have-completed-the-lab"></a>이 랩을 완료했습니다.
