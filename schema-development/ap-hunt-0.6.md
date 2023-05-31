## Schema
|                . | .                                                                                                                                                                                                              |
|-----------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **package:** | https://github.com/oasis-tcs/openc2-ap-hunt                                                                                                                                                                    |
|     **version:** | 0-wd01                                                                                                                                                                                                         |
|       **title:** | Threat Hunting Profile                                                                                                                                                                                         |
| **description:** | Data definitions for Threat Hunting (TH) functions                                                                                                                                                             |
|  **namespaces:** | **ls**: http://oasis-open.org/openc2/oc2ls-types/v1.1                                                                                                                                                          |
|     **exports:** | AP-Target, AP-Args, AP-Specifiers, AP-Results                                                                                                                                                                  |
|      **config:** | **$MaxBinary**: 5555 **$MaxString**: 5555 **$MaxElements**: 555 **$Sys**: $ **$TypeName**: ^[A-Za-z][-:_A-Za-z0-9]{0,63}$ **$FieldName**: ^[A-Za-z][-:_A-Za-z0-9]{0,63}$ **$NSID**: ^[A-Za-z][A-Za-z0-9]{0,7}$ |

**_Type: Action (Enumerated)_**

| ID | Name            | Description                                                                                            |
|---:|:----------------|:-------------------------------------------------------------------------------------------------------|
|  3 | **query**       | Initiate a request for information.                                                                    |
| 30 | **investigate** | Task the recipient to aggregate and report information as it pertains to a security event or incident. |

**_Type: Target (Enumerated)_**

|   ID | Name         | Description |
|-----:|:-------------|:------------|
|    9 | **features** |             |
| 1036 | **th**       |             |

**_Type: Args (Enumerated)_**

|   ID | Name                   | Description |
|-----:|:-----------------------|:------------|
|    1 | **start_time**         |             |
|    2 | **stop_time**          |             |
|    3 | **duration**           |             |
|    4 | **response_requested** |             |
| 1036 | **th**                 |             |

**_Type: Actuator (Enumerated)_**

|   ID | Name   | Description |
|-----:|:-------|:------------|
| 1036 | **th** |             |

**_Type: Results (Enumerated)_**

|   ID | Name           | Description |
|-----:|:---------------|:------------|
|    1 | **versions**   |             |
|    2 | **profiles**   |             |
|    3 | **pairs**      |             |
|    4 | **rate_limit** |             |
|    5 | **args**       |             |
| 1036 | **th**         |             |

**_Type: Pairs (Enumerated)_**

| ID | Name                                          | Description |
|---:|:----------------------------------------------|:------------|
|  3 | **query: features, /huntbooks, /datasources** |             |
| 30 | **investigate: /hunt**                        |             |

**_Type: AP-Target (Choice)_**

| ID | Name            | Type                | # | Description                                                                                            |
|---:|:----------------|:--------------------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **hunt**        | String              | 1 | A procedure to find a set of entities in the monitored environment that associates with a cyberthreat. |
|  2 | **huntbooks**   | Huntbook-Specifiers | 1 | TH Huntbook specifiers.                                                                                |
|  3 | **datasources** | String              | 1 |                                                                                                        |

**_Type: AP-Args (Map)_**

| ID | Name         | Type     | # | Description                                                    |
|---:|:-------------|:---------|--:|:---------------------------------------------------------------|
|  1 | **huntargs** | Huntargs | 1 | Arguments for use in conjunction with huntbook implementation. |

**_Type: Huntargs (Record{1..*})_**

| ID | Name             | Type             | # | Description                                                                                       |
|---:|:-----------------|:-----------------|--:|:--------------------------------------------------------------------------------------------------|
|  1 | **string_arg**   | String           | 1 | string arguments supplied as huntargs.                                                            |
|  2 | **integer_arg**  | Integer{0..*}    | 1 | integer arguments supplied as huntargs.                                                           |
|  3 | **stix**         | sco:STIX-Cybersecurity-Observables  | 1 | STIX arguments supplied as huntargs.                                                              |
|  4 | **timeranges**   | Timeranges       | 1 | Timeranges used in the execution of a hunt.                                                       |
|  5 | **datasources**  | Datasource-Array | 1 | Available data sources for hunting. These may be a host monitor, an EDR, a SIEM, a firewall, etc. |
|  6 | **ipv4_address** | ls:IPv4-Addr     | 1 | IPv4 address as defined in [RFC0791].                                                             |
|  7 | **ipv6_address** | ls:IPv6-Addr     | 1 | IPv6 address as defined in [RFC8200].                                                             |
|  8 | **ipv4_network** | ls:IPv4-Net     | 1 | ipv4 network targeted by hunt activity.                                                           |
|  9 | **ipv6_network** | ls:IPv6-Net     | 1 | ipv6 network targeted by hunt activity.                                                           |

