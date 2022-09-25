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

8. First, you need to see where the data is stored. Since you just performed the attacks.  Set the Log Time Range to <bpt id="p1">**</bpt>Last 24 hours<ept id="p1">**</ept>.

9. 다음 KQL 문을 실행합니다.

```KQL
search "temp\\startup.bat"
```

10. 결과에는 다음의 3개 테이블이 표시됩니다. DeviceProcessEvents DeviceRegistryEvents Event

    The Device* tables are from Defender for Endpoint (Data Connector - Microsoft 365 Defender).  Event is from our Data Connector Security Events. 

    Since we are receiving data from two different sources - Sysmon and Defender for Endpoint,  we will need to build two KQL statements that could be unioned later.  In our initial investigation, you will look at each separately.

11. Our first data source is Sysmon from Windows hosts.  Run the following KQL Statement.

```KQL
search in (Event) "temp\\startup.bat"
```
이제 결과에는 Event 테이블만 표시됩니다.  

16. Create your own KQL statement to display all Registry Key Set Value rows.  Run the following KQL query:

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
    
    In the Log window, select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>, then <bpt id="p2">**</bpt>Save as function<ept id="p2">**</ept>.
    In the Save flyout, enter the following:

    이름: Event_Reg_SetValue 다른 이름으로 저장: 함수 별칭: Event_Reg_SetValue Category: Sysmon

18. 새 로그 쿼리 탭을 엽니다. 해당 탭에서 다음 KQL 문을 실행합니다.

```KQL

Event_Reg_SetValue

```
Depending on the current data collection, you could receive many rows.  This is expected.  Our next task is to filter to our specific scenario.

19. 다음 KQL 문을 실행합니다.

```KQL

Event_Reg_SetValue | search "startup.bat"

```

22. It is important to help the Security Operations Analyst by providing as much context about the alert as you can. This includes projecting Entities for use in the investigation graph.  Run the following query:

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName

```

## <a name="you-have-completed-the-demo"></a>이 데모를 완료했습니다.