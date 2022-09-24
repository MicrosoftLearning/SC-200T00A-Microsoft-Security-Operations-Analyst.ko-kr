# <a name="module-5-configure-your-microsoft-sentinel-environment"></a>모듈 5 Microsoft Sentinel 환경 구성

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## <a name="explore-the-microsoft-sentinel-interface"></a>Microsoft Sentinel 인터페이스 살펴보기

1. [필수 구성 요소](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4) 섹션을 완료하는 동안 이전에 만든 Microsoft Sentinel 인터페이스로 돌아갑니다.

1. 새로 만든 Microsoft Sentinel 작업 영역 내를 이동하면서 사용자 인터페이스 옵션을 숙지합니다.

## <a name="create-a-watchlist"></a>관심 목록 만들기

이 작업에서는 관심 목록을 만듭니다.

1. In the search box at the bottom of the screen, enter <ph id="ph1">`Notepad`</ph>.  Select <bpt id="p1">**</bpt>Notepad<ept id="p1">**</ept> from the results.

1. `Hostname`을 입력한 다음 새 줄을 입력합니다.

1. 2~6행에 다음 호스트 이름을 추가합니다.
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. From the menu select, <bpt id="p1">**</bpt>File - Save As<ept id="p1">**</ept>, Name the file <ph id="ph1">`HighValue.csv`</ph>.  Then change the file type to <bpt id="p1">**</bpt>All files(<bpt id="p2">*</bpt>.<ept id="p2">*</ept>)<ept id="p1">**</ept>.  Then select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.

1. 메모장을 닫습니다.

1. Microsoft Sentinel의 **내 관심 목록** 영역에서 **관심 목록** 옵션을 선택합니다.

1. 명령 모음에서 **새로 추가**를 선택합니다.

1. 관심 목록 마법사에 다음 정보를 입력합니다.  이름: HighValueHosts  설명: 중요 호스트  관심 목록 별칭: HighValueHosts

1. **다음: 원본 >** 을 선택합니다.

1. 방금 만든 `HighValue.csv` 파일을 찾습니다. 

1. CSV 파일이 로드되면 **SearchKey 필드** 드롭다운에서 상자에서 **Hostname**을 선택합니다.

1. **다음: 검토 및 만들기 >** 를 선택합니다.

1. **만들기**를 선택합니다.

1. 화면에 관심 목록 목록이 다시 표시됩니다.

1. Select your new watchlist.  On the right tab, select <bpt id="p1">**</bpt>View in Log Analytics<ept id="p1">**</ept>.

1. 다음 KQL 문이 자동 실행되고 결과가 표시됩니다.

```KQL
_GetWatchlist('HighValueHosts')
```
**참고** 가져오기가 완료되려면 시간이 다소 걸릴 수 있습니다.

You can now use the _GetWatchlist('HighValueHosts') in your own KQL statements to access the list. The column to reference would be <bpt id="p1">*</bpt>Hostname<ept id="p1">*</ept>.

## <a name="create-a-threat-indicator"></a>위협 표시기 만들기

이 작업에서는 표시기를 만듭니다.

1. Microsoft Sentinel의 **위협 관리** 영역에서 **위협 인텔리전스** 옵션을 선택합니다.

1. 명령 모음에서 **새로 추가**를 선택합니다.

1. Review the different indicator types available in the Types dropdown.  Then select <bpt id="p1">**</bpt>domain-name<ept id="p1">**</ept>. Enter your initials in the Domain box. An example would be fmg.com.

1. 위협 유형에 대해 **+ 추가**를 선택하고 **악의적 활동**을 복사하여 필드에 붙여넣습니다.

1. For the name, enter the same value used for the Domain. An example would be fmg.com.

1. **유효 기간(시작)** 필드의 값을 오늘 날짜로 설정합니다.

1. **적용**을 선택합니다.

**참고** 표시기가 표시되려면 시간이 다소 걸릴 수 있습니다.

1. Select <bpt id="p1">**</bpt>Logs<ept id="p1">**</ept> option in the General area.  You may have to disable the "Always show queries" option to get to the query window.

1. 다음 KQL 문을 실행합니다.

```KQL
ThreatIntelligenceIndicator 
```
Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column.  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## <a name="you-have-completed-the-demo"></a>이 데모를 완료했습니다.