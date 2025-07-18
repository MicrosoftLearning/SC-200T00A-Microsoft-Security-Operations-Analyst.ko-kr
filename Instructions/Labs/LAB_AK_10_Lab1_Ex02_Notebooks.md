---
lab:
  title: 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅
  module: Learning Path 10 - Perform threat hunting in Microsoft Sentinel
---

# 학습 경로 10 - 랩 1 - 연습 2 - Microsoft Sentinel이 설치된 Notebooks를 사용하여 위협 헌팅

## 랩 시나리오

당신은 Microsoft Sentinel을 구현한 회사에서 근무하는 보안 운영 분석가입니다. Microsoft Sentinel Notebooks를 사용하는 위협 헌팅의 이점을 파악해야 합니다. Notebook을 사용하여 다음을 수행할 수 있습니다.

- 일부 Python 기계 학습 기능과 같이 Microsoft Sentinel에서 기본 제공되지 않는 분석을 수행합니다.
- 사용자 지정 타임라인 및 프로세스 트리와 같이 Microsoft Sentinel에서 기본 제공되지 않는 데이터 시각화를 만듭니다.
- Microsoft Sentinel 외부의 데이터 원본(예: 온-프레미스 데이터 세트)을 통합합니다.

>**중요:** 학습 경로 #10의 랩은 *독립 실행형* 환경으로 되어 있습니다. 완료하기 전에 랩을 종료하면 구성을 다시 실행해야 합니다.

### 이 랩의 예상 완료 시간은 30분입니다.

### 작업 1: Notebooks 살펴보기

이 작업에서는 Microsoft Sentinel에서 Notebooks를 사용하는 방법을 살펴봅니다.

>**참고:** Microsoft Sentinel이 Azure 구독에 **defenderWorkspace**라는 이름으로 사전 배포되었으며 필요한 *콘텐츠 허브* 솔루션이 설치되어 있습니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

1. Microsoft Edge 브라우저에서 <https://portal.azure.com>의 Azure Portal로 이동합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여 넣은 후 **다음**을 선택합니다.

1. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여 넣은 후 **로그인**을 선택합니다.

1. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

1. Microsoft Sentinel **defenderWorkspace**을 선택합니다.

1. Microsoft Sentinel 작업 영역의 *위협 관리* 영역에서 **Notebooks**을 선택합니다.

1. 다음으로, Azure Machine Learning 작업 영역을 만들어야 합니다. **Azure Machine Learning 구성**을 선택한 다음, 명령 모음에서 **새 Azure ML 작업 영역 만들기** 단추를 선택합니다.

1. 구독 상자에서 구독을 선택합니다.

1. 리소스 그룹에 대해 **새로 만들기**를 선택하고, 이름에 *RG-MachineLearning*을 입력하고, **확인**을 선택합니다. 

1. 작업 영역 정보 섹션에서 다음 작업을 수행합니다.

     - 작업 영역에 고유한 이름을 지정합니다.
     - 지역 기본값으로 **미국 동부**를 그대로 둡니다.**
     - 기본 스토리지 계정, 키 자격 증명 모음 및 애플리케이션 인사이트 정보는 그대로 유지합니다.
     - Container Registry 옵션은 **없음**으로 유지하면 됩니다.

1. 페이지의 아래쪽에서 **검토 + 생성**를 선택합니다. “유효성 검사 통과” 메시지가 표시되면 **만들기**를 선택합니다.** 

     >**참고:** Machine Learning 작업 영역을 배포하는 데 몇 분 정도 걸릴 수 있습니다.

1. 배포가 완료됨 메시지가 나타난 후 Microsoft Sentinel 포털로 돌아갑니다.**

1. 다시 **Notebooks**을 선택한 다음 가운데 명령 모음에서 **템플릿** 탭을 선택합니다. 

1. **Microsoft Sentinel ML Notebooks에 대한 시작 가이드**를 선택합니다.

1. 오른쪽 창에서 아래로 스크롤하고 **템플릿에서 만들기** 단추를 선택합니다. 기본 옵션을 검토한 다음 **저장**을 선택합니다.

1. 저장이 완료되면 **Notebook 시작** 단추를 선택합니다. 그러면 Microsoft Azure Machine Learning Studio로 연결됩니다.

