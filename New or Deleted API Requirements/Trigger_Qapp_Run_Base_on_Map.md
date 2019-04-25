
## ***POST*** /V1/CMDB/Maps/TriggerQapp{?mapID}
Calling this API to trigger a Qapp run base on an existing map with input of mapID and Qapp information.

## Detail Information

> **Title** : Trigger Qapp Run Base on Existing Map API<br>

> **Version** : 04/25/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Maps/TriggerQapp	

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Query Parameters(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|mapID* | string  | The identify ID of one existing map.  |

 ## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|QappPath* | string  | The absolute path of the Qapp in NetBrain system. |
|dataSource* | integer  | 1 : Current baseline <br> 2 : Select a time period <br> 3 : Select a time point <br> 4 : Pull live data regularly <br> 5 : Pull live data once <br>  |
|dataSource.from| string | If customer select 2 in dataSource, the value of this field must be provided.|
|dataSource.to| string | If customer select 2 in dataSource, the value of this field must be provided.|
|dataSource.timePoint| string | If customer select 3 in dataSource, the value of this field must be provided.|
|dataSource.period| integer | If customer select 4 in dataSource, the value of this field must be provided. how long customer want to re-run current Qapp. |
|dataSource.unit| char | If customer select 4 in dataSource, the value of this field must be provided. Unit of time period<br> s: second <br> m: minute<br> h: hour|
|dataSource.times| integer | how many times customer wants to re-run this Qapp. |


***Example:***


```python
body = {
    "QappPath" : "All Qapps/Built-in Qapps/Monitoring/Monitor CLNS Traffic",
    "dataSource" : {
        "dataSource" : 2,
        "from" : "mm/dd/yyyy-hh:mm",
        "to" : "mm/dd/yyyy-hh:mm"
    }
}
```

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Massage| string | Qapp running status description. |
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

> ***Example***


```python
{
    "Message" : "Qapp run successfully!",
    "statusCode" : "790200",
    "statusDescription" : "Success."
}
```
