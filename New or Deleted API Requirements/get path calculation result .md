
# Path API Design

## ***GET*** /V1/CMDB/Path/Calculation/{taskID}/Result	
Call this API to get the hop information of a path calculated through the CalcPath API. 

If the Calculation Path task is not finished yet or failed, user will get an error with messsage reminding.which means you don't need to wait anymore before trying to query the result.

All directed links in the result consists of a directed path grapth, which contains all possible reachable paths from the original source to the destination specified in path calculation

## Detail Information

> **Title** : Get Path Calulation Result API<br>

> **Version** : 01/30/2019.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Path/Calculation/{taskID}/Result	

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)

> No request body.

## Path Parameters(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|taskID* | string  | Input the task ID returned by the CalcPath API. |

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
|path_overview| need to be fixed | need to be fixed |
|path_overview.failure_reasons| need to be fixed | need to be fixed |
|path_overview.status| need to be fixed | need to be fixed |
|path_overview.path_list.failure_reasons| need to be fixed | need to be fixed|
|path_overview.path_list.path_name| need to be fixed | need to be fixed |
|path_overview.path_list.description| need to be fixed | need to be fixed |
|path_overview.path_list.status| need to be fixed | need to be fixed |
|path_overview.path_list.branch_list[].failure_reason| need to be fixed | need to be fixed |
|path_overview.path_list.branch_list[].status| need to be fixed | need to be fixed |
|path_overview.path_list.branch_list[].hop_detail_list[]| need to be fixed | need to be fixed |
|path_overview.path_list.branch_list[].hop_detail_list[].hop_id| need to be fixed | need to be fixed |
|path_overview.path_list.branch_list[].hop_detail_list[].hop_detail| need to be fixed |need to be fixed |
|path_overview.path_list.branch_list[].hop_detail_list[].hop_detail.fromDev| need to be fixed | need to be fixed |
|path_overview.path_list.branch_list[].hop_detail_list[].hop_detail.fromDev.devId| need to be fixed | need to be fixed|
|...|need to be fixed|need to be fixed|
|...|need to be fixed|need to be fixed|
|...|need to be fixed|need to be fixed|
|...|need to be fixed|need to be fixed|
|...|need to be fixed|need to be fixed|
|.|need to be fixed|need to be fixed|
|.|need to be fixed|need to be fixed|
|.|need to be fixed|need to be fixed|
|statusCode| integer | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |


## Example:


```python
{
    "path_overview": { #modified name
        "failure_reasons": [],
        "status": "Success",
        "path_list": [{
                "failure_reasons": [],
                "path_name": "L3 Path",
                "description": "UDP 10.88.8.4:0 -> 10.88.0.68:20000",
                "status": "Success",
                "branch_list": [{
                        "failure_reason": "",
                        "status": "Success",
                        "hop_detail_list": [ #modified name
                            {
                                "hop_id": "efb27df1-c7ad-45dc-b26c-734e32d5983b", #modified position
                                "hop_detail": { #modified name
                                    "fromDev": {
                                        "devId": "d9cdd7ed-8dae-f74b-5eb7-1590f6561953",
                                        "devName": "East_Call_Center",
                                        "devType": 1006,
                                        "domainId": ""
                                    },
                                    "fromIntf": {
                                        "intfKeyObj": {
                                            "schema": "ipIntfs._id",
                                            "value": "fee7dec5-42da-426b-a53e-8a155f456c7b"
                                        },
                                        "intfDisplaySchemaObj": {
                                            "schema": "ipIntfs.name",
                                            "value": "E0 10.88.8.4/26"
                                        },
                                        "PhysicalInftName": "E0"
                                    },
                                    "isComplete": false,
                                    "isP2P": false,
                                    "mediaId": "eac015d2-a213-4dc1-a03f-54fcc2c46f7b",
                                    "mediaInfo": {
                                        "mediaName": "10.88.8.0/26\r\nHSRP: 0(10.88.8.1)",
                                        "mediaType": "Lan",
                                        "neat": false,
                                        "topoType": "L3_Topo_Type"
                                    },
                                    "preHopId": "00000000-0000-0000-0000-000000000000",
                                    "sequnce": 0,
                                    "toIntf": {
                                        "intfKeyObj": {
                                            "schema": "ipIntfs._id",
                                            "value": "df711817-737e-4c6e-af06-53b20edf1d71"
                                        },
                                        "intfDisplaySchemaObj": {
                                            "schema": "ipIntfs.name",
                                            "value": "Vlan30 10.88.8.2/26"
                                        },
                                        "PhysicalInftName": "Vlan30"
                                    },
                                    "toDev": {
                                        "devId": "5f21fc5b-d54e-40fa-b264-7c2c61acfe6a",
                                        "devName": "Sjc-Dist-3750-01",
                                        "devType": 2001,
                                        "domainId": ""
                                    },
                                    "topoType": "L3_Topo_Type",
                                    "trafficState": {
                                        "acl": "",
                                        "alg": -1,
                                        "dev_name": "East_Call_Center",
                                        "dev_type": 1006,
                                        "in_intf": "E0",
                                        "in_intf_schema": "intfs",
                                        "in_intf_topo_type": "L3_Topo_Type",
                                        "next_dev_in_intf": "Vlan30 10.88.8.2/26",
                                        "next_dev_in_intf_schema": "ipIntfs",
                                        "next_dev_in_intf_topo_type": "L3_Topo_Type",
                                        "next_dev_name": "Sjc-Dist-3750-01",
                                        "next_dev_type": 2001,
                                        "next_hop_ip": "10.88.8.2",
                                        "next_hop_mac": "",
                                        "out_intf": "E0 10.88.8.4/26",
                                        "out_intf_schema": "ipIntfs",
                                        "out_intf_topo_type": "L3_Topo_Type",
                                        "pbr": "",
                                        "vrf": ""
                                    },
                                    "parentHopId": ""
                                }
                            },
                            {
                                "hop_id": "a2f84c09-58c6-4f97-a988-a092bdd94b7e", #modified position
                                "hop_detail": { #modified name
                                    "fromDev": {
                                        "devId": "5f21fc5b-d54e-40fa-b264-7c2c61acfe6a",
                                        "devName": "Sjc-Dist-3750-01",
                                        "devType": 2001,
                                        "domainId": ""
                                    },
                                    "fromIntf": {
                                        "intfKeyObj": {
                                            "schema": "ipIntfs._id",
                                            "value": "f530607b-0c53-4835-9a12-08da8fc0ec93"
                                        },
                                        "intfDisplaySchemaObj": {
                                            "schema": "ipIntfs.name",
                                            "value": "FastEthernet1/0/18 10.88.11.26/30"
                                        },
                                        "PhysicalInftName": "FastEthernet1/0/18"
                                    },
                                    "isComplete": false,
                                    "isP2P": false,
                                    "mediaId": "dcd2b309-4001-4384-b7fb-8485dbbc099d",
                                    "mediaInfo": {
                                        "mediaName": "10.88.11.24/30",
                                        "mediaType": "Lan",
                                        "neat": true,
                                        "topoType": "L3_Topo_Type"
                                    },
                                    "preHopId": "efb27df1-c7ad-45dc-b26c-734e32d5983b",
                                    "sequnce": 1,
                                    "toIntf": {
                                        "intfKeyObj": {
                                            "schema": "ipIntfs._id",
                                            "value": "706d103a-fe33-4561-8462-208e6b036301"
                                        },
                                        "intfDisplaySchemaObj": {
                                            "schema": "ipIntfs.name",
                                            "value": "GigabitEthernet0/21 10.88.11.25/30"
                                        },
                                        "PhysicalInftName": "GigabitEthernet0/21"
                                    },
                                    "toDev": {
                                        "devId": "1fbfb24e-dce4-4b19-81a7-159a821c247d",
                                        "devName": "Sjc-Core-3560x-01",
                                        "devType": 2001,
                                        "domainId": ""
                                    },
                                    "topoType": "L3_Topo_Type",
                                    "trafficState": {
                                        "acl": "",
                                        "alg": -1,
                                        "dev_name": "Sjc-Dist-3750-01",
                                        "dev_type": 2001,
                                        "in_intf": "Vlan30 10.88.8.2/26",
                                        "in_intf_schema": "ipIntfs",
                                        "in_intf_topo_type": "L3_Topo_Type",
                                        "next_dev_in_intf": "GigabitEthernet0/21 10.88.11.25/30",
                                        "next_dev_in_intf_schema": "ipIntfs",
                                        "next_dev_in_intf_topo_type": "L3_Topo_Type",
                                        "next_dev_name": "Sjc-Core-3560x-01",
                                        "next_dev_type": 2001,
                                        "next_hop_ip": "10.88.11.25",
                                        "next_hop_mac": "",
                                        "out_intf": "FastEthernet1/0/18 10.88.11.26/30",
                                        "out_intf_schema": "ipIntfs",
                                        "out_intf_topo_type": "L3_Topo_Type",
                                        "pbr": "",
                                        "vrf": ""
                                    },
                                    "parentHopId": ""
                                }
                            },
                            {
                                "hop_id": "703111e9-4977-4858-a0af-fa50ca4b8012",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "7027bd86-3250-4adf-8b16-8304a18d4032",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "9530d550-9a2d-4c1f-8287-2221dfd385ee",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "2253069d-0df4-4821-bb24-96a3757677f4",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "dcc551fb-8a6f-4002-9dc3-b8a182db056f",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "7d69b570-5137-4379-96a7-21039b7e5f99",
                                "hop_detail": {
                                    ...
                                }
                            }
                        ]
                    },
                    {
                        "failure_reason": "",
                        "status": "Success",
                        "hop_list": [{
                                "hop_id": "49a46063-c819-4ded-9ed6-182a9139bc69",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "2c429463-5c45-4822-9c67-05167eda5740",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "ce7909a5-2535-4add-a85b-fbb5f38baccb",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "7027bd86-3250-4adf-8b16-8304a18d4032",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "9530d550-9a2d-4c1f-8287-2221dfd385ee",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "2253069d-0df4-4821-bb24-96a3757677f4",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "dcc551fb-8a6f-4002-9dc3-b8a182db056f",
                                "hop_detail": {
                                    ...
                                }
                            },
                            {
                                "hop_id": "7d69b570-5137-4379-96a7-21039b7e5f99",
                                "hop_detail": {
                                    ...
                                }
                            }
                        ]
                    }
                ]
            },
            {
                "failure_reasons": [],
                "path_name": "L2 Path",
                "description": "10.88.8.4 -> 10.88.8.2",
                "status": "Failed",
                "branch_list": [{
                    "failure_reason": "No L2 connections were found",
                    "status": "Failed",
                    "hop_list": [{
                        "hop_id": "02724de1-995b-4334-96b0-5c033d7bb738",
                        "hop_detail": {
                            ...
                        }
                    }]
                }]
            },
            {
                "failure_reasons": [],
                "path_name": "L2 Path",
                "description": "10.88.8.4 -> 10.88.8.3",
                "status": "Failed",
                "branch_list": [{
                    "failure_reason": "No L2 connections were found",
                    "status": "Failed",
                    "hop_list": [{
                        "hop_id": "3c99e38d-e082-4f6f-a5e5-eeb86e0c2ca5",
                        "hop_detail": {
                            ...
                        }
                    }]
                }]
            }
        ]
    },
	"isLiveUseBaseLineConfig" : true,
	"statusCode": 790200,
    "statusDescription": "Success."
}

```
