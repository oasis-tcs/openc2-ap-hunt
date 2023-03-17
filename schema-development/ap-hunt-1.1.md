## Schema
|                . | .                                                         |
|-----------------:|:----------------------------------------------------------|
|       **title:** | Threat Hunting Profile                                    |
|     **package:** | https://praxiseng.com/threat-hunter-9001                  |
|     **version:** | 0-wd01                                                    |
| **description:** | Data definitions for Threat Hunting (TH) functions        |
| **namespaces:**  | {'ls': 'http://oasis-open.org/openc2/oc2ls-types/v1.1'}   |
|     **exports:** | AP-Target, AP-Args, AP-Specifiers, AP-Results, StixObject |

**_Type: Action (Enumerated)_**

| ID | Name            | Description                                                                                            |
|---:|:----------------|:-------------------------------------------------------------------------------------------------------|
|  3 | **query**       | Initiate a request for information.                                                                    |
| 30 | **investigate** | Task the recipient to aggregate and report information as it pertains to a security event or incident. |

**_Type: Target (Choice)_**

|   ID | Name         | Type         | # | Description                                                                        |
|-----:|:-------------|:-------------|--:|:-----------------------------------------------------------------------------------|
|    9 | **features** | Features     | 1 | A set of items used with the query Action to determine an Actuator's capabilities. |
| 1036 | **th**       | AP-Target$th | 1 | Threat Hunting Profile-defined targets                                             |

**_Type: Args (Map{1..*})_**

|   ID | Name                   | Type          | # | Description |
|-----:|:-----------------------|:--------------|--:|:------------|
|    1 | **start_time**         | Date-Time     | 1 |             |
|    2 | **stop_time**          | Date-Time     | 1 |             |
|    3 | **duration**           | Duration      | 1 |             |
|    4 | **response_requested** | Response-Type | 1 |             |
| 1036 | **th**                 | AP-Args$th    | 1 |             |

**_Type: Actuator (Choice)_**

|   ID | Name   | Type             | # | Description                    |
|-----:|:-------|:-----------------|--:|:-------------------------------|
| 1036 | **th** | AP-Specifiers$th | 1 | TH-defined actuator specifiers |

**_Type: Results (Map{1..*})_**

|   ID | Name           | Type               | # | Description                                                         |
|-----:|:---------------|:-------------------|--:|:--------------------------------------------------------------------|
|    1 | **versions**   | Results$Versions   | 1 | List of OpenC2 language versions supported by this Actuator         |
|    2 | **profiles**   | Results$Profiles   | 1 | List of profiles supported by this Actuator                         |
|    3 | **pairs**      | Action-Targets     | 1 | Targets applicable to each supported Action                         |
|    4 | **rate_limit** | Results$Rate-limit | 1 | Maximum number of requests per minute supported by design or policy |
| 1036 | **th**         | AP-Results$th      | 1 | TH-defined results                                                  |

**_Type: Pairs (Enumerated)_**

| ID | Name                                          | Description |
|---:|:----------------------------------------------|:------------|
|  3 | **query: features, /huntbooks, /datasources** |             |
| 30 | **investigate: /hunt**                        |             |

**_Type: AP-Target$th (Choice)_**

| ID | Name            | Type                   | # | Description                                                                                            |
|---:|:----------------|:-----------------------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **hunt**        | String                 | 1 | A procedure to find a set of entities in the monitored environment that associates with a cyberthreat. |
|  2 | **huntbooks**   | Huntbook-Specifiers$th | 1 | TH Huntbook specifiers.                                                                                |
|  3 | **datasources** | String                 | 1 |                                                                                                        |

**_Type: AP-Args$th (Map)_**

| ID | Name         | Type        | # | Description                                                    |
|---:|:-------------|:------------|--:|:---------------------------------------------------------------|
|  1 | **huntargs** | Huntargs$th | 1 | Arguments for use in conjunction with huntbook implementation. |

**_Type: Huntargs$th (Record{1..*})_**