**_Type: AP-Specifiers (Map{1..*})_**

| ID | Name | Type | # | Description |
|---:|:-----|:-----|--:|:------------|

**_Type: Huntbook-Specifiers (Map)_**

| ID | Name              | Type                | # | Description                                                             |
|---:|:------------------|:--------------------|--:|:------------------------------------------------------------------------|
|  1 | **path**          | String              | 1 | Return huntbooks at and below this filesystem location (absolute path). |
|  2 | **tags**          | Tags                | 1 | Return huntbooks with these keywords.                                   |
|  3 | **arg_types**     | Specified-Arg-Types | 1 | Return huntbooks that take these argument types.                        |
|  4 | **arg_names**     | Specified-Arg-Names | 1 | Return huntbooks that take these argument types.                        |
|  5 | **format_types**  | Return-Type         | 1 | Return huntbooks that produce these output types.                       |
|  6 | **return_format** | Huntbook-Sections   | 1 | For each huntbook returned, include these data items.                   |


| Type Name               | Type Definition   | Description                                      |
|:------------------------|:------------------|:-------------------------------------------------|
| **Specified-Arg-Types** | ArrayOf(Arg-Type) | Return huntbooks that take these argument types. |


| Type Name               | Type Definition   | Description                                            |
|:------------------------|:------------------|:-------------------------------------------------------|
| **Specified-Arg-Names** | ArrayOf(Arg-Name) | Return huntbooks that take arguments with these names. |

**_Type: AP-Results (Map{1..*})_**

| ID | Name              | Type                     | # | Description                                              |
|---:|:------------------|:-------------------------|--:|:---------------------------------------------------------|
|  1 | **huntbook_info** | Ap-results$Huntbook-info | 1 | Structured data returned by Query: Huntbooks.            |
|  2 | **datasources**   | Datasource-Array         | 1 | Datasource names and info returned by Query Datasources. |
|  3 | **stix_returns**  | sco:STIX-Cybersecurity-Observables | 1 | STIX SCO object returns                                  |


| Type Name      | Type Definition    | Description                                  |
|:---------------|:-------------------|:---------------------------------------------|
| **Timeranges** | ArrayOf(Timerange) | a timerange used in the execution of a hunt. |

**_Type: Timerange (Choice)_**

| ID | Name                   | Type          | # | Description                                                             |
|---:|:-----------------------|:--------------|--:|:------------------------------------------------------------------------|
|  1 | **timerange_absolute** | Timerange-Abs | 1 | Absolute timerange, defined by a start and end time in ISO 8601 format. |
|  2 | **timerange_relative** | Timerange-Rel | 1 | Relative timerange, example '3, Days' for last 3 days.                  |

**_Type: Time-Unit (Enumerated)_**

| ID | Name        | Description |
|---:|:------------|:------------|
|  1 | **Days**    |             |
|  2 | **Hours**   |             |
|  3 | **Minutes** |             |
|  4 | **Seconds** |             |

**_Type: Timerange-Abs (Record{2..*})_**

| ID | Name                | Type   | # | Description                        |
|---:|:--------------------|:-------|--:|:-----------------------------------|
|  1 | **hunt_start_time** | sco:timerange | 1 | Start time, as a STIX time string. |
|  2 | **hunt_stop_time**  | sco:timerange | 1 | Stop time, as a STIX time string.  |

**_Type: Timerange-Rel (Record{2..*})_**

| ID | Name          | Type          | # | Description                                                |
|---:|:--------------|:--------------|--:|:-----------------------------------------------------------|
|  1 | **number**    | Integer{0..*} | 1 | Number of specified Time Units used in Relative Timerange. |
|  2 | **time_unit** | Time-Unit     | 1 | Time Unit Keywords.                                        |


| Type Name    | Type Definition | Description                                                                                                                                                                         |
|:-------------|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Arg-Type** | String          | Argument types used by a Huntbook. Follow STIX naming conventions, with lowercase characters and hyphens replacing spaces. Common types include process, file, and network-traffic. |