1. Microsoft Azure Machine Learning Studio에 정보 창이 나타나면 **닫기**를 선택합니다.

1. 명령 모음의 **컴퓨팅:** 선택기 오른쪽에 있는 **+** 기호를 선택하여 *Azure ML 컴퓨팅* 인스턴스를 만듭니다. **힌트:** 줄임표 아이콘 **(...)** 안에 숨겨져 있을 수 있습니다.

     >**참고:** *햄버거 메뉴*(왼쪽 위에 있는 3개의 가로줄)을 선택하고 **<<** 아이콘을 선택하여 Notebooks 파일을 축소하여 Azure ML Studio 왼쪽 블레이드를 숨김으로써 더 많은 화면 공간을 확보할 수 있습니다.

1. 컴퓨팅 이름 필드에 고유한 이름을 입력합니다.** 컴퓨팅 인스턴스를 식별합니다.

1. 아래로 스크롤하여 사용 가능한 첫 번째 옵션을 선택합니다. **힌트:** 워크로드 유형: Notebook(또는 다른 IDE)에서 개발 및 경량화 테스트.

1. 화면 아래쪽에서 **검토 + 만들기** 단추를 선택한 다음 아래로 스크롤하여 **만들기**를 선택합니다. 표시할 수 있는 피드백 창을 닫습니다. 이 작업은 몇 분 정도 소요됩니다. 완료되면 알림(종 모양 아이콘)이 표시되고 *컴퓨팅 인스턴스* 왼쪽 아이콘이 파란색에서 녹색으로 변합니다.

1. 컴퓨팅이 만들어지고 실행되면 사용할 커널이 *Python 3.10 - Pytorch 및 Tensorflow*인지 확인합니다. **힌트:** 명령 모음의 오른쪽에 표시됩니다.

1. **인증** 단추를 선택하고 인증이 완료되기를 기다립니다.

1. 명령 모음에서 **모든 출력 지우기**(지우기 아이콘)를 선택하여 Notebook의 모든 결과를 지우고 *시작* 자습서를 따릅니다. **힌트:** 명령 모음에서 줄임표(...)를 선택하여 찾을 수 있습니다.

1. Notebook에서 섹션 *1 소개*를 검토하고 *2 Notebook 및 MSTICPy 초기화* 섹션으로 진행합니다.

1. *2 Notebook 및 MSTICPy 초기화* 섹션에서 Notebook을 초기화하고 MSTICPy 패키지를 설치하는 내용을 검토합니다.

1. 코드 왼쪽에 있는 **셀 실행** 버튼(재생 아이콘)을 선택하여 *Python 코드*를 실행하여 셀을 초기화합니다.

1. 실행하는 데 약 15초가 걸립니다. 완료되면 출력 메시지를 검토하고 Python 커널 버전에 대한 경고를 무시합니다. 왼쪽의 *파일 탐색기* 창에 있는 *유틸리티* 폴더에 *msticpyconfig.yaml*을 만든 경우 코드가 성공적으로 실행되었습니다. 파일이 표시되려면 30초 정도 더 걸릴 수 있습니다.

    >**힌트:** *출력 메뉴*의 코드 창 왼쪽에서 줄임표(...)를 선택하고 *출력 지우기*(x*가 있는 사각형) 아이콘을 선택하면 출력 메시지를 지울 수 있습니다.

1. 왼쪽의 *파일 탐색기* 창에서 **msticpyconfig.yaml** 파일을 선택하여 파일 내용을 검토한 다음 닫습니다.

1. *3 MSTICPy로 데이터 쿼리* 섹션으로 이동하여 내용을 검토합니다. *여러 Microsoft Sentinel 작업 영역* 코드 셀은 실패하므로 실행하지 마세요. 다른 코드 셀은 성공적으로 실행할 수 있습니다.

>**참고:** 위의 단계를 완료하여 Notebook에 액세스할 수 없는 경우 대신 GitHub 뷰어 페이지에서 이를 따를 수 있습니다. [Azure ML Notebooks 및 Microsoft Sentinel 시작](https://nbviewer.org/github/Azure/Azure-Sentinel-Notebooks/blob/master/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## 이 랩을 완료했습니다.
