
## ***POST*** /V1/CMDB/Maps/TriggerQapp{?mapID}{?pageID}
Calling this API to trigger a Qapp run base on an existing map with input of mapID, pageID and Qapp information.

The purpose of this API is service for "Embeded Map", when customer open the embeded map to check the data view, the real time data is necessary for customers. So we need to trigger the Qapp to run with a period to renew the data continuously. But in embeded map, we don't allow customer to make any changes to the map, even run Qapp. Then we need a API to trigger the Qapp run automatically on back end.

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

> No required query parameters.

 ## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|mapID* | string  | The identify ID of one existing map.  |
|pageID* | string  | The identify ID of one existing page in one existing map.  |
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
    "Message" : "Qapp trigger successfully!",
    "statusCode" : "790200",
    "statusDescription" : "Success."
}
```