| Type Name    | Type Definition | Description                                                                                                                |
|:-------------|:----------------|:---------------------------------------------------------------------------------------------------------------------------|
| **Arg-Name** | String          | Argument names used by a Huntbook. Follow C variable naming conventions. Examples include name, src_port, and x_unique_id. |

**_Type: Return-Type (Record{2..*})_**

| ID | Name         | Type     | # | Description                                      |
|---:|:-------------|:---------|--:|:-------------------------------------------------|
|  1 | **var_name** | Arg-Name | 1 | Variable name to be returned by use of Huntbook. |
|  2 | **var_type** | Arg-Type | 1 | Type of data to be returned by use of Huntbook.  |

**_Type: Datasource (Record{1..*})_**

| ID | Name        | Type   | # | Description                                                 |
|---:|:------------|:-------|--:|:------------------------------------------------------------|
|  1 | **ds_name** | String | 1 | Name of a Datasource used by a Huntbook in Kestrel runtime. |
|  2 | **ds_tags** | Tags   | 1 | Tags applied to a Datasource for search or filter purposes. |


| Type Name             | Type Definition           | Description                                           |
|:----------------------|:--------------------------|:------------------------------------------------------|
| **Huntbook-Sections** | ArrayOf(Huntbook-Section) | For each huntbook returned, include these data items. |

**_Type: Huntbook-Section (Enumerated)_**

| ID | Name                 | Description                                                                                           |
|---:|:---------------------|:------------------------------------------------------------------------------------------------------|
|  1 | **path**             | Specifies the return should include the path to each Huntbook specified by the query conditions.      |
|  2 | **uniqueId**         | Specifies the return should include the ID of each Huntbook specified by the query conditions.        |
|  3 | **version**          | Specifies the return should include the ID of each Huntbook specified by the query conditions.        |
|  4 | **args_required**    | Specifies the returned data should include the required arguments for the available Huntbooks.        |
|  5 | **expected_returns** | Specifies the returned data should include the expected returns for the available Huntbooks.          |
|  6 | **script**           | Specifies the returned data should include the full text of the Huntflow for each available Huntbook. |

**_Type: Huntbook-Info (Record{1..*})_**

| ID | Name                 | Type            | # | Description                                          |
|---:|:---------------------|:----------------|--:|:-----------------------------------------------------|
|  1 | **path**             | String          | 1 | Path used to identify a Huntbook in place of a name. |
|  2 | **uniqueId**         | Integer{0..*}   | 1 | Unique ID associated with a specified Huntbook.      |
|  3 | **version**          | String          | 1 | Unique ID associated with a specified Huntbook.      |
|  4 | **args_required**    | Typed-Arguments | 1 | List of arguments used in the specified Huntflow.    |
|  5 | **expected_returns** | Typed-Arguments | 1 | Data returned by the specified Huntbooks.            |
|  6 | **script**           | String          | 1 | Text of Hunt logic imlemented by specified Huntbook. |


| Type Name      | Type Definition      | Description                          |
|:---------------|:---------------------|:-------------------------------------|
| **STIX-Array** | ArrayOf(STIX-Object) | STIX arguments supplied as huntargs. |


| Type Name       | Type Definition | Description                                                             |
|:----------------|:----------------|:------------------------------------------------------------------------|
| **STIX-Object** | ArrayOf(String) | STIX cyber observables used in threat hunting. link to STIX table HERE. |


| Type Name            | Type Definition     | Description                                                  |
|:---------------------|:--------------------|:-------------------------------------------------------------|
| **Datasource-Array** | ArrayOf(Datasource) | An Array of Datasources, with multiple uses in Threathunting |


| Type Name | Type Definition | Description                                 |
|:----------|:----------------|:--------------------------------------------|
| **Tags**  | ArrayOf(String) | Tags applied for search or filter purposes. |


| Type Name           | Type Definition           | Description                                           |
|:--------------------|:--------------------------|:------------------------------------------------------|
| **Typed-Arguments** | MapOf(Arg-Name, Arg-Type) | Argument names and types tied to a specific Huntbook. |


| Type Name                    | Type Definition        | Description                                   |
|:-----------------------------|:-----------------------|:----------------------------------------------|
| **Ap-results$Huntbook-info** | ArrayOf(Huntbook-Info) | Structured data returned by Query: Huntbooks. |