| ID | Name             | Type                    | # | Description                                                                                                                     |
|---:|:-----------------|:------------------------|--:|:--------------------------------------------------------------------------------------------------------------------------------|
|  1 | **string_arg**   | String                  | 1 | string arguments supplied as huntargs.                                                                                          |
|  2 | **integer_arg**  | Integer{0..*}           | 1 | integer arguments supplied as huntargs.                                                                                         |
|  3 | **stix**         | AP-Args$STIX$th         | 1 | STIX arguments supplied as huntargs.                                                                                            |
|  4 | **timeranges**   | Huntargs$th$Timeranges  | 1 | a timerange used in the execution of a hunt.                                                                                    |
|  5 | **datasources**  | Huntargs$th$Datasources | 1 | You must identify one or more available data sources for hunting. These may be a host monitor, an EDR, a SIEM, a firewall, etc. |
|  6 | **ipv4_address** | IPv4-Addr               | 1 | IPv4 address as defined in [RFC0791].                                                                                           |
|  7 | **ipv6_address** | IPv6-Addr               | 1 | IPv6 address as defined in [RFC8200].                                                                                           |
|  8 | **ipv4_network** | IPv4-Net                | 1 | ipv4 network targeted by hunt activity.                                                                                         |
|  9 | **ipv6_network** | IPv6-Net                | 1 | ipv6 network targeted by hunt activity.                                                                                         |

**_Type: AP-Specifiers (Map)_**

| ID | Name | Type | # | Description |
| ---: | :--- | :--- | ---: | :--- |

**_Type: Huntbook-Specifiers (Map{1..*})_**

**_Type: Huntbook-Specifiers$th (Map)_**

| ID | Name              | Type                                 | # | Description                                                             |
|---:|:------------------|:-------------------------------------|--:|:------------------------------------------------------------------------|
|  1 | **path**          | String                               | 1 | Return huntbooks at and below this filesystem location (absolute path). |
|  2 | **tags**          | Huntbook-specifiers$th$Tags          | 1 | Return huntbooks with these keywords.                                   |
|  3 | **arg_types**     | Huntbook-specifiers$th$Arg-types     | 1 | Return huntbooks that take these argument types.                        |
|  4 | **arg_names**     | Huntbook-specifiers$th$Arg-names     | 1 | Return huntbooks that take these argument types.                        |
|  5 | **format_types**  | Return-Type$th                       | 1 | Return huntbooks that produce these output types.                       |
|  6 | **return_format** | Huntbook-specifiers$th$Return-format | 1 | For each huntbook returned, include these data items.                   |

**_Type: AP-Results$th (Map{1..*})_**

| ID | Name              | Type                        | # | Description                                              |
|---:|:------------------|:----------------------------|--:|:---------------------------------------------------------|
|  1 | **huntbook_info** | AP-Results$Huntbook-Info$th | 1 | Structured data returned by Query: Huntbooks.            |
|  2 | **datasources**   | Ap-results$th$Datasources   | 1 | Datasource names and info returned by Query Datasources. |

**_Type: Timerange$th (Choice)_**

| ID | Name                   | Type             | # | Description                                                             |
|---:|:-----------------------|:-----------------|--:|:------------------------------------------------------------------------|
|  1 | **timerange_absolute** | Timerange-Abs$th | 1 | Absolute timerange, defined by a start and end time in ISO 8601 format. |
|  2 | **timerange_relative** | Timerange-Rel$th | 1 | Relative timerange, example '3, Days' for last 3 days.                  |

**_Type: Time-Unit$th (Enumerated)_**

| ID | Name        | Description |
|---:|:------------|:------------|
|  1 | **Days**    |             |
|  2 | **Hours**   |             |
|  3 | **Minutes** |             |
|  4 | **Seconds** |             |

**_Type: Timerange-Abs$th (Record{2..*})_**

| ID | Name                | Type                             | # | Description                        |
|---:|:--------------------|:---------------------------------|--:|:-----------------------------------|
|  1 | **hunt_start_time** | Timerange-abs$th$Hunt-start-time | 1 | Start time, as a STIX time string. |
|  2 | **hunt_stop_time**  | Timerange-abs$th$Hunt-stop-time  | 1 | Stop time, as a STIX time string.  |

**_Type: Timerange-Rel$th (Record{2..*})_**

