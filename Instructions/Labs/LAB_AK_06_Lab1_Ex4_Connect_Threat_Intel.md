---
lab:
    title: '연습 4 - 데이터 커넥터를 사용하여 Microsoft Sentinel에에 위협 인텔리전스 연결'
    module: '모듈 6 - Microsoft Sentinel에 로그 연결'
---

# 모듈 6 - 랩 1 - 연습 4 - 데이터 커넥터를 사용하여 Microsoft Sentinel에에 위협 인텔리전스 연결


### 작업 1: 위협 인텔리전스 연결

이 작업에서는 위협 인텔리전스 - TAXII 커넥터를 사용하여 위협 인텔리전스 공급자를 연결합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. Edge 브라우저에서 Azure Portal(https://portal.azure.com) 로 이동합니다.

3. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

4. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

5. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

6. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

7. 데이터 커넥터 탭에서 **위협 인텔리전스 - TAXII** 커넥터를 선택합니다.

8. 커넥터 정보 블레이드에서 **커넥터 페이지 열기**를 선택합니다.

9. 구성 영역에서 **식별 이름(서버용)** 으로는 *PhishURL*을 입력합니다.

10. API 루트 URL로는 https://limo.anomali.com/api/v1/taxii2/feeds/ 를 입력합니다.

11. 컬렉션 ID로는 **107**을 입력합니다.

12. 사용자 이름으로는 **guest**를 입력합니다.

13. 암호로는 **guest**를 입력합니다.

14. 이제 **추가** 단추를 선택합니다.  

    피싱 URL 끌어오기가 진행되며 ThreatIntelligenceIndicator 테이블에 피싱 URL이 입력됩니다.

>**참고:** 추가적인 컬렉션에 대해서는 브라우저에서 https://limo.anomali.com/api/v1/taxii2/feeds/collections/ 를 열고, 사용자 이름과 암호로 guest를 사용하여 사용 가능한 다른 컬렉션 ID를 검토합니다.

## 이 랩을 완료했습니다.
