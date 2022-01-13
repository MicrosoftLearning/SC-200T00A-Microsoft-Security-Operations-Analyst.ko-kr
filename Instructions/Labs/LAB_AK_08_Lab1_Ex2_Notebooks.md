---
lab:
    title: '연습 2 - Microsoft Sentinel을 통해 Notebooks를 사용하여 위협 헌팅 수행'
    module: '모듈 8 - Microsoft Sentinel에서 위협 헌팅 수행'
---

# 모듈 8 - 랩 1 - 연습 2 - Microsoft Sentinel을 통해 Notebooks를 사용하여 위협 헌팅 수행

## 랩 시나리오

여러분은 Microsoft Sentinel을 구현한 회사에서 일하는 보안 작업 분석가입니다. Microsoft Sentinel Notebooks를 사용하는 위협 헌팅의 이점을 파악해야 합니다.


### 작업 1: Notebooks 살펴보기

이 작업에서는 Microsoft Sentinel에서 Notebooks를 사용하는 방법을 살펴봅니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. Edge 브라우저에서 Azure Portal https://portal.azure.com 으로 이동합니다.

3. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

4. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

5. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

6. Microsoft Sentinel 작업 영역을 선택합니다.

7. Microsoft Sentinel 작업 영역에서 **Notebooks**를 선택합니다.

8. 다음으로, AzureML 작업 영역을 선택해야 합니다. **Azure Machine Learning 구성**을 선택하고 명령 모음에서 **새 Azure ML 작업 영역 만들기** 단추를 클릭합니다.

9. 구독 상자에서 구독을 선택합니다.

10. 리소스 그룹에서 **새로 만들기**를 선택하고 이름으로 *RG-MachineLearning*을 입력한 후 **확인**을 선택합니다. 

11.	작업 영역 정보 섹션에서 다음 작업을 수행합니다.

    - 작업 영역에 고유한 이름을 지정합니다.
    - 지역을 선택합니다(적절한 옵션이 기본값으로 선택되어 있음).
    - 기본 스토리지 계정, 키 자격 증명 모음 및 애플리케이션 인사이트 정보는 그대로 유지합니다.
    - Container Registry 옵션은 **없음**으로 유지하면 됩니다.

12.	페이지의 아래쪽에서 **검토 + 만들기**를 선택합니다. 그리고 다음 페이지에서 **만들기**를 선택합니다. 

    >**참고:** Machine Learning 작업 영역을 배포하는 데 몇 분 정도 걸릴 수 있습니다. 

13.	배포가 완료되면 Microsoft Sentinel 포털로 돌아갑니다.

14. **Notebook**, **템플릿** 탭을 차례로 선택합니다. 

15. **Microsoft Sentinel ML Notebook용 시작 가이드**를 선택한 다음 **Notebook 템플릿 복제** 단추를 선택합니다. Notebook 이름을 입력하라는 팝업이 표시되면 기본 이름을 사용하고 **저장**을 선택합니다.

16. **Notebook 시작** 단추를 선택합니다. Microsoft Azure Machine Learning Studio에 창이 표시되면 모두 닫습니다.

17.	화면 맨 위의 **컴퓨팅:** 인스턴스 선택기 옆에 있는 **+** 기호를 선택하여 **새 컴퓨팅** 화면을 표시합니다.

18.	지금은 랩 환경이므로 *컴퓨터 이름*에 고유한 이름을 입력하고 사용 가능한 첫 번째 컴퓨터를 선택합니다. **힌트:** 워크로드 유형: 개발

19.	화면 아래쪽에서 **만들기** 단추를 선택합니다. 피드백 창이 표시되면 모두 닫습니다. 이 작업은 몇 분 정도 걸립니다.

20.	컴퓨팅 인스턴스가 작성되어 실행되면 Notebook 오른쪽 위에서 사용할 커널이 *Python 3.8 - AzureML*인지 확인합니다.

21. 명령 모음에서 **지우개** 아이콘을 선택하여 Notebook에서 결과를 모두 지우고 시작 자습서를 따라 진행합니다.

>**참고** 위의 단계를 완료하여 Notebook에 액세스할 수 없는 경우에는 GitHub 페이지에서 Notebook을 확인할 수 있습니다.  다음 페이지의 Notebook을 참조하세요. [GitHub의 Azure Sentinal Notebooks](https://github.com/Azure/Azure-Sentinel-Notebooks/blob/8122bca32387d60a8ee9c058ead9d3ab8f4d61e6/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## 이 랩을 완료했습니다.
