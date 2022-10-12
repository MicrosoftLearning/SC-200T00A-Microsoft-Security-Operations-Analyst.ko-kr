# <a name="module-6-create-detections-and-perform-investigations-with-microsoft-sentinel"></a>모듈 6 Microsoft Sentinel을 사용하여 탐지 만들기 및 조사 수행

**참고** 이 데모의 성공적인 완료는 [필수 구성 요소 문서](00-prerequisites.md)에 있는 모든 단계를 완료하는 것에 달려 있습니다. 

## <a name="attack-1-detection-with-sysmon"></a>Sysmon을 사용하여 공격 1 검색

이 작업에서는 보안 이벤트 커넥터와 Sysmon이 설치된 호스트에서 공격 1 검색을 만듭니다.

이 공격은 시작 시에 실행되는 레지스트리 키를 만듭니다.  
```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

1. WIN1 가상 머신에 Admin으로 로그인합니다. 암호로는 **Pa55w.rd**를 사용하여 로그인합니다.  

2. Edge 브라우저에서 Azure Portal(https://portal.azure.com )로 이동합니다.

3. 랩 호스팅 공급자가 제공한 관리자용 **테넌트 전자 메일** 계정을 복사하여 **로그인** 대화 상자에 붙여넣은 후 **다음**을 선택합니다.

4. 랩 호스팅 공급자가 제공한 관리자용 **테넌트 암호**를 복사하여 **암호 입력** 대화 상자에 붙여넣은 후 **로그인**을 선택합니다.

5. Azure Portal의 검색 창에 *Sentinel*을 입력하고 **Microsoft Sentinel**을 선택합니다.

6. 앞에서 만든 Microsoft Sentinel 작업 영역을 선택합니다.

7. 일반 섹션에서 **로그**를 선택합니다.

8. 먼저 데이터가 저장되는 위치를 확인해야 합니다. 방금 공격을 수행했으므로,  로그 시간 범위를 **지난 24시간**으로 설정합니다.

9. 다음 KQL 문을 실행합니다.

```KQL
search "temp\\startup.bat"
```

10. 결과에는 다음의 3개 테이블이 표시됩니다. DeviceProcessEvents DeviceRegistryEvents Event

    Device* 테이블은 엔드포인트용 Defender(데이터 커넥터 - Microsoft 365 Defender)에서 제공된 것입니다.  그리고 Event 테이블은 여기서 사용하는 데이터 커넥터 보안 이벤트에서 제공된 것입니다. 

    여기서는 Sysmon과 엔드포인트용 Defender의 두 원본에서 데이터를 수신하므로, 나중에 통합할 수 있는 KQL 문 두 개를 작성해야 합니다.  초기 조사에서 각 문을 개별적으로 살펴볼 예정입니다.

11. 첫 번째 데이터 원본은 Windows 호스트의 Sysmon입니다.  다음 KQL 문을 실행합니다.

```KQL
search in (Event) "temp\\startup.bat"
```
이제 결과에는 Event 테이블만 표시됩니다.  

16. Registry Key Set Value 행을 표시하는 KQL 문을 직접 작성합니다.  다음 KQL 쿼리를 실행합니다.

```KQL

Event
| where Source == "Microsoft-Windows-Sysmon"
| where EventID == 13
| extend RenderedDescription = tostring(split(RenderedDescription, ":")[0])
| project TimeGenerated, Source, EventID, Computer, UserName, EventData, RenderedDescription
| extend EvData = parse_xml(EventData)
| extend EventDetail = EvData.DataItem.EventData.Data
| project-away EventData, EvData  
| extend RuleName = EventDetail.[0].["#text"], EventType = EventDetail.[1].["#text"], UtcTime = EventDetail.[2].["#text"], ProcessGuid = EventDetail.[3].["#text"], 
    ProcessId = EventDetail.[4].["#text"], Image = EventDetail.[5].["#text"], TargetObject = EventDetail.[6].["#text"], Details = EventDetail.[7].["#text"]
    | project-away EventDetail 


```

17.  검색 규칙을 계속 작성할 수도 있지만, 이 KQL 문을 다른 검색 규칙의 KQL 문에 이 KQL 문을 재사용할 수 있을 것으로 보입니다.  
    
    로그 창에서 **저장**, **함수로 저장**을 차례로 선택합니다.
    저장 플라이아웃에 다음 정보를 입력합니다.

    이름: Event_Reg_SetValue 다른 이름으로 저장: 함수 별칭: Event_Reg_SetValue Category: Sysmon

18. 새 로그 쿼리 탭을 엽니다. 해당 탭에서 다음 KQL 문을 실행합니다.

```KQL

Event_Reg_SetValue

```
현재 데이터 컬렉션에 따라 행이 여러 개 반환될 수도 있습니다.  예상된 동작입니다.  다음 작업에서 이 랩의 시나리오에 맞게 결과를 필터링합니다.

19. 다음 KQL 문을 실행합니다.

```KQL

Event_Reg_SetValue | search "startup.bat"

```

22. 보안 작업 분석가가 위협을 정확하게 분석할 수 있도록 경고 관련 상황 정보를 최대한 많이 제공해야 합니다. 가령 조사 그래프에 사용할 엔터티 등을 제공할 수 있습니다.  다음 쿼리를 실행합니다.

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName

```

## <a name="you-have-completed-the-demo"></a>이 데모를 완료했습니다.