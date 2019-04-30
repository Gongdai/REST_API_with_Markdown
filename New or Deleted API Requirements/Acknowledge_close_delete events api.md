
## ***PUT*** / acknowledge or close event alert
## ***DELETE*** / delete event alert

## Detail Information

> **Title** : Modify Event Console API<br>

> **Version** : 04/30/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/V1/CMDB/EventConsole

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request Body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|eventID* | list of string  | A string list include the taskIDs of all events which customer want to acknowledged. |
|eventStatus| integer | Modify event status<br> 1 : set event as acknowledged<br> 2 : set event as closed | # Only for PUT function

***Example:***


```python
# For DELETE function this is a data form not a body.
data form for DELETE function = {
    "eventIDs" : [
        {"eventID" : "4d409565-eb4d-817e-8180-c24c25d309c1"},
        {"eventID" : "4d409565-eb4d-817e-8180-............"},
        .
        .
        .
    ]
}

body for PUT function = {
    "eventIDs" : [
        {"eventID" : "4d409565-eb4d-817e-8180-c24c25d309c1", "eventStatus" : 1}, #set event as acknowledged
        {"eventID" : "4d409565-eb4d-817e-8180-............", "eventStatus" : 2}, #set event as closed
        .
        .
        .
    ]
}


```

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|message | string |decribe the acknowledge status.|
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

***Example:***


```python
# Modify successfully.
{
    "message":"[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...] have been acknowledged successfully, [XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...] have been closed successfully!"
    "statusCode" : 790200,[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...]
    "statusDescription": "Success."
}

# Modify failed.
{
    "message":"[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...] acknowledge or close failed! Reason:...",
    "statusCode" : "...",
    "statusDescription": "Failed"
}

# DELETE successfully.
{
    "message":"[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...] have been delete successfully!"
    "statusCode" : 790200,
    "statusDescription": "Success."
}

# DELETE failed.
{
    "message":"[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...]  delete failed! Reason:...",
    "statusCode" : "...",
    "statusDescription": "Failed"
}

# acknowledged partially successed.
{
    "message":"Warning: acknowledge/closed/delete partially successed! Reason:[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...] in "eventIDs" list are not found.",
    "statusCode" : "790200", # HTTP status code: 200 partial content.
    "statusDescription": "Success with warning."
}
```
