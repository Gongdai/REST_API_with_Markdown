
## ***PUT*** / acknowledge event alert
## ***PUT*** / close event alert
## ***DELETE*** / delete event alert

## Detail Information

> **Title** : Get Event Console API<br>

> **Version** : 04/03/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/...

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

***Example:***


```python
body = {
    "eventIDs" : [
        {"eventID" : "4d409565-eb4d-817e-8180-c24c25d309c1"},
        {"eventID" : "4d409565-eb4d-817e-8180-............"},
        .
        .
        .
    ]
}

# For DELETE function this is a data form not a body.
```

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|message | string |decribe the acknowledge status.|
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

***Example:***


```python
# acknowledged successfully.
{
    "message":"XXX have been acknowledged/closed/delete successfully!",
    "statusCode" : 790200,
    "statusDescription": "Success."
}

# acknowledged failed.
{
    "message":"[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...] acknowledge/closed/delete failed! Reason:...",
    "statusCode" : "...",
    "statusDescription": "..."
}

# acknowledged partial successfully.
{
    "message":"Warning: acknowledge/closed/delete partial successfully! Reason:[XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, ...] in "eventIDs" list are not found.",
    "statusCode" : "790206", # HTTP status code: 206 partial content.
    "statusDescription": "Success with warning."
}
```
