## Schema
| . | . |
| ---: | :--- |
| **title:** | Threat Hunting Profile |
| **package:** | https://praxiseng.com/threat-hunter-9001 |
| **version:** | 0-wd01 |
| **description:** | Data definitions for Threat Hunting (TH) functions |
| **namespaces:** | {'ls': 'http://oasis-open.org/openc2/oc2ls-types/v1.1', 'th': 'https://github.com/oasis-tcs/openc2-ap-hunt'} |
| **exports:** | OpenC2-Command, OpenC2-Response |

**_Type: OpenC2-Command (Record)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **action** | Action | 1 | The task or activity to be performed (i.e., the 'verb'). |
| 2 | **target** | Target | 1 | The object of the Action. The Action is performed on the Target. |
| 3 | **args** | Args | 0..1 | Additional information that applies to the Command. |
| 4 | **actuator** | Actuator | 0..1 | The subject of the Action. The Actuator executes the Action on the Target. |
| 5 | **command_id** | ls:Command-ID | 0..1 | An identifier of this Command. |

**_Type: OpenC2-Response (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **status** | ls:Status-Code | 1 | An integer status code |
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
| 9 | **features** | ls:Features | 1 | A set of items used with the query Action to determine an Actuator's capabilities. |
| 1036 | **th/** | th:AP-Target | 1 | Threat Hunting Profile-defined targets |

**_Type: Args (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **start_time** | ls:Date-Time | 0..1 |  |
| 2 | **stop_time** | ls:Date-Time | 0..1 |  |
| 3 | **duration** | ls:Duration | 0..1 |  |
| 4 | **response_requested** | ls:Response-Type | 0..1 |  |
| 1036 | **th/** | th:AP-Args | 1 |  |

**_Type: Actuator (Choice)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1036 | **th/** | th:AP-Specifiers | 1 | TH-defined actuator specifiers |

**_Type: Results (Map{1..*})_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |
| 1 | **versions** | ls:Version unique | 0..10 | List of OpenC2 language versions supported by this Actuator |
| 2 | **profiles** | ls:Nsid unique | 0..* | List of profiles supported by this Actuator |
| 3 | **pairs** | Pairs | 0..1 | Targets applicable to each supported Action |
| 4 | **rate_limit** | Number{0.0..*} | 0..1 | Maximum number of requests per minute supported by design or policy |
| 1036 | **th/** | th:AP-Results | 0..1 | TH-defined results |

**_Type: Pairs (Enumerated)_**

| ID | Name | Description |
| ---: | :--- | :--- |
| 3 | **query: features, /huntbooks, /datasources** |  |
| 30 | **investigate: /hunt** |  |
