## Schema
| . | . |
| ---: | :--- |
| **title:** | Threat Hunting Profile |
| **package:** | https://github.com/oasis-tcs/openc2-ap-hunt |
| **version:** | 0-wd01 |
| **description:** | Data definitions for Threat Hunting (TH) functions |
| **namespaces:** | {'ls': 'http://oasis-open.org/openc2/oc2ls-types/v1.1'} |
| **exports:** | AP-Target, AP-Args, AP-Specifiers, AP-Results, StixObject |

**_Type: Action (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 3 | **query** |  |
| 30 | **investigate** |  |

**_Type: Target (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 9 | **features** |  |
| 1036 | **th** |  |

**_Type: Args (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 1 | **start_time** |  |
| 2 | **stop_time** |  |
| 3 | **duration** |  |
| 4 | **response_requested** |  |
| 1036 | **th** |  |

**_Type: Actuator (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 1036 | **th** |  |

**_Type: Results (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 1 | **versions** |  |
| 2 | **profiles** |  |
| 3 | **pairs** |  |
| 4 | **rate_limit** |  |
| 5 | **args** |  |
| 1036 | **th** |  |

**_Type: Pairs (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 3 | **query: features, /huntbooks, /datasources** |  |
| 30 | **investigate: /hunt** |  |

**_Type: AP-Target (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **hunt** | String | 1 | description here |
| 2 | **huntbooks** | Huntbook-Specifiers | 1 | description here |
| 3 | **datasources** | Datasource-Specifiers | 1 | description here |

**_Type: AP-Args (Map{2..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **string_arg** | String | 0..1 | string arguments supplied as huntargs |
| 2 | **integer_arg** | Integer | 0..1 | integer arguments supplied as huntargs |
| 3 | **time_arg** | AP-Args$Time-arg | 0..1 | Date-Time arguments supplied as huntargs |
| 4 | **stix/** | AP-Args$Stix | 0..1 | stix arguments supplied as huntargs |
| 5 | **timerange** | Stix-Timerange | 0..1 | string arguments supplied as huntargs |
| 6 | **path** | Path-Format | 0..1 | integer arguments supplied as huntargs |
| 7 | **datasource** | String{1..*} | 1 | Date-Time arguments supplied as huntargs |
| 8 | **hunt_process/** | Hunt-Process | 0..1 | process targeted by hunt activity: specify type. |
| 9 | **ipv4_address** | ls:IPv4-Addr | 0..1 | IPv4 address as defined in [RFC0791] |
| 10 | **ipv6_address** | ls:IPv6-Addr | 0..1 | IPv6 address as defined in [RFC8200] |
| 11 | **ipv4_network** | ls:IPv4-Net | 0..1 | ipv4 network targeted by hunt activity |
| 12 | **ipv6_network** | ls:IPv6-Net | 0..1 | ipv6 network targeted by hunt activity |
| 13 | **endpoint** | String | 0..1 | endpoint targeted by hunt activity |
| 14 | **directory** | String | 0..1 | directory targeted by hunt activity |

**_Type: AP-Specifiers (Map)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |

**_Type: Huntbook-Specifiers (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **named** | String | 0..1 | requests information from an element with the given name |
| 2 | **full** | Boolean | 1 | Specifies the return should include each supported huntbook with their full usage information |
| 3 | **titles** | Boolean | 0..1 | Specifies the return type should be a list of titles (Strings) |
| 4 | **args** | String | 0..1 | Specifies the returned data should include the required arguments for the given Huntbook |
| 5 | **returns** | String | 0..1 | Specifies the returned data should include the expected returns for the given Huntbook |

**_Type: Datasource-Specifiers (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **named** | String | 0..1 | requests information from an element with the given name |
| 2 | **full** | Boolean | 1 | Specifies the return should include each accessible datasource with their full usage information |
| 3 | **titles** | Boolean | 0..1 | Specifies the return type should be a list of titles (Strings) |

**_Type: AP-Results (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **huntbooks** | Ap-results$Huntbooks | 0..1 | Huntbook names returned by query huntbooks |
| 2 | **datasources** | Ap-results$Datasources | 0..1 | Datasource identifiers returned by query datasources |

**_Type: Hunt-Process (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **name** | String | 0..1 | targeted process name as a String |
| 2 | **uuid** | String | 0..1 | targeted process UUID |
| 3 | **pid** | Integer | 0..1 | targeted process PID |

**_Type: Stix-Timerange (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **timerange_absolute** | Timerange-Abs | 0..1 | Absolute timerange, defined by a start and end time in ISO 8601 format |
| 2 | **timerange_relative** | Timerange-Rel | 0..1 | Relative timerange, example '3, Days' for last 3 days |

**_Type: Path-Format (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **path_absolute** | String | 0..1 | absolute path to target |
| 2 | **path_relative** | String | 0..1 | relative path to target |

**_Type: Time-Unit (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 1 | **Days** |  |
| 2 | **Hours** |  |
| 3 | **Minutes** |  |
| 4 | **Seconds** |  |

**_Type: Timerange-Abs (Record{2..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **hunt_start_time** | String | 1 | Start time, as a Stix time string |
| 2 | **hunt_stop_time** | String | 1 | Start time, as a Stix time string |

**_Type: Timerange-Rel (Record{2..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **number** | Integer | 1 | Start time, as a Stix time string |
| 2 | **time_unit** | Time-Unit | 1 | Start time, as a Stix time string |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **StixObject** | ArrayOf(String){1..*} | Stix cyber observables used in threat hunting. link to STIX table HERE |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **AP-Args$Time-arg** | ArrayOf(ls:Date-Time){1..*} | time arguments supplied as huntargs |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **StixTime** | String | string representation of ISO 8601 time |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **AP-Args$Stix** | ArrayOf(StixObject){1..*} | stix arguments supplied as huntargs |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Ap-results$Huntbooks** | ArrayOf(String) | Huntbook names returned by query huntbooks |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Ap-results$Datasources** | ArrayOf(String) | Datasource identifiers returned by query datasources |
