## Schema
| . | . |
| ---: | :--- |
| **title:** | Threat Hunting Profile |
| **package:** | https://praxiseng.com/threat-hunter-9001 |
| **version:** | 0-wd01 |
| **description:** | Data definitions for Threat Hunting (TH) functions |
| **exports:** | OpenC2-Command, OpenC2-Response |

**_Type: OpenC2-Command (Record)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **action** | Action | 1 | The task or activity to be performed (i.e., the 'verb'). |
| 2 | **target** | Target | 1 | The object of the Action. The Action is performed on the Target. |
| 3 | **args** | Args | 0..1 | Additional information that applies to the Command. |
| 4 | **actuator** | Actuator | 0..1 | The subject of the Action. The Actuator executes the Action on the Target. |
| 5 | **command_id** | Command-ID | 0..1 | An identifier of this Command. |

**_Type: OpenC2-Response (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **status** | Status-Code | 1 | An integer status code |
| 2 | **status_text** | String | 0..1 | A free-form human-readable description of the Response status |
| 3 | **results** | Results | 0..1 | Map of key:value pairs that contain additional results based on the invoking Command. |

**_Type: Action (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 3 | **query** | Initiate a request for information. |
| 30 | **investigate** |  |

**_Type: Target (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 9 | **features** | Features | 1 | A set of items used with the query Action to determine an Actuator's capabilities. |
| 1036 | **th/** | AP-Target$th | 1 | Threat Hunting Profile-defined targets |

**_Type: Args (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **start_time** | Date-Time | 0..1 |  |
| 2 | **stop_time** | Date-Time | 0..1 |  |
| 3 | **duration** | Duration | 0..1 |  |
| 4 | **response_requested** | Response-Type | 0..1 |  |
| 1036 | **th/** | AP-Args$th | 1 |  |

**_Type: Actuator (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1036 | **th/** | AP-Specifiers$th | 1 | TH-defined actuator specifiers |

**_Type: Results (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **versions** | Version unique | 0..10 | List of OpenC2 language versions supported by this Actuator |
| 2 | **profiles** | Nsid unique | 0..* | List of profiles supported by this Actuator |
| 3 | **pairs** | Pairs | 0..1 | Targets applicable to each supported Action |
| 4 | **rate_limit** | Number{0.0..*} | 0..1 | Maximum number of requests per minute supported by design or policy |
| 1036 | **th/** | AP-Results$th | 0..1 | TH-defined results |

**_Type: Pairs (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 3 | **query: features, /huntbooks, /datasources** |  |
| 30 | **investigate: /hunt** |  |

**_Type: AP-Target$th (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **hunt** | String | 1 | description here |
| 2 | **huntbooks** | Huntbook-Specifiers$th | 1 | description here |
| 3 | **datasources** | Datasource-Specifiers$th | 1 | description here |

**_Type: AP-Args$th (Map{2..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **string_arg** | String | 0..1 | string arguments supplied as huntargs |
| 2 | **integer_arg** | Integer | 0..1 | integer arguments supplied as huntargs |
| 3 | **time_arg** | AP-Args$Time-arg$th | 0..1 | Date-Time arguments supplied as huntargs |
| 4 | **stix/** | AP-Args$Stix$th | 0..1 | stix arguments supplied as huntargs |
| 5 | **timerange** | Stix-Timerange$th | 0..1 | string arguments supplied as huntargs |
| 6 | **path** | Path-Format$th | 0..1 | integer arguments supplied as huntargs |
| 7 | **datasource** | String{1..*} | 1 | Date-Time arguments supplied as huntargs |
| 8 | **hunt_process/** | Hunt-Process$th | 0..1 | process targeted by hunt activity: specify type. |
| 9 | **ipv4_address** | IPv4-Addr | 0..1 | IPv4 address as defined in [RFC0791] |
| 10 | **ipv6_address** | IPv6-Addr | 0..1 | IPv6 address as defined in [RFC8200] |
| 11 | **ipv4_network** | IPv4-Net | 0..1 | ipv4 network targeted by hunt activity |
| 12 | **ipv6_network** | IPv6-Net | 0..1 | ipv6 network targeted by hunt activity |
| 13 | **endpoint** | String | 0..1 | endpoint targeted by hunt activity |
| 14 | **directory** | String | 0..1 | directory targeted by hunt activity |

**_Type: AP-Specifiers$th (Map)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |

**_Type: Huntbook-Specifiers$th (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **named** | String | 0..1 | requests information from an element with the given name |
| 2 | **full** | Boolean | 1 | Specifies the return should include each supported huntbook with their full usage information |
| 3 | **titles** | Boolean | 0..1 | Specifies the return type should be a list of titles (Strings) |
| 4 | **args** | String | 0..1 | Specifies the returned data should include the required arguments for the given Huntbook |
| 5 | **returns** | String | 0..1 | Specifies the returned data should include the expected returns for the given Huntbook |

**_Type: Datasource-Specifiers$th (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **named** | String | 0..1 | requests information from an element with the given name |
| 2 | **full** | Boolean | 1 | Specifies the return should include each accessible datasource with their full usage information |
| 3 | **titles** | Boolean | 0..1 | Specifies the return type should be a list of titles (Strings) |

**_Type: AP-Results$th (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **huntbooks** | Ap-results$Huntbooks$th | 0..1 | Huntbook names returned by query huntbooks |
| 2 | **datasources** | Ap-results$Datasources$th | 0..1 | Datasource identifiers returned by query datasources |

**_Type: Hunt-Process$th (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **name** | String | 0..1 | targeted process name as a String |
| 2 | **uuid** | String | 0..1 | targeted process UUID |
| 3 | **pid** | Integer | 0..1 | targeted process PID |

**_Type: Stix-Timerange$th (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **timerange_absolute** | Timerange-Abs$th | 0..1 | Absolute timerange, defined by a start and end time in ISO 8601 format |
| 2 | **timerange_relative** | Timerange-Rel$th | 0..1 | Relative timerange, example '3, Days' for last 3 days |

**_Type: Path-Format$th (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **path_absolute** | String | 0..1 | absolute path to target |
| 2 | **path_relative** | String | 0..1 | relative path to target |

**_Type: Time-Unit$th (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 1 | **Days** |  |
| 2 | **Hours** |  |
| 3 | **Minutes** |  |
| 4 | **Seconds** |  |

**_Type: Timerange-Abs$th (Record{2..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **hunt_start_time** | String | 1 | Start time, as a Stix time string |
| 2 | **hunt_stop_time** | String | 1 | Start time, as a Stix time string |

**_Type: Timerange-Rel$th (Record{2..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **number** | Integer | 1 | Start time, as a Stix time string |
| 2 | **time_unit** | Time-Unit$th | 1 | Start time, as a Stix time string |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **StixObject$th** | ArrayOf(String){1..*} | Stix cyber observables used in threat hunting. link to STIX table HERE |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **AP-Args$Time-arg$th** | ArrayOf(Date-Time){1..*} | time arguments supplied as huntargs |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **AP-Args$Stix$th** | ArrayOf(StixObject$th){1..*} | stix arguments supplied as huntargs |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Ap-results$Huntbooks$th** | ArrayOf(String) | Huntbook names returned by query huntbooks |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Ap-results$Datasources$th** | ArrayOf(String) | Datasource identifiers returned by query datasources |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Features** | ArrayOf(Feature){0..10} unique | An array of zero to ten names used to query a Consume for its supported capabilities. |

**_Type: IPv4-Net (Array /ipv4-net)_**

| ID | Type | # | Description |
| ---: | :--- | ---: | :--- |
| 1 | **** | IPv4-Addr | 1 | ipv4_addr:: IPv4 address as defined in [[RFC0791]](#rfc0791) |
| 2 | **** | Integer | 0..1 | prefix_length:: CIDR prefix-length. If omitted, refers to a single host address. |

**_Type: IPv6-Net (Array /ipv6-net)_**

| ID | Type | # | Description |
| ---: | :--- | ---: | :--- |
| 1 | **** | IPv6-Addr | 1 | ipv6_addr:: IPv6 address as defined in [[RFC8200]](#rfc8200) |
| 2 | **** | Integer | 0..1 | prefix_length:: prefix length. If omitted, refers to a single host address |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Date-Time** | Integer{0..*} | Date and Time |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Duration** | Integer{0..*} | A length of time |

**_Type: Feature (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 1 | **versions** | List of OpenC2 Language versions supported by this Consumer |
| 2 | **profiles** | List of profiles supported by this Consumer |
| 3 | **pairs** | List of supported Actions and applicable Targets |
| 4 | **rate_limit** | Maximum number of Commands per minute supported by design or policy |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **IPv4-Addr** | Binary /ipv4-addr | 32 bit IPv4 address as defined in [[RFC0791]](#rfc0791) |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **IPv6-Addr** | Binary /ipv6-addr | 128 bit IPv6 address as defined in [[RFC8200]](#rfc8200) |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Nsid** | String{1..16} | A short identifier that refers to a namespace. |

**_Type: Response-Type (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 0 | **none** | No response |
| 1 | **ack** | Respond when Command received |
| 2 | **status** | Respond with progress toward Command completion |
| 3 | **complete** | Respond when all aspects of Command completed |

**_Type: Status-Code (Enumerated.ID)_**

| ID | Description |
| ---: | :--- |
| 102 | **Processing**::an interim Response used to inform the Producer that the Consumer has accepted the Command but has not yet completed it |
| 200 | **OK**::the Command has succeeded |
| 201 | **Created**::the Command has succeeded and a new resource has been created as a result of it |
| 400 | **Bad Request**::the Consumer cannot process the Command due to something that is perceived to be a Producer error (e.g., malformed Command syntax) |
| 401 | **Unauthorized**::the Command Message lacks valid authentication credentials for the target resource or authorization has been refused for the submitted credentials |
| 403 | **Forbidden**::the Consumer understood the Command but refuses to authorize it |
| 404 | **Not Found**::the Consumer has not found anything matching the Command |
| 500 | **Internal Error**::the Consumer encountered an unexpected condition that prevented it from performing the Command |
| 501 | **Not Implemented**::the Consumer does not support the functionality required to perform the Command |
| 503 | **Service Unavailable**::the Consumer is currently unable to perform the Command due to a temporary overloading or maintenance of the Consumer |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Command-ID** | String{pattern="^\S{0,36}$"} | Command Identifier |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Version** | String | Major.Minor version number |
