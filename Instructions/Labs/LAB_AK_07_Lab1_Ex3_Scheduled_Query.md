---
lab:
    title: '연습 3 - 예약된 쿼리 만들기'
    module: '모듈 7 - Microsoft Sentinel을 사용하여 검색 만들기 및 조사 수행'
---

# 모듈 7 - 랩 1 - 연습 3 - 예약된 쿼리 만들기


### 작업 1: 예약된 쿼리 만들기

이 작업에서는 예약된 쿼리를 만들고 이를 이전 연습에서 만든 Teams 채널에 연결합니다.

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용합니다.  

2. 랩 호스팅 공급자가 제공한 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

3. 랩 호스팅 공급자가 제공한 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

4. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

5. Microsoft Sentinel 작업 영역을 선택합니다.

6. 구성 영역에서 **분석**을 선택합니다.

7. **+ 만들기** 단추를 선택하고 **예약된 쿼리 규칙**을 선택합니다.

8. Analytics 규칙 마법사의 일반 탭에서 이름으로 *Azure AD 역할 할당 감사 내역*을 입력합니다.

9. 전술로는 **지속성**을 선택합니다.

10. 심각도로는 **낮음**을 선택합니다.

11. **다음: 규칙 논리 설정 >** 단추를 선택합니다.

12. 규칙 쿼리에 다음 KQL 문을 붙여넣습니다.

    >**경고:** 가상 머신에 붙여넣기 기능을 사용할 때는 추가 (파이프) 문자를 추가할 수 없습니다. 먼저 메모장에 다음 쿼리를 붙여 넣으세요.

```KQL
AuditLogs 
| where isnotempty(InitiatedBy.user.userPrincipalName) and Result == 'success' and OperationName contains "member to role" and AADOperationType startswith "Assign"
| extend InitiatedByUPN = tostring(InitiatedBy.user.userPrincipalName)
| extend InitiatedFromIP = iff(tostring(AdditionalDetails.[7].value) == '', tostring(AdditionalDetails.[6].value), tostring(AdditionalDetails.[7].value))
| extend TargetUser = tostring(TargetResources.[2].displayName)
| extend TargetRoleName = tostring(TargetResources.[0].displayName)
| project TimeGenerated, InitiatedByUPN, InitiatedFromIP, TargetUser, TargetRoleName, AADOperationType, OperationName
```

>**참고:** "쿼리 결과 보기" 링크를 선택하면 결과나 오류가 반환되지 않아야 합니다. 오류가 반환될 경우 쿼리가 이전 KQL 문과 같은지 검토하세요.

13. 다시 "Analytics 규칙 마법사 - 새 예약된 규칙 만들기" 블레이드의 *경고 보강(미리 보기)* 영역에서 *엔터티 매핑*을 선택하고 다음 값을 선택합니다. 

    - *엔터티 형식* 드롭다운 목록에서 **계정**을 선택합니다.
    - *ID* 드롭다운 목록에서 **전체_이름**을 선택합니다.
    - *값* 드롭다운 목록에서 **InitiatedByUPN**을 선택합니다.

    그런 다음 **새 엔터티 추가**를 선택하고 다음 값을 선택합니다.

    - *엔터티 형식* 드롭다운 목록에서 **IP**를 선택합니다.
    - *ID* 드롭다운 목록에서 **주소**를 선택합니다.
    - *값* 드롭다운 목록에서 **InitiatedByUPN**을 선택합니다.

14. *쿼리 예약*에서 다음 항목을 설정합니다.

    |설정|값|
    |---|---|
    |쿼리 실행 빈도|5분|
    |데이터를 확인할 기간|1일|

    >**참고:** 여기서는 같은 데이터에 대해 의도적으로 여러 인시던트를 생성합니다.  그러면 랩에서 해당 경고를 사용할 수 있기 때문입니다.

15. *경고 임계값* 영역의 옵션은 변경하지 않고 그대로 유지합니다.

    >**참고:** 모범 사례에 따라 경고 규칙 KQL 쿼리 문의 임계값을 관리해야 합니다.

16. *이벤트 그룹화* 영역에서 **모든 이벤트를 단일 경고로 그룹화** 옵션을 선택된 상태로 유지합니다.

17. **다음: 인시던트 설정 >** 단추를 클릭합니다.  

18. *인시던트 설정(미리 보기)* 탭에서 기본 옵션을 검토합니다.

19. **다음: 자동화된 응답 >** 단추를 클릭합니다.

20. *경고 자동화* 영역의 자동화된 응답 탭에서 이전 연습에서 만든 *PostMessageTeams-OnAlert* 플레이북을 선택합니다.

22. **다음: 검토 >** 단추를 선택합니다.
  
23. **만들기**를 선택합니다.


### 작업 2: 새 규칙 테스트

이 작업에서는 새 예약된 쿼리 규칙을 테스트합니다.

1. Azure Portal의 검색 창에 *Azure Active Directory*를 입력합니다. 그런 다음 **Azure Active Directory**를 선택합니다.

2. 관리 영역에서 **사용자**를 선택하여 "사용자 - 모든 사용자(미리 보기)" 페이지를 표시합니다.

3. 목록에서 사용자 **Christie Cline**을 선택하여 "Christie Cline - 프로필" 페이지를 표시합니다.

4. 관리 영역에서 **할당된 역할**을 선택하여 "Christie Cline - 할당된 역할" 페이지를 표시합니다.

5. 명령 모음에서 **+ 할당 추가**를 선택합니다.

6. *할당 추가* 페이지 *구성원* 탭의 *역할 선택* 아래에서 **사용자 관리자**를 선택하고 **다음 >** 을 선택합니다.

7. *설정 탭에서 기본*할당 유형*을* 검토하고 **할당**을 선택합니다. 할당 완료에 실패한 경우 다시 시도하세요.

8. 오른쪽 위에서 'x'를 두 번 선택하여 "Christie Cline - 할당된 역할" 및 "사용자 - 모든 사용자(미리 보기)" 페이지를 닫습니다.

9. "Contoso - 개요" 페이지의 *모니터링*에서 **감사 로그**를 선택합니다.

10. **데이터 설정 내보내기**를 선택하여 Sentinel에서 "Azure Active Directory" 데이터 커넥터가 올바르게 설정되었는지 확인합니다.

11. 앞에서 Sentinel에 대해 만든 *Log Analytics 작업 영역*에 대한 *진단 설정* 항목이 있는지 검토합니다.

12. 오른쪽 위에서 'x'를 선택하여 페이지를 닫습니다.

13. *범주: RoleManagement*에 대한 항목이 표시될 때까지**새로 고침**을 선택합니다. 이는 앞에서 수행한 역할 변경을 나타냅니다.

14. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

15. Microsoft Sentinel 작업 영역을 선택합니다.

16. **인시던트** 메뉴 옵션을 선택합니다.

    >**참고:** 트리거된 경고를 처리하는 데 5분 정도 걸릴 수 있습니다. 다음 연습을 계속 진행하다가 나중에 이 지점으로 돌아와도 됩니다. 인시던트 페이지를 자동으로 업데이트하려면 **인시던트 자동 새로 고침** 토글을 선택합니다.

17. 새로 만든 인시던트가 표시됩니다. 인시던트를 선택하고 오른쪽 블레이드의 정보를 검토합니다.

18. 브라우저 탭을 열고 https://teams.microsoft.com 로 이동하여 Microsoft Teams를 엽니다. *SOC* 팀으로 이동하여 인시던트에 대한 메시지가 게시되었는지 확인합니다.

## 연습 4 계속 진행
