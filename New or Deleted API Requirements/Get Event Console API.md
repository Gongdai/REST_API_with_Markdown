
# Event Console API

## ***GET*** / entire or partial console table
how to get the map URL 

***Use Case:***<br>
First of all, according to the user requirment, we should return the whole event console table to customers. Then we should also provide a simplyfied dynamic search for customer to get a piece of events from entire console. In our opinion, it should be a complex key(device + event), ((need return the unique event ID for each row)) 

>hint: if the customers want to get a specified events group then customer can put in the hostname of device to get all event about this device, event name to get all devices own this event or device name and event name together to return the data about the device own the event.

For event console API, except get function we also need DELETE, acknowledge, close and open map according to the GUI event console. Then we face to a problem: how to specify an event? As we know, in the event console, the device hostname and event are always same in different rows, if we want to provide a primary key, then it must be unique. How can we set up the primary key?

After we set up the primary key for each event, then we can provide the other functions to modify the entire event console with primary key as input(DELETE, acknowledge, close and open map).

***Work Flow:***
> Calling get event console API -> <br>return entire console table(json) -> <br>get primary key for specified event -> <br>calling acknowledge event or open event map API -> <br>acknowledge event alert or check detail map information -> <br>calling close event alert API -> <br>calling delete event alert API.

## Detail Information

> **Title** : Get Events API<br>

> **Version** : 03/20/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/...

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Query Parameters(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|eventType|list of integer| The collection region of events.<br>1: My Events<br>2: Shared Events<br>1: Global Events|
|level|list of integer| The collection level of events.<br>1: Error<br>2:Warning|
|timeRange| integer |The collection time region of events.<br>24: last 24 hours<br>48: last 48 hours<br>7: last 7 days|
|fromTime| date |customized events collection start time. We only support UTC time structure, customer need to follow the data example.|
|toTime| date |customized events collection end time.We only support UTC time structure, customer need to follow the data example.|

***Example:***


```python
data = {
    "eventType" : [1,2,3],
    "level" : [1,2],
    "timeRange": 24,
    "fromTime":"yyyy-mm-ddThh:mm:ssZ",
    "toTime":"yyyy-mm-ddThh:mm:ssZ"
}
```

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
| eventID | string | the unique ID of each event (Must exist, for modify and delete API) |
| device | string |device name or ip|
| event | string |description of event |
| firstTime |string| The first time of happend of this event|
| lastTime |string| The last happend time of this event|
| count | integer |...|
|acknowleged| string | ...|
|status|integer|...|
|executedBy|string|...|
|taskType|integer|...|
|fromTask|string|...|



```python
 response = {
    "content": [
      {
        "id": "4d409565-eb4d-817e-8180-c24c25d309c1",
        "runUserId": "5c8becac-dec4-400e-a5e8-87db424fe88d",
        "runUserName": "gdluserTest",
        "qappId": "25c5b0e2-7e0a-4a72-a885-3abfbe8a1871",
        "objId": "f7b8059c-61c1-4adc-9879-f1d726a68a49",
        "objName": "R11",
        "devId": "f7b8059c-61c1-4adc-9879-f1d726a68a49",
        "devName": "R11",
        "intfId": "",
        "intfName": "",
        "msg": "Memory utilization is 61.0% >=  60.0%.",
        "level": 1,
        "firstTime": "2019-03-28T11:57:25Z",
        "lastTime": "2019-03-28T11:57:25Z",
        "count": 1,
        "fromTask": "stub4-20190328115722.Page 1.Result 1.Overall Health Monitor [SNMP]",
        "alertBzType": 1,
        "ackFlag": false,
        "closeFlag": false,
        "alertBzId": "83e6707b-1852-437e-879d-c00dd30eaba8",
        "alertBzInfo": {
          "mapInfo": {
            "mapId": "dc949c0a-344a-4690-8900-41bad2ff4fd5",
            "mapTitle": "stub4-20190328115722",
            "mapPageId": "127c69d1-cb04-4078-9a91-5bb8699a452f",
            "mapPageTitle": "Page 1"
          },
          "activity": {
            "id": "83e6707b-1852-437e-879d-c00dd30eaba8",
            "name": "Result 1",
            "sourceTaskId": "e5b1f9de-89aa-4e91-a8fc-a0294759ceb0",
            "createInfo": {
              "userId": "5c8becac-dec4-400e-a5e8-87db424fe88d",
              "userName": "gdluserTest",
              "dateTime": "0001-01-01T00:00:00Z"
            }
          }
        }
      },
        .
        .
        .
    ]
   
 }
```
