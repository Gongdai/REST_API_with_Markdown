
# Get Device Data API

## ***GET*** /V1/CMDB/Devices/DeviceRawData{?hostname}&{?IP}&{?tableName}&{?command}
Call this API to get the raw data for specified devices by device hostname or mgmIp.

## Detail Information

> **Title** : Get Device Raw Data API<br>

> **Version** : 04/30/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Devices/DeviceRawData

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Query parameter(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|hostname* | list of string  | The hostname of the device.  |
|IP* | list of string  | The management IP of  the device.  |
|table* | list of string  | the name of table which customer wants to retrieve. |
|cliCommand* | list of string  | The command which supported by customer system operation.  |
|baseline| string | Whether the customer want to retrieve the data from current baseline, currently we only support data from current baseline|

> ***Example***

```python
{
    "hostname" : ["R1", "R2"],
    "IP" : ["10.2.3.4", "10.2.3.5"],
    "table" : ["config...", "MAC"],
    "cliCommand" : ["show interface...", "show spinning tree..."],
    "baseline" : "currentBaseline"
}
```

## Headers

> **Data Format Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string  | support "application/json" |
| Accept | string  | support "application/json" |

> **Authorization Headers**

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from login API. |

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|content| string | Data content. |
|retrievalTime| string | The time of users retrieved data. |
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

> ***Example***


```python
# Success response:

{
    "content" : "raw data from database",
    "retrievalTime" : "yyyy-mm-dd:hh-mm-ss",
    "statusCode" : "790200",
    "statusDescription" : "Success."
}

#Failed Response:

{
    "content" : "Get raw data failed, reason:...",
    "retrievalTime" : "yyyy-mm-dd:hh-mm-ss",
    "statusCode" : "...",
    "statusDescription" : "..."
}
```
