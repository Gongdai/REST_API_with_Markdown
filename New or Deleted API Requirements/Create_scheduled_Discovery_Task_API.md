
## ***POST*** /V1/CMDB/Benchmark/Tasks
This API call is used to crreate a scheduled Discovery task to a domain.

Note that, as the key, task name should be unique system wide.

***Warning:*** We only consider "Scan the following IPs" as input method.

## Detail Information

> **Title** : Create Scheduled Discovery Task API<br>

> **Version** : 04/22/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Discovery/Tasks	

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

 ## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|taskName* | string  | The name of the task.  |
|description | string  | The description of the task. This field is optional.  |
|startDate* | string  | The date when the task starts to run. The standard time format is required, for example, '2017-07-13', '2017/07/13'. This field is optional. Current date will be used by default.  |
|schedule* | object  | The schedule to run the task. The following sub parameters are included in this object: <br>▪ frequency* (string) - the frequency to run the task. This field is required and includes ”once”, “hourly”,” daily”, “weekly” and “monthly” options.<br>▪ interval(string) - the interval to run the task (optional). This field is only valid for “hourly”,” daily”, and “weekly” options and the default value is 1, such as every 1 hour, 1 week.<br>▪ startTime* (string) - the time to run the task. This field is required and startTime should be in format: ["HH:mm:ss"], if you put date time format such as "2018/04/04 19:20:20 ", "19:20:20" will be used and the date part "2018/04/04" will be ignored.<br> **Note:** Set the time according to your IIS server time zone since the time zone of your ISS server rather than your physical time zone is adopted by the benchmark task.<br>▪ weekday(integer) - the day of the week to run the task. This field is optional and only valid when the frequency is weekly.  0 stands for Sunday, 6 for Saturday and 1-5 for Monday to Friday respectively.<br>▪ dayOfMonth(integer) - which day of a month to run the task. This field is optional and only valid when the frequency is monthly. The default is 1.<br>▪ Months(integer) - which month to run the task. This field is optional and only valid when the frequency is monthly. The default is all 12 months.|

> ### ***Example***



```python
body = {
        "taskName":taskName, #The name of the task.
        "startDate":startDate, #The date when the task starts to run. The standard time format is required, for example, '2017-07-13', '2017/07/13'.
        "schedule":{
            "frequency":frequency, #The frequency to run the task. This field is required and includes ”once”, “hourly”,” daily”, “weekly” and “monthly” options.
            "startTime":[startTime] #The time to run the task. This field is required and startTime should be in format: ["HH:mm:ss"], if you put date time format such as "2018/04/04 19:20:20 ", "19:20:20" will be used and the date part "2018/04/04" will be ignored.
            }
        }
```

## Parameters(****required***)

> No parameters required.

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
|statusCode| integer | Code issued by NetBrain server indicating the execution result.  |
|statusDescription| string | The explanation of the status code. |

> ***Example***


```python
{
    "Message" : "Discovery Task <task name> created successfully. "
    "statusCode": 790200,
    "statusDescription": "Success."
}
```