| ID | Name          | Type          | # | Description                        |
|---:|:--------------|:--------------|--:|:-----------------------------------|
|  1 | **number**    | Integer{0..*} | 1 | Start time, as a STIX time string. |
|  2 | **time_unit** | Time-Unit$th  | 1 | Start time, as a STIX time string. |


| Type Name           | Type Definition         | Description                          |
|:--------------------|:------------------------|:-------------------------------------|
| **AP-Args$STIX$th** | ArrayOf(STIX-Object$th) | STIX arguments supplied as huntargs. |


| Type Name          | Type Definition       | Description                                                             |
|:-------------------|:----------------------|:------------------------------------------------------------------------|
| **STIX-Object$th** | ArrayOf(String){1..*} | STIX cyber observables used in threat hunting. link to STIX table HERE. |


| Type Name       | Type Definition | Description                                                                                                                                                                         |
|:----------------|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Arg-Type$th** | String          | Argument types used by a Huntbook. Follow STIX naming conventions, with lowercase characters and hyphens replacing spaces. Common types include process, file, and network-traffic. |


| Type Name       | Type Definition | Description                                                                                                                |
|:----------------|:----------------|:---------------------------------------------------------------------------------------------------------------------------|
| **Arg-Name$th** | String          | Argument names used by a Huntbook. Follow C variable naming conventions. Examples include name, src_port, and x_unique_id. |

**_Type: Return-Type$th (Record{2..*})_**

| ID | Name         | Type        | # | Description                                      |
|---:|:-------------|:------------|--:|:-------------------------------------------------|
|  1 | **var_name** | Arg-Name$th | 1 | Variable name to be returned by use of Huntbook. |
|  2 | **var_type** | Arg-Type$th | 1 | Type of data to be returned by use of Huntbook.  |

**_Type: Datasource$th (Record{1..*})_**

| ID | Name        | Type                  | # | Description                                                |
|---:|:------------|:----------------------|--:|:-----------------------------------------------------------|
|  1 | **ds_name** | String                | 1 | Name of a Datasource used by a Huntbook in Kestrel runtime. |
|  2 | **ds_tags** | Datasource$th$Ds-tags | 1 | Tags applied to a Datasource for search or filter purposes. |

**_Type: Huntbook-Section$th (Enumerated)_**

| ID | Name                 | Description                                                                                           |
|---:|:---------------------|:------------------------------------------------------------------------------------------------------|
|  1 | **path**             | Specifies the return should include the path to each Huntbook specified by the query conditions.      |
|  2 | **uniqueId**         | Specifies the return should include the ID of each Huntbook specified by the query conditions.        |
|  3 | **args**             | Specifies the returned data should include the required arguments for the available Huntbooks.        |
|  4 | **expected_returns** | Specifies the returned data should include the expected returns for the available Huntbooks.          |
|  5 | **script**           | Specifies the returned data should include the full text of the Huntflow for each available Huntbook. |

**_Type: AP-Results$Huntbook-Info$th (Record{1..*})_**

| ID | Name                 | Type                                         | # | Description                                          |
|---:|:---------------------|:---------------------------------------------|--:|:-----------------------------------------------------|
|  1 | **path**             | String                                       | 1 | Path used to identify a Huntbook in place of a name. |
|  2 | **uniqueId**         | Integer{0..*}                                | 1 | Unique ID associated with a specified Huntbook.      |
|  3 | **args**             | Ap-results$huntbook-info$th$Args             | 1 | a list of arguments used in the specified Huntflow.  |
|  4 | **expected_returns** | Ap-results$huntbook-info$th$Expected-returns | 1 | Data returned by the specified Huntbooks.            |
|  5 | **script**           | String                                       | 1 | Text of Hunt logic imlemented by specified Huntbook. |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **StixTime** | String | string representation of ISO 8601 time |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Ap-results$Huntbooks** | ArrayOf(String) | Huntbook names returned by query huntbooks |


| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Ap-results$Datasources** | ArrayOf(String) | Datasource identifiers returned by query datasources |

| Type Name                 | Type Definition | Description                                                |
|:--------------------------|:----------------|:-----------------------------------------------------------|
| **Datasource$th$Ds-tags** | ArrayOf(String) | Tags applied to a datasruce for search or filter purposes. |

