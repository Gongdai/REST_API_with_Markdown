
# CRUD site/group dynamic search criteria API.

## ***GET*** /V1/CMDB/...
## ***POST*** /V1/CMDB...
## ***PUT*** /V1/CMDB/...
## ***DELETE*** /V1/CMDB/...
Calling this API to advenced search devices in a specified devices range.

>***Use Case:*** <br>
Currently, after customer create Site successfully by calling our API and prepare to add devices into created site by calling add devices API, a device list is required as a input of add devices API. Then a commen issue is occured, if the customer own a significant number of devices and want to filt out a specified device list, that would be very hard to implemented by our current APIs.  Thus, we want to provide a dynamic search function for customers to help customers filt the specified devices from a huge device domain easily. Same with the dynamic search in our GUI system site manager page. We want to rely on the flexible combination of different filt conditions to let customers customize the unique devices filter for different purpose.

> If we can implement this feature successfully then that would be a very powerful function in our API. In order to maximize efficiency of dynamic search, we want to set the dynamic search as a independent API from others. The reason is when customers trying to create no matter a site or a group or modify the devices in current site, they always need to filt the devices first, if we only provide dynamic search in one API that will limite the utilize of dynamic search. The most convenient is if we can provide dynamic search independently, we can calling the dynamic search API with other already exist APIs during one workflow  to implemente a lot of complex use case. 

>As our conclusion, we want customers to call dynamic search first before create site or group to filt out a device list, we can return the device list to customers directly or return a taskID like calculate path API, then customers can put in the device list or taskID into create a group/site API. (decide by DEV)

>> **Workflow:**<br>
Create a site: calling dynamic search with curent domain as range -> get specified device list -> calling create site API(already exist) -> get the new site -> calling add devices API with the device list got from step one as input.<br><br>
Update a site: calling dynamic search API -> get device list -> calling add/replace site API(already exist) with the device list from dynamic search as input.<br><br>
Get site devices: calling get site devices API(already exist) -> get a device list of the whole site -> calling dynamic search API -> get device list after filt by dynamic search.<br><br>
Delete site devices: calling dynamic search API -> get device list -> calling delete site devices API(already exist) with the device list from dynamic search as input.<br>

>>***Note:*** all of these workflows are also fit for group modification and group devices modificaton.

## Detail Information

> **Title** : Dynamic search criteria API<br>

> **Version** : 03/19/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Sites{?sitePath}|{siteId}/SiteDevices{?deviceIp}|{?deviceHostName}

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)

>No request body.(We already have add, update, delete, replace site devices API, only need a GET function)


## Query Parameters(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|tenantIDorName | string  | The ID or name of a tenant that customers want to modify devices. |
|domainIDorName | string  | The ID or name of a domain that customers want to modify devices. |
|sitePathorID | string  | Full path name of a site. For example, 'My Network/Site1/Boston/Dev'. Or site ID |
|groupNameorID | string  | The ID or name of a group that customers want to modify devices. |
|devices* | json file  | List of device attributes.  |
>>**Note :** ^ required if the other parameter is null.


```python
data = {
    #"tenantIDorName" : "",
    "domainIDorName" : "",
    "sitePathorID" : "My Network/Site1/Boston/Dev", # OR
    "groupNameorID" : "",
    "devices" : {
        "deviceProperty":{
            "hostname" : [""],
            "mgmIp" : [""],
            "deviceType" : [""],
            "vendor" : [""],
            "model" : [""],
            "softwareVersion" : [""],
            "serialNumber" : [""],
            "location" : [""],
            "contact" : [""],
            "assetTag" : [""],
            "hierarchyLayer" : [""],
            "description" : [""],
            "virtualTech" : [""],
            "nodeGroup" : [""],
            "parentDevice" : [""],
            "time" : [""]
        },
        "interfaceProperty":{
            "interfaceName":[""],
            "ipv4Adress":[""],
            "ipv6Adress":[""],
            "ipv6LinkLocalAddress":[""],
            "bandwidth":[""],
            "speed":[""],
            "duplex":[""],
            "macAddress":[""],
            "moduleType":[""],
            "description":[""],
            "routingProtocol":[""],
            "multicastingMode":[""],
            "mplsVRF":[""],
            "mplsVPN":[""],
            "inboundACL":[""],
            "outboundACL":[""],
            "switchportMode":[""],
            "nativeVLAN":[""],
            "trunkEncapsulation":[""]
        },
        "moduleProperty":{
            "moduleType" : [""],
            "ports" : [""],
            "moduleSerialNum" : [""],
            "hwRev" : [""],
            "fwRev" : [""],
            "swRev" : [""],
            "description" : [""],
        },
        "configFile":"",
        "frontServer":"",
        "customizedGDR":{
            ......
        },
        "returnAtts":[......]
    }
}
# Set all device attributs as unrequired. Give the full privilege to users to modify which kinds of attributes they need to set
# as filter to search devices. And I recongnize to put a special symbol in value fields like "hostname" : "!R3", which means
# return all devices which name are not equal to "R3". Becasue in json file, there is no "!=", so i think we can set the input 
# rule for customer: in the value section, if the first charactor is "!", then it means "Does not match".
# Matches : "=", Contains : ">=", Does not contain : "!>"
```

## Response

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|deviceList|list of objects|The detail information of devices specified by ip or hostname|
|statusCode| integer | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |

> ***Example***


```python
# In the API response, we'd better can return the value of attributes of those which have been set by customers during
# input setting in "returnAtts" field.                 
#    
    
{
    "devicesList": [
        {
            "id": "ad53a0f6-644a-400b-9216-8df746baed3b",
            "mgmtIP": "10.1.12.2",
            "hostname": "Client1",
            "deviceTypeName": "Cisco Router"
        },
        {
            "id": "cd97d9ce-1d39-421d-a56d-e8da3aaa08c7",
            "mgmtIP": "10.1.13.2",
            "hostname": "Client2",
            "deviceTypeName": "Cisco Router"
        },
        {
            "id": "612a963c-e6cd-4ed1-8742-67b664dd214c",
            "mgmtIP": "10.2.18.2",
            "hostname": "Client4",
            "deviceTypeName": "Cisco Router"
        },
        {
            "id": "1a5d49f5-3755-4aad-b27d-cb5760aa494d",
            "mgmtIP": "10.1.20.130",
            "hostname": "Client7",
            "deviceTypeName": "Cisco Router"
        }
    ],
    "statusCode": 790200,
    "statusDescription": "Success."
}
```
