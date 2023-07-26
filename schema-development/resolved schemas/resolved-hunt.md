## Schema
|                . | .                                                                                                                                                                                                              |
|-----------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **package:** | https://praxiseng.com/threat-hunter-9001                                                                                                                                                                       |
|     **version:** | 0-wd01                                                                                                                                                                                                         |
|       **title:** | Threat Hunting Profile                                                                                                                                                                                         |
| **description:** | Data definitions for Threat Hunting (TH) functions                                                                                                                                                             |
|     **exports:** | OpenC2-Command, OpenC2-Response, SCO                                                                                                                                                                           |
|      **config:** | **$MaxBinary**: 5555 **$MaxString**: 5555 **$MaxElements**: 555 **$Sys**: $ **$TypeName**: ^[A-Za-z][-:_A-Za-z0-9]{0,63}$ **$FieldName**: ^[A-Za-z][-:_A-Za-z0-9]{0,63}$ **$NSID**: ^[A-Za-z][A-Za-z0-9]{0,7}$ |

**_Type: OpenC2-Command (Record)_**

| ID | Name           | Type       | # | Description                                                                |
|---:|:---------------|:-----------|--:|:---------------------------------------------------------------------------|
|  1 | **action**     | Action     | 1 | The task or activity to be performed (i.e., the 'verb').                   |
|  2 | **target**     | Target     | 1 | The object of the Action. The Action is performed on the Target.           |
|  3 | **args**       | Args       | 1 | Additional information that applies to the Command.                        |
|  4 | **actuator**   | Actuator   | 1 | The subject of the Action. The Actuator executes the Action on the Target. |
|  5 | **command_id** | Command-ID | 1 | An identifier of this Command.                                             |

**_Type: OpenC2-Response (Map{1..*})_**

| ID | Name            | Type        | # | Description                                                                           |
|---:|:----------------|:------------|--:|:--------------------------------------------------------------------------------------|
|  1 | **status**      | Status-Code | 1 | An integer status code                                                                |
|  2 | **status_text** | String      | 1 | A free-form human-readable description of the Response status                         |
|  3 | **results**     | Results     | 1 | Map of key:value pairs that contain additional results based on the invoking Command. |

**_Type: Action (Enumerated)_**

| ID | Name            | Description                                                                                            |
|---:|:----------------|:-------------------------------------------------------------------------------------------------------|
|  3 | **query**       | Initiate a request for information.                                                                    |
| 30 | **investigate** | Task the recipient to aggregate and report information as it pertains to a security event or incident. |

**_Type: Target (Choice)_**

|   ID | Name         | Type      | # | Description                                                                        |
|-----:|:-------------|:----------|--:|:-----------------------------------------------------------------------------------|
|    9 | **features** | Features  | 1 | A set of items used with the query Action to determine an Actuator's capabilities. |
| 1036 | **th**       | AP-Target | 1 | Threat Hunting Profile-defined targets                                             |

**_Type: Args (Map{1..*})_**

|   ID | Name                   | Type          | # | Description |
|-----:|:-----------------------|:--------------|--:|:------------|
|    1 | **start_time**         | Date-Time     | 1 |             |
|    2 | **stop_time**          | Date-Time     | 1 |             |
|    3 | **duration**           | Duration      | 1 |             |
|    4 | **response_requested** | Response-Type | 1 |             |
| 1036 | **th**                 | AP-Args       | 1 |             |

**_Type: Actuator (Choice)_**

|   ID | Name   | Type          | # | Description                    |
|-----:|:-------|:--------------|--:|:-------------------------------|
| 1036 | **th** | AP-Specifiers | 1 | TH-defined actuator specifiers |

**_Type: Results (Map{1..*})_**

|   ID | Name           | Type               | # | Description                                                         |
|-----:|:---------------|:-------------------|--:|:--------------------------------------------------------------------|
|    1 | **versions**   | Results$Versions   | 1 | List of OpenC2 language versions supported by this Actuator         |
|    2 | **profiles**   | Results$Profiles   | 1 | List of profiles supported by this Actuator                         |
|    3 | **pairs**      | Pairs              | 1 | Targets applicable to each supported Action                         |
|    4 | **rate_limit** | Results$Rate-limit | 1 | Maximum number of requests per minute supported by design or policy |
|    5 | **args**       | Results$Args       | 1 |                                                                     |
| 1036 | **th**         | AP-Results         | 1 | TH-defined results                                                  |

**_Type: Pairs (Enumerated)_**

| ID | Name                                          | Description |
|---:|:----------------------------------------------|:------------|
|  3 | **query: features, /huntflows, /datasources** |             |
| 30 | **investigate: /hunt**                        |             |

**_Type: AP-Target (Choice)_**

| ID | Name            | Type                | # | Description                                                                                            |
|---:|:----------------|:--------------------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **hunt**        | String              | 1 | A procedure to find a set of entities in the monitored environment that associates with a cyberthreat. |
|  2 | **huntflows**   | Huntflow-Specifiers | 1 | TH Huntflow specifiers.                                                                                |
|  3 | **datasources** | String              | 1 |                                                                                                        |

**_Type: AP-Args (Map)_**

| ID | Name         | Type     | # | Description                                                    |
|---:|:-------------|:---------|--:|:---------------------------------------------------------------|
|  1 | **huntargs** | Huntargs | 1 | Arguments for use in conjunction with huntflow implementation. |

**_Type: Huntargs (Record{1..*})_**

| ID | Name                | Type                           | # | Description                                                                                       |
|---:|:--------------------|:-------------------------------|--:|:--------------------------------------------------------------------------------------------------|
|  1 | **string_args**     | Huntargs$String-args           | 1 | string arguments supplied as huntargs.                                                            |
|  2 | **integer_args**    | Huntargs$Integer-args          | 1 | integer arguments supplied as huntargs.                                                           |
|  3 | **typed_args**      | Typed-Arguments                | 1 | Paired strings of named arguments.                                                                |
|  4 | **native_oc2**      | OC2-Data                       | 1 | OC2 Language types supplied as huntargs.                                                          |
|  5 | **stix**            | STIX-Cybersecurity-Observables | 1 | STIX arguments supplied as huntargs.                                                              |
|  6 | **stix_extensions** | String                         | 1 | OCA Extended STIX arguments supplied as huntargs. add a custom stix for oca-asset and event       |
|  7 | **timeranges**      | Timeranges                     | 1 | Timeranges used in the execution of a hunt.                                                       |
|  8 | **datasources**     | Datasource-Array               | 1 | Available data sources for hunting. These may be a host monitor, an EDR, a SIEM, a firewall, etc. |


| Type Name    | Type Definition                    | Description                                                                   |
|:-------------|:-----------------------------------|:------------------------------------------------------------------------------|
| **OC2-Data** | ArrayOf(Language-Spec-Types){1..*} | OC2-Data is an array of one or more types defined in the OpenC2 language spec |

**_Type: Language-Spec-Types (Record)_**

| ID | Name                  | Type            | # | Description                                                                                              |
|---:|:----------------------|:----------------|--:|:---------------------------------------------------------------------------------------------------------|
|  1 | **artifact**          | Artifact        | 1 | An array of bytes representing a file-like object or a link to that object.                              |
|  2 | **device**            | Device          | 1 | The properties of a hardware device.                                                                     |
|  3 | **domain_name**       | Domain-Name     | 1 | A network domain name.                                                                                   |
|  4 | **email-address**     | Email-Addr      | 1 | A single email address                                                                                   |
|  5 | **file**              | File            | 1 | Properties of a file.                                                                                    |
|  6 | **hashes**            | Hashes          | 1 | Not used as an entity; use inside File or other attribute of another type. May be used as a query value. |
|  7 | **hostname**          | Hostname        | 1 | Value must be a hostname as defined in [RFC1034], Section 3.1                                            |
|  8 | **idn_domain_name**   | IDN-Domain-Name | 1 | An internationalized domain name.                                                                        |
|  9 | **idn_email_address** | IDN-Email-Addr  | 1 | A single internationalized email address.                                                                |
| 10 | **ipv4_address**      | IPv4-Addr       | 1 | IPv4 address as defined in [RFC0791].                                                                    |
| 11 | **ipv6_address**      | IPv6-Addr       | 1 | IPv6 address as defined in [RFC8200].                                                                    |
| 12 | **ipv4_network**      | IPv4-Net        | 1 | IPv4 network targeted by hunt activity.                                                                  |
| 13 | **ipv6_network**      | IPv6-Net        | 1 | IPv6 network targeted by hunt activity.                                                                  |
| 14 | **ipv4_connection**   | IPv4-Connection | 1 | A 5-tuple of source and destination IPv4 address ranges, source and destination ports, and protocol.     |
| 15 | **ipv6_connection**   | IPv6-Connection | 1 | A 5-tuple of source and destination IPv6 address ranges, source and destination ports, and protocol.     |
| 16 | **iri**               | IRI             | 1 | An internationalized resource identifier (IRI).                                                          |
| 17 | **mac_address**       | MAC-Addr        | 1 | A Media Access Control (MAC) address - EUI-48 or EUI-64 as defined in [EUI].                             |
| 18 | **port**              | Port            | 1 | Transport Protocol Port Number, [RFC6335]                                                                |
| 19 | **process**           | Process         | 1 | Common properties of an instance of a computer program as executed on an operating system.               |
| 20 | **uri**               | URI             | 1 | A uniform resource identifier (URI).                                                                     |

**_Type: Artifact (Record{1..*})_**

| ID | Name          | Type    | # | Description                                                                        |
|---:|:--------------|:--------|--:|:-----------------------------------------------------------------------------------|
|  1 | **mime_type** | String  | 1 | Permitted values specified in the IANA Media Types registry, [[RFC6838]](#rfc6838) |
|  2 | **payload**   | Payload | 1 | Choice of literal content or URL                                                   |
|  3 | **hashes**    | Hashes  | 1 | Hashes of the payload content                                                      |

**_Type: Device (Map{1..*})_**

| ID | Name             | Type         | # | Description                                                                             |
|---:|:-----------------|:-------------|--:|:----------------------------------------------------------------------------------------|
|  1 | **hostname**     | Hostname     | 1 | A hostname that can be used to connect to this device over a network                    |
|  2 | **idn_hostname** | IDN-Hostname | 1 | An internationalized hostname that can be used to connect to this device over a network |
|  3 | **device_id**    | String       | 1 | An identifier that refers to this device within an inventory or management system       |


| Type Name       | Type Definition  | Description                        |
|:----------------|:-----------------|:-----------------------------------|
| **Domain-Name** | String /hostname | [[RFC1034]](#rfc1034), Section 3.5 |


| Type Name      | Type Definition | Description                                         |
|:---------------|:----------------|:----------------------------------------------------|
| **Email-Addr** | String /email   | Email address, [[RFC5322]](#rfc5322), Section 3.4.1 |

**_Type: File (Map{1..*})_**

| ID | Name       | Type   | # | Description                                                      |
|---:|:-----------|:-------|--:|:-----------------------------------------------------------------|
|  1 | **name**   | String | 1 | The name of the file as defined in the file system               |
|  2 | **path**   | String | 1 | The absolute path to the location of the file in the file system |
|  3 | **hashes** | Hashes | 1 | One or more cryptographic hash codes of the file contents        |


| Type Name           | Type Definition      | Description                                                            |
|:--------------------|:---------------------|:-----------------------------------------------------------------------|
| **IDN-Domain-Name** | String /idn-hostname | Internationalized Domain Name, [[RFC5890]](#rfc5890), Section 2.3.2.3. |


| Type Name          | Type Definition   | Description                                            |
|:-------------------|:------------------|:-------------------------------------------------------|
| **IDN-Email-Addr** | String /idn-email | Internationalized email address, [[RFC6531]](#rfc6531) |

**_Type: IPv4-Net (Array /ipv4-net)_**

| ID | Type      | # | Description                                                             |
|---:|:----------|--:|:------------------------------------------------------------------------|
|  1 | IPv4-Addr | 1 | None:: IPv4 address as defined in [[RFC0791]](#rfc0791)                 |
|  2 | Integer   | 1 | None:: CIDR prefix-length. If omitted, refers to a single host address. |

**_Type: IPv4-Connection (Record{1..*})_**

| ID | Name         | Type        | # | Description                                                               |
|---:|:-------------|:------------|--:|:--------------------------------------------------------------------------|
|  1 | **src_addr** | IPv4-Net    | 1 | IPv4 source address range                                                 |
|  2 | **src_port** | Port        | 1 | source service per [[RFC6335]](#rfc6335)                                  |
|  3 | **dst_addr** | IPv4-Net    | 1 | IPv4 destination address range                                            |
|  4 | **dst_port** | Port        | 1 | destination service per [[RFC6335]](#rfc6335)                             |
|  5 | **protocol** | L4-Protocol | 1 | layer 4 protocol (e.g., TCP) - see [Section 3.4.2.10](#34210-l4-protocol) |

**_Type: IPv6-Net (Array /ipv6-net)_**

| ID | Type      | # | Description                                                        |
|---:|:----------|--:|:-------------------------------------------------------------------|
|  1 | IPv6-Addr | 1 | None:: IPv6 address as defined in [[RFC8200]](#rfc8200)            |
|  2 | Integer   | 1 | None:: prefix length. If omitted, refers to a single host address. |

**_Type: IPv6-Connection (Record{1..*})_**

| ID | Name         | Type        | # | Description                                                           |
|---:|:-------------|:------------|--:|:----------------------------------------------------------------------|
|  1 | **src_addr** | IPv6-Net    | 1 | IPv6 source address range                                             |
|  2 | **src_port** | Port        | 1 | source service per [[RFC6335]](#rfc6335)                              |
|  3 | **dst_addr** | IPv6-Net    | 1 | IPv6 destination address range                                        |
|  4 | **dst_port** | Port        | 1 | destination service per [[RFC6335]](#rfc6335)                         |
|  5 | **protocol** | L4-Protocol | 1 | layer 4 protocol (e.g., TCP) - [Section 3.4.2.10](#34210-l4-protocol) |


| Type Name | Type Definition | Description                                                   |
|:----------|:----------------|:--------------------------------------------------------------|
| **IRI**   | String /iri     | Internationalized Resource Identifier, [[RFC3987]](#rfc3987). |


| Type Name    | Type Definition | Description                                                                                               |
|:-------------|:----------------|:----------------------------------------------------------------------------------------------------------|
| **MAC-Addr** | Binary /eui     | Media Access Control / Extended Unique Identifier address - EUI-48 or EUI-64 as defined in [[EUI]](#eui). |

**_Type: Process (Map{1..*})_**

| ID | Name             | Type        | # | Description                                                                          |
|---:|:-----------------|:------------|--:|:-------------------------------------------------------------------------------------|
|  1 | **pid**          | Process$Pid | 1 | Process ID of the process                                                            |
|  2 | **name**         | String      | 1 | Name of the process                                                                  |
|  3 | **cwd**          | String      | 1 | Current working directory of the process                                             |
|  4 | **executable**   | File        | 1 | Executable that was executed to start the process                                    |
|  5 | **parent**       | Process$pid | 1 | Process that spawned this one                                                        |
|  6 | **command_line** | String      | 1 | The full command line invocation used to start this process, including all arguments |


| Type Name | Type Definition | Description                                         |
|:----------|:----------------|:----------------------------------------------------|
| **URI**   | String /uri     | Uniform Resource Identifier, [[RFC3986]](#rfc3986). |

**_Type: Hashes (Map{1..*})_**

| ID | Name       | Type          | # | Description                                     |
|---:|:-----------|:--------------|--:|:------------------------------------------------|
|  1 | **md5**    | Hashes$Md5    | 1 | MD5 hash as defined in [[RFC1321]](#rfc1321)    |
|  2 | **sha1**   | Hashes$Sha1   | 1 | SHA1 hash as defined in [[RFC6234]](#rfc6234)   |
|  3 | **sha256** | Hashes$Sha256 | 1 | SHA256 hash as defined in [[RFC6234]](#rfc6234) |


| Type Name    | Type Definition  | Description                                              |
|:-------------|:-----------------|:---------------------------------------------------------|
| **Hostname** | String /hostname | Internet host name as specified in [[RFC1123]](#rfc1123) |


| Type Name        | Type Definition      | Description                                                                                  |
|:-----------------|:---------------------|:---------------------------------------------------------------------------------------------|
| **IDN-Hostname** | String /idn-hostname | Internationalized Internet host name as specified in [[RFC5890]](#rfc5890), Section 2.3.2.3. |


| Type Name     | Type Definition   | Description                                             |
|:--------------|:------------------|:--------------------------------------------------------|
| **IPv4-Addr** | Binary /ipv4-addr | 32 bit IPv4 address as defined in [[RFC0791]](#rfc0791) |


| Type Name     | Type Definition   | Description                                              |
|:--------------|:------------------|:---------------------------------------------------------|
| **IPv6-Addr** | Binary /ipv6-addr | 128 bit IPv6 address as defined in [[RFC8200]](#rfc8200) |


| Type Name | Type Definition   | Description                                           |
|:----------|:------------------|:------------------------------------------------------|
| **Port**  | Integer{0..65535} | Transport Protocol Port Number, [[RFC6335]](#rfc6335) |

**_Type: AP-Specifiers (Map{1..*})_**

| ID | Name | Type | # | Description |
|---:|:-----|:-----|--:|:------------|

**_Type: Huntflow-Specifiers (Map)_**

| ID | Name              | Type                | # | Description                                                             |
|---:|:------------------|:--------------------|--:|:------------------------------------------------------------------------|
|  1 | **path**          | String              | 1 | Return huntflows at and below this filesystem location (absolute path). |
|  2 | **tags**          | Tags                | 1 | Return huntflows with these keywords.                                   |
|  3 | **arg_types**     | Specified-Arg-Types | 1 | Return huntflows that take these argument types.                        |
|  4 | **arg_names**     | Specified-Arg-Names | 1 | Return huntflows that take these argument types.                        |
|  5 | **format_types**  | Return-Type         | 1 | Return huntflows that produce these output types.                       |
|  6 | **return_format** | Huntflow-Sections   | 1 | For each huntflow returned, include these data items.                   |


| Type Name               | Type Definition   | Description                                      |
|:------------------------|:------------------|:-------------------------------------------------|
| **Specified-Arg-Types** | ArrayOf(Arg-Type) | Return huntflows that take these argument types. |


| Type Name               | Type Definition   | Description                                            |
|:------------------------|:------------------|:-------------------------------------------------------|
| **Specified-Arg-Names** | ArrayOf(Arg-Name) | Return huntflows that take arguments with these names. |

**_Type: AP-Results (Map{1..*})_**

| ID | Name              | Type                     | # | Description                                              |
|---:|:------------------|:-------------------------|--:|:---------------------------------------------------------|
|  1 | **huntflow_info** | Ap-results$Huntflow-info | 1 | Structured data returned by Query: Huntflows.            |
|  2 | **datasources**   | Datasource-Array         | 1 | Datasource names and info returned by Query Datasources. |
|  3 | **inv_returns**   | Inv-Returns              | 1 | STIX SCO object returns                                  |


| Type Name       | Type Definition           | Description                                       |
|:----------------|:--------------------------|:--------------------------------------------------|
| **Inv-Returns** | ArrayOf(Inv-Return){1..*} | Array of returns from threat hunt investigations. |

**_Type: Inv-Return (Record)_**

| ID | Name               | Type                           | # | Description                         |
|---:|:-------------------|:-------------------------------|--:|:------------------------------------|
|  1 | **string_returns** | Inv-return$String-returns      | 1 | String return from an investigation |
|  2 | **stix_sco**       | STIX-Cybersecurity-Observables | 1 | STIX SCO object returns             |


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

| ID | Name                | Type      | # | Description                        |
|---:|:--------------------|:----------|--:|:-----------------------------------|
|  1 | **hunt_start_time** | timestamp | 1 | Start time, as a STIX time string. |
|  2 | **hunt_stop_time**  | timestamp | 1 | Stop time, as a STIX time string.  |

**_Type: Timerange-Rel (Record{2..*})_**

| ID | Name          | Type          | # | Description                                                |
|---:|:--------------|:--------------|--:|:-----------------------------------------------------------|
|  1 | **number**    | Integer{0..*} | 1 | Number of specified Time Units used in Relative Timerange. |
|  2 | **time_unit** | Time-Unit     | 1 | Time Unit Keywords.                                        |

**_Type: Return-Type (Record{2..*})_**

| ID | Name         | Type     | # | Description                                      |
|---:|:-------------|:---------|--:|:-------------------------------------------------|
|  1 | **var_name** | Arg-Name | 1 | Variable name to be returned by use of Huntflow. |
|  2 | **var_type** | Arg-Type | 1 | Type of data to be returned by use of Huntflow.  |

**_Type: Datasource (Record{1..*})_**

| ID | Name        | Type   | # | Description                                                 |
|---:|:------------|:-------|--:|:------------------------------------------------------------|
|  1 | **ds_name** | String | 1 | Name of a Datasource used by a Huntflow in Kestrel runtime. |
|  2 | **ds_tags** | Tags   | 1 | Tags applied to a Datasource for search or filter purposes. |


| Type Name             | Type Definition           | Description                                           |
|:----------------------|:--------------------------|:------------------------------------------------------|
| **Huntflow-Sections** | ArrayOf(Huntflow-Section) | For each huntflow returned, include these data items. |

**_Type: Huntflow-Section (Enumerated)_**

| ID | Name                 | Description                                                                                           |
|---:|:---------------------|:------------------------------------------------------------------------------------------------------|
|  1 | **path**             | Specifies the return should include the path to each Huntflow specified by the query conditions.      |
|  2 | **uniqueId**         | Specifies the return should include the ID of each Huntflow specified by the query conditions.        |
|  3 | **version**          | Specifies the return should include the ID of each Huntflow specified by the query conditions.        |
|  4 | **args_required**    | Specifies the returned data should include the required arguments for the available Huntflows.        |
|  5 | **expected_returns** | Specifies the returned data should include the expected returns for the available Huntflows.          |
|  6 | **script**           | Specifies the returned data should include the full text of the Huntflow for each available Huntflow. |

**_Type: Huntflow-Info (Record{1..*})_**

| ID | Name                 | Type            | # | Description                                           |
|---:|:---------------------|:----------------|--:|:------------------------------------------------------|
|  1 | **path**             | String          | 1 | Path used to identify a Huntflow in place of a name.  |
|  2 | **uniqueId**         | Integer{0..*}   | 1 | Unique ID associated with a specified Huntflow.       |
|  3 | **version**          | String          | 1 | Unique ID associated with a specified Huntflow.       |
|  4 | **args_required**    | Typed-Arguments | 1 | List of arguments used in the specified Huntflow.     |
|  5 | **expected_returns** | Typed-Arguments | 1 | Data returned by the specified Huntflows.             |
|  6 | **script**           | String          | 1 | Text of Hunt logic implemented by specified Huntflow. |


| Type Name            | Type Definition     | Description                                                  |
|:---------------------|:--------------------|:-------------------------------------------------------------|
| **Datasource-Array** | ArrayOf(Datasource) | An Array of Datasources, with multiple uses in Threathunting |


| Type Name | Type Definition | Description                                 |
|:----------|:----------------|:--------------------------------------------|
| **Tags**  | ArrayOf(String) | Tags applied for search or filter purposes. |


| Type Name           | Type Definition           | Description                                           |
|:--------------------|:--------------------------|:------------------------------------------------------|
| **Typed-Arguments** | MapOf(Arg-Name, Arg-Type) | Argument names and types tied to a specific Huntflow. |


| Type Name    | Type Definition | Description                                                                                                                                                                         |
|:-------------|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Arg-Type** | String          | Argument types used by a Huntflow. Follow STIX naming conventions, with lowercase characters and hyphens replacing spaces. Common types include process, file, and network-traffic. |


| Type Name    | Type Definition | Description                                                                                                                |
|:-------------|:----------------|:---------------------------------------------------------------------------------------------------------------------------|
| **Arg-Name** | String          | Argument names used by a Huntflow. Follow C variable naming conventions. Examples include name, src_port, and x_unique_id. |


| Type Name                          | Type Definition | Description                                              |
|:-----------------------------------|:----------------|:---------------------------------------------------------|
| **STIX-Cybersecurity-Observables** | ArrayOf(SCO)    | An Array of Cybersecurity Observables in STIX formatting |

**_Type: SCO (Choice)_**

| ID | Name                     | Type                 | # | Description |
|---:|:-------------------------|:---------------------|--:|:------------|
|  1 | **Artifact**             | artifact             | 1 |             |
|  2 | **Autonomous-System**    | autonomous-system    | 1 |             |
|  3 | **Directory**            | directory            | 1 |             |
|  4 | **Domain-Name**          | domain-name          | 1 |             |
|  5 | **Email-Addr**           | email-addr           | 1 |             |
|  6 | **Email-Message**        | email-message        | 1 |             |
|  7 | **File**                 | file                 | 1 |             |
|  8 | **IPv4-Addr**            | ipv4-addr            | 1 |             |
|  9 | **IPv6-Addr**            | ipv6-addr            | 1 |             |
| 10 | **Mac-Addr**             | mac-addr             | 1 |             |
| 11 | **Mutex**                | mutex                | 1 |             |
| 12 | **Network-Traffic**      | network-traffic      | 1 |             |
| 13 | **Process**              | process              | 1 |             |
| 14 | **Software**             | software             | 1 |             |
| 15 | **URL**                  | url                  | 1 |             |
| 16 | **User-Account**         | user-account         | 1 |             |
| 17 | **Windows-Registry-Key** | windows-registry-key | 1 |             |
| 18 | **X509-Certificate**     | x509-certificate     | 1 |             |

**_Type: artifact (Record)_**

| ID | Name                     | Type                      | # | Description                                                                                                                              |
|---:|:-------------------------|:--------------------------|--:|:-----------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                 | Artifact$Type             | 1 | The value of this property MUST be `artifact`.                                                                                           |
|  2 | **id**                   | Artifact$Id               | 1 |                                                                                                                                          |
|  3 | **mime_type**            | Artifact$Mime-type        | 1 | The value of this property MUST be a valid MIME type as specified in the IANA Media Types registry.                                      |
|  4 | **payload_bin**          | Binary                    | 1 | Specifies the binary data contained in the artifact as a base64-encoded string.                                                          |
|  5 | **url**                  | url                       | 1 | The value of this property MUST be a valid URL that resolves to the unencoded content.                                                   |
|  6 | **hashes**               | Artifact$Hashes           | 1 | Specifies a dictionary of hashes for the contents of the url or the payload_bin. This MUST be provided when the url property is present. |
|  7 | **encryption_algorithm** | encryption_algorithm_enum | 1 | If the artifact is encrypted, specifies the type of encryption algorithm the binary data  (either via payload_bin or url) is encoded in. |
|  8 | **decryption_key**       | String                    | 1 | Specifies the decryption key for the encrypted binary data (either via payload_bin or url).                                              |
|  9 | **spec_version**         | spec_version              | 1 |                                                                                                                                          |
| 10 | **object_marking_refs**  | object_marking_refs       | 1 |                                                                                                                                          |
| 11 | **granular_markings**    | granular_markings         | 1 |                                                                                                                                          |
| 12 | **defanged**             | defanged                  | 1 |                                                                                                                                          |
| 13 | **core_extensions**      | extensions                | 1 |                                                                                                                                          |

**_Type: autonomous-system (Record)_**

| ID | Name                    | Type                   | # | Description                                                                                                                |
|---:|:------------------------|:-----------------------|--:|:---------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Autonomous-system$Type | 1 |                                                                                                                            |
|  2 | **id**                  | Autonomous-system$Id   | 1 |                                                                                                                            |
|  3 | **number**              | Integer{0..*}          | 1 | Specifies the number assigned to the AS. Such assignments are typically performed by a Regional Internet Registries (RIR). |
|  4 | **name**                | String                 | 1 | Specifies the name of the AS.                                                                                              |
|  5 | **rir**                 | String                 | 1 | Specifies the name of the Regional Internet Registry (RIR) that assigned the number to the AS.                             |
|  6 | **spec_version**        | spec_version           | 1 |                                                                                                                            |
|  7 | **object_marking_refs** | object_marking_refs    | 1 |                                                                                                                            |
|  8 | **granular_markings**   | granular_markings      | 1 |                                                                                                                            |
|  9 | **defanged**            | defanged               | 1 |                                                                                                                            |
| 10 | **core_extensions**     | extensions             | 1 |                                                                                                                            |

**_Type: directory (Record)_**

| ID | Name                    | Type                    | # | Description                                                                                           |
|---:|:------------------------|:------------------------|--:|:------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Directory$Type          | 1 |                                                                                                       |
|  2 | **id**                  | Directory$Id            | 1 |                                                                                                       |
|  3 | **path**                | String                  | 1 | Specifies the path, as originally observed, to the directory on the file system.                      |
|  4 | **path_enc**            | Directory$Path-enc      | 1 | Specifies the observed encoding for the path.                                                         |
|  5 | **ctime**               | timestamp               | 1 | Specifies the date/time the directory was created.                                                    |
|  6 | **mtime**               | timestamp               | 1 | Specifies the date/time the directory was last written to/modified.                                   |
|  7 | **atime**               | timestamp               | 1 | Specifies the date/time the directory was last accessed.                                              |
|  8 | **contains_refs**       | Directory$Contains-refs | 1 | Specifies a list of references to other File and/or Directory Objects contained within the directory. |
|  9 | **spec_version**        | spec_version            | 1 |                                                                                                       |
| 10 | **object_marking_refs** | object_marking_refs     | 1 |                                                                                                       |
| 11 | **granular_markings**   | granular_markings       | 1 |                                                                                                       |
| 12 | **defanged**            | defanged                | 1 |                                                                                                       |
| 13 | **core_extensions**     | extensions              | 1 |                                                                                                       |

**_Type: domain-name (Record)_**

| ID | Name                    | Type                         | # | Description                                                                                                  |
|---:|:------------------------|:-----------------------------|--:|:-------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Domain-name$Type             | 1 |                                                                                                              |
|  2 | **id**                  | Domain-name$Id               | 1 |                                                                                                              |
|  3 | **domain_name**         | String                       | 1 | Specifies the value of the domain name.                                                                      |
|  4 | **resolves_to_refs**    | Domain-name$Resolves-to-refs | 1 | Specifies a list of references to one or more IP addresses or domain names that the domain name resolves to. |
|  5 | **spec_version**        | spec_version                 | 1 |                                                                                                              |
|  6 | **object_marking_refs** | object_marking_refs          | 1 |                                                                                                              |
|  7 | **granular_markings**   | granular_markings            | 1 |                                                                                                              |
|  8 | **defanged**            | defanged                     | 1 |                                                                                                              |
|  9 | **core_extensions**     | extensions                   | 1 |                                                                                                              |

**_Type: email-addr (Record)_**

| ID | Name                    | Type                | # | Description                                                                                                      |
|---:|:------------------------|:--------------------|--:|:-----------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Email-addr$Type     | 1 |                                                                                                                  |
|  2 | **id**                  | Email-addr$Id       | 1 |                                                                                                                  |
|  3 | **email_address**       | String              | 1 | Specifies a single email address. This MUST not include the display name.                                        |
|  4 | **display_name**        | String              | 1 | Specifies a single email display name, i.e., the name that is displayed to the human user of a mail application. |
|  5 | **belongs_to_ref**      | String              | 1 | Specifies the user account that the email address belongs to, as a reference to a User Account Object.           |
|  6 | **spec_version**        | spec_version        | 1 |                                                                                                                  |
|  7 | **object_marking_refs** | object_marking_refs | 1 |                                                                                                                  |
|  8 | **granular_markings**   | granular_markings   | 1 |                                                                                                                  |
|  9 | **defanged**            | defanged            | 1 |                                                                                                                  |
| 10 | **core_extensions**     | extensions          | 1 |                                                                                                                  |

**_Type: email-message (Record)_**

| ID | Name                         | Type                                   | # | Description                                                                                                                        |
|---:|:-----------------------------|:---------------------------------------|--:|:-----------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                     | Email-message$Type                     | 1 |                                                                                                                                    |
|  2 | **id**                       | Email-message$Id                       | 1 |                                                                                                                                    |
|  3 | **date**                     | timestamp                              | 1 | Specifies the date/time that the email message was sent.                                                                           |
|  4 | **content_type**             | String                                 | 1 | Specifies the value of the 'Content-Type' header of the email message.                                                             |
|  5 | **from_ref**                 | String                                 | 1 | Specifies the value of the 'From:' header of the email message.                                                                    |
|  6 | **sender_ref**               | spec_version                           | 1 | Specifies the value of the 'From' field of the email message.                                                                      |
|  7 | **to_refs**                  | Email-message$To-refs                  | 1 | Specifies the mailboxes that are 'To:' recipients of the email message.                                                            |
|  8 | **cc_refs**                  | Email-message$Cc-refs                  | 1 | Specifies the mailboxes that are 'CC:' recipients of the email message.                                                            |
|  9 | **bcc_refs**                 | Email-message$Bcc-refs                 | 1 | Specifies the mailboxes that are 'BCC:' recipients of the email message.                                                           |
| 10 | **message_id**               | String                                 | 1 | Specifies the Message-ID field of the email message.                                                                               |
| 11 | **subject**                  | String                                 | 1 | Specifies the subject of the email message.                                                                                        |
| 12 | **received_lines**           | Email-message$Received-lines           | 1 | Specifies one or more Received header fields that may be included in the email headers.                                            |
| 13 | **additional_header_fields** | Email-message$Additional-header-fields | 1 | Specifies any other header fields found in the email message, as a dictionary.                                                     |
| 14 | **raw_email_ref**            | String                                 | 1 | Specifies the raw binary contents of the email message, including both the headers and body, as a reference to an Artifact Object. |
| 15 | **is_multipart**             | Boolean                                | 1 | Indicates whether the email body contains multiple MIME parts.                                                                     |
| 16 | **body_multipart**           | Email-message$Body-multipart           | 1 | Specifies a list of the MIME parts that make up the email body. This property MAY only be used if is_multipart is true.            |
| 17 | **body**                     | String                                 | 1 | Specifies a string containing the email body. This field MAY only be used if is_multipart is false.                                |
| 18 | **spec_version**             | spec_version                           | 1 |                                                                                                                                    |
| 19 | **object_marking_refs**      | object_marking_refs                    | 1 |                                                                                                                                    |
| 20 | **granular_markings**        | granular_markings                      | 1 |                                                                                                                                    |
| 21 | **defanged**                 | defanged                               | 1 |                                                                                                                                    |
| 22 | **core_extensions**          | extensions                             | 1 |                                                                                                                                    |

**_Type: file (Record)_**

| ID | Name                    | Type                | # | Description                                                                                                                                                                                |
|---:|:------------------------|:--------------------|--:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | File$Type           | 1 | The value of this property MUST be `file`.                                                                                                                                                 |
|  2 | **id**                  | File$Id             | 1 |                                                                                                                                                                                            |
|  3 | **extensions**          | String              | 1 | The File Object defines the following extensions. In addition to these, producers MAY create their own. Extensions: ntfs-ext, raster-image-ext, pdf-ext, archive-ext, windows-pebinary-ext |
|  4 | **hashes**              | File$Hashes         | 1 | Specifies a dictionary of hashes for the file.                                                                                                                                             |
|  5 | **size**                | File$Size           | 1 | Specifies the size of the file, in bytes, as a non-negative integer.                                                                                                                       |
|  6 | **name**                | String              | 1 |                                                                                                                                                                                            |
|  7 | **name_enc**            | File$Name-enc       | 1 | Specifies the observed encoding for the name of the file.                                                                                                                                  |
|  8 | **magic_number_hex**    | Hex                 | 1 | Specifies the hexadecimal constant ('magic number') associated with a specific file format that corresponds to the file, if applicable.                                                    |
|  9 | **mime_type**           | String              | 1 | Specifies the MIME type name specified for the file, e.g., 'application/msword'.                                                                                                           |
| 10 | **ctime**               | timestamp           | 1 | Specifies the date/time the file was created.                                                                                                                                              |
| 11 | **mtime**               | timestamp           | 1 | Specifies the date/time the file was last written to/modified.                                                                                                                             |
| 12 | **atime**               | timestamp           | 1 | Specifies the date/time the file was last accessed.                                                                                                                                        |
| 13 | **parent_directory**    | String              | 1 | Specifies the parent directory of the file, as a reference to a Directory Object.                                                                                                          |
| 14 | **contains_refs**       | File$Contains-refs  | 1 | Specifies a list of references to other Observable Objects contained within the file.                                                                                                      |
| 15 | **content_ref**         | String              | 1 | Specifies the content of the file, represented as an Artifact Object.                                                                                                                      |
| 16 | **spec_version**        | spec_version        | 1 |                                                                                                                                                                                            |
| 17 | **object_marking_refs** | object_marking_refs | 1 |                                                                                                                                                                                            |
| 18 | **granular_markings**   | granular_markings   | 1 |                                                                                                                                                                                            |
| 19 | **defanged**            | defanged            | 1 |                                                                                                                                                                                            |
| 20 | **core_extensions**     | extensions          | 1 |                                                                                                                                                                                            |

**_Type: ipv4-addr (Record)_**

| ID | Name                    | Type                       | # | Description |
|---:|:------------------------|:---------------------------|--:|:------------|
|  1 | **type**                | Ipv4-addr$Type             | 1 |             |
|  2 | **id**                  | Ipv4-addr$Id               | 1 |             |
|  3 | **ipv4_addr**           | Ipv4-addr$Ipv4-addr        | 1 |             |
|  4 | **resolves_to_refs**    | Ipv4-addr$Resolves-to-refs | 1 |             |
|  5 | **belongs_to_refs**     | Ipv4-addr$Belongs-to-refs  | 1 |             |
|  6 | **spec_version**        | spec_version               | 1 |             |
|  7 | **object_marking_refs** | object_marking_refs        | 1 |             |
|  8 | **granular_markings**   | granular_markings          | 1 |             |
|  9 | **defanged**            | defanged                   | 1 |             |
| 10 | **core_extensions**     | extensions                 | 1 |             |

**_Type: ipv6-addr (Record)_**

| ID | Name                    | Type                       | # | Description                                                                                                                   |
|---:|:------------------------|:---------------------------|--:|:------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Ipv6-addr$Type             | 1 |                                                                                                                               |
|  2 | **id**                  | Ipv6-addr$Id               | 1 |                                                                                                                               |
|  3 | **ipv6_addr**           | Ipv6-addr$Ipv6-addr        | 1 | The IPv6 Address Object represents one or more IPv6 addresses expressed using CIDR notation.                                  |
|  4 | **resolves_to_refs**    | Ipv6-addr$Resolves-to-refs | 1 | Specifies a list of references to one or more Layer 2 Media Access Control (MAC) addresses that the IPv6 address resolves to. |
|  5 | **belongs_to_refs**     | Ipv6-addr$Belongs-to-refs  | 1 | Specifies a reference to one or more autonomous systems (AS) that the IPv6 address belongs to.                                |
|  6 | **spec_version**        | spec_version               | 1 |                                                                                                                               |
|  7 | **object_marking_refs** | object_marking_refs        | 1 |                                                                                                                               |
|  8 | **granular_markings**   | granular_markings          | 1 |                                                                                                                               |
|  9 | **defanged**            | defanged                   | 1 |                                                                                                                               |
| 10 | **core_extensions**     | extensions                 | 1 |                                                                                                                               |

**_Type: mac-addr (Record)_**

| ID | Name                    | Type                       | # | Description                                                        |
|---:|:------------------------|:---------------------------|--:|:-------------------------------------------------------------------|
|  1 | **type**                | Mac-addr$Type              | 1 |                                                                    |
|  2 | **id**                  | Mac-addr$Id                | 1 |                                                                    |
|  3 | **mac_address_value**   | Mac-addr$Mac-address-value | 1 | Specifies one or more mac addresses expressed using CIDR notation. |
|  4 | **spec_version**        | spec_version               | 1 |                                                                    |
|  5 | **object_marking_refs** | object_marking_refs        | 1 |                                                                    |
|  6 | **granular_markings**   | granular_markings          | 1 |                                                                    |
|  7 | **defanged**            | defanged                   | 1 |                                                                    |
|  8 | **core_extensions**     | extensions                 | 1 |                                                                    |

**_Type: mutex (Record)_**

| ID | Name                    | Type                | # | Description                             |
|---:|:------------------------|:--------------------|--:|:----------------------------------------|
|  1 | **type**                | Mutex$Type          | 1 |                                         |
|  2 | **id**                  | Mutex$Id            | 1 |                                         |
|  3 | **name**                | String              | 1 | Specifies the name of the mutex object. |
|  4 | **spec_version**        | spec_version        | 1 |                                         |
|  5 | **object_marking_refs** | object_marking_refs | 1 |                                         |
|  6 | **granular_markings**   | granular_markings   | 1 |                                         |
|  7 | **defanged**            | defanged            | 1 |                                         |
|  8 | **core_extensions**     | extensions          | 1 |                                         |

**_Type: network-traffic (Record)_**

| ID | Name                    | Type                                  | # | Description                                                                                                                                                            |
|---:|:------------------------|:--------------------------------------|--:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Network-traffic$Type                  | 1 |                                                                                                                                                                        |
|  2 | **id**                  | Network-traffic$Id                    | 1 |                                                                                                                                                                        |
|  3 | **extensions**          | network_traffic_extensions_dictionary | 1 | The Network Traffic Object defines the following extensions. In addition to these, producers MAY create their own. Extensions: http-ext, tcp-ext, icmp-ext, socket-ext |
|  4 | **start**               | Network-traffic$Start                 | 1 | Specifies the date/time the network traffic was initiated, if known.                                                                                                   |
|  5 | **stop**                | Network-traffic$Stop                  | 1 | Specifies the date/time the network traffic ended, if known.                                                                                                           |
|  6 | **is_active**           | Boolean                               | 1 | Indicates whether the network traffic is still ongoing.                                                                                                                |
|  7 | **src_port**            | Network-traffic$Src-port              | 1 | Specifies the source port used in the network traffic, as an integer. The port value MUST be in the range of 0 - 65535.                                                |
|  8 | **dst_port**            | Network-traffic$Dst-port              | 1 | Specifies the destination port used in the network traffic, as an integer. The port value MUST be in the range of 0 - 65535.                                           |
|  9 | **protocols**           | Network-traffic$Protocols             | 1 | Specifies the protocols observed in the network traffic, along with their corresponding state.                                                                         |
| 10 | **src_byte_count**      | Integer{0..*}                         | 1 | Specifies the number of bytes, as a positive integer, sent from the source to the destination.                                                                         |
| 11 | **dst_byte_count**      | Integer{0..*}                         | 1 | Specifies the number of bytes, as a positive integer, sent from the destination to the source.                                                                         |
| 12 | **src_packets**         | Integer{0..*}                         | 1 | Specifies the number of packets, as a positive integer, sent from the source to the destination.                                                                       |
| 13 | **dst_packets**         | Integer{0..*}                         | 1 | Specifies the number of packets, as a positive integer, sent from the destination to the source.                                                                       |
| 14 | **ipfix**               | ipfix_choice                          | 1 | Specifies any IP Flow Information Export (IPFIX) data for the traffic.                                                                                                 |
| 15 | **src_payload_ref**     | String                                | 1 | Specifies the bytes sent from the source to the destination.                                                                                                           |
| 16 | **dst_payload_ref**     | String                                | 1 | Specifies the bytes sent from the source to the destination.                                                                                                           |
| 17 | **encapsulates_refs**   | Network-traffic$Encapsulates-refs     | 1 | Specifies the bytes sent from the source to the destination.                                                                                                           |
| 18 | **encapsulated_by_ref** | String                                | 1 | Links to another network-traffic object which encapsulates this object.                                                                                                |
| 19 | **spec_version**        | spec_version                          | 1 |                                                                                                                                                                        |
| 20 | **object_marking_refs** | object_marking_refs                   | 1 |                                                                                                                                                                        |
| 21 | **granular_markings**   | granular_markings                     | 1 |                                                                                                                                                                        |
| 22 | **defanged**            | defanged                              | 1 |                                                                                                                                                                        |
| 23 | **core_extensions**     | extensions                            | 1 |                                                                                                                                                                        |

**_Type: process (Record)_**

| ID | Name                       | Type                          | # | Description                                                                                                                                                                         |
|---:|:---------------------------|:------------------------------|--:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                   | Process$Type                  | 1 |                                                                                                                                                                                     |
|  2 | **id**                     | Process$Id                    | 1 |                                                                                                                                                                                     |
|  3 | **extensions**             | process_extensions_dictionary | 1 |                                                                                                                                                                                     |
|  4 | **is_hidden**              | Boolean                       | 1 |                                                                                                                                                                                     |
|  5 | **pid**                    | Integer{0..*}                 | 1 | Specifies the Process ID, or PID, of the process.                                                                                                                                   |
|  6 | **created_time**           | timestamp                     | 1 | Specifies the date/time at which the process was created.                                                                                                                           |
|  7 | **cwd**                    | String                        | 1 | Specifies the current working directory of the process.                                                                                                                             |
|  8 | **command_line**           | String                        | 1 | Specifies the full command line used in executing the process, including the process name (which may be specified individually via the binary_ref.name property) and any arguments. |
|  9 | **environment_variables**  | Process$Environment-variables | 1 | Specifies the list of environment variables associated with the process as a dictionary.                                                                                            |
| 10 | **opened_connection_refs** | String                        | 1 | Specifies the list of network connections opened by the process, as a reference to one or more Network Traffic Objects.                                                             |
| 11 | **creator_user_ref**       | Process$Creator-user-ref      | 1 | Specifies the user that created the process, as a reference to a User Account Object.                                                                                               |
| 12 | **image_ref**              | String                        | 1 | Specifies the executable binary that was executed as the process image, as a reference to a File Object.                                                                            |
| 13 | **parent_ref**             | String                        | 1 | Specifies the other process that spawned (i.e. is the parent of) this one, as represented by a Process Object.                                                                      |
| 14 | **child_refs**             | Process$Child-refs            | 1 | Specifies the other processes that were spawned by (i.e. children of) this process, as a reference to one or more other Process Objects.                                            |
| 15 | **spec_version**           | spec_version                  | 1 |                                                                                                                                                                                     |
| 16 | **object_marking_refs**    | object_marking_refs           | 1 |                                                                                                                                                                                     |
| 17 | **granular_markings**      | granular_markings             | 1 |                                                                                                                                                                                     |
| 18 | **defanged**               | defanged                      | 1 |                                                                                                                                                                                     |
| 19 | **core_extensions**        | extensions                    | 1 |                                                                                                                                                                                     |

**_Type: software (Record)_**

| ID | Name                    | Type                | # | Description                                                                                                                                                                      |
|---:|:------------------------|:--------------------|--:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Software$Type       | 1 |                                                                                                                                                                                  |
|  2 | **id**                  | String              | 1 | %^software--                                                                                                                                                                     |
|  3 | **name**                | Software$Name       | 1 | Specifies the name of the software.                                                                                                                                              |
|  4 | **cpe**                 | Software$Cpe        | 1 | Specifies the Common Platform Enumeration (CPE) entry for the software, if available. The value for this property MUST be a CPE v2.3 entry from the official NVD CPE Dictionary. |
|  5 | **swid**                | Software$Swid       | 1 | Specifies the Software Identification (SWID) Tags entry for the software, if available.                                                                                          |
|  6 | **languages**           | Software$Languages  | 1 | Specifies the languages supported by the software. The value of each list member MUST be an ISO 639-2 language code.                                                             |
|  7 | **vendor**              | Software$Vendor     | 1 | Specifies the name of the vendor of the software.                                                                                                                                |
|  8 | **version**             | Software$Version    | 1 | Specifies the version of the software.                                                                                                                                           |
|  9 | **spec_version**        | spec_version        | 1 |                                                                                                                                                                                  |
| 10 | **object_marking_refs** | object_marking_refs | 1 |                                                                                                                                                                                  |
| 11 | **granular_markings**   | granular_markings   | 1 |                                                                                                                                                                                  |
| 12 | **defanged**            | defanged            | 1 |                                                                                                                                                                                  |
| 13 | **core_extensions**     | extensions          | 1 |                                                                                                                                                                                  |

**_Type: user-account (Record)_**

| ID | Name                        | Type                               | # | Description                                                                                                                                                                                                                                                        |
|---:|:----------------------------|:-----------------------------------|--:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                    | User-account$Type                  | 1 | The value of this property MUST be `user-account`.                                                                                                                                                                                                                 |
|  2 | **id**                      | User-account$Id                    | 1 |                                                                                                                                                                                                                                                                    |
|  3 | **user_account_extensions** | user_account_extensions_dictionary | 1 | The User Account Object defines the following extensions. In addition to these, producers MAY create their own. Extensions: unix-account-ext.                                                                                                                      |
|  4 | **user_id**                 | String                             | 1 | Specifies the identifier of the account.                                                                                                                                                                                                                           |
|  5 | **credential**              | String                             | 1 | Specifies a cleartext credential. This is only intended to be used in capturing metadata from malware analysis (e.g., a hard-coded domain administrator password that the malware attempts to use for lateral movement) and SHOULD NOT be used for sharing of PII. |
|  6 | **account_login**           | String                             | 1 | Specifies the account login string, used in cases where the user_id property specifies something other than what a user would type when they login.                                                                                                                |
|  7 | **account_type**            | String                             | 1 | Specifies the type of the account. This is an open vocabulary and values SHOULD come from the account-type-ov vocabulary.                                                                                                                                          |
|  8 | **display_name**            | String                             | 1 | Specifies the display name of the account, to be shown in user interfaces, if applicable.                                                                                                                                                                          |
|  9 | **is_service_account**      | Boolean                            | 1 | Indicates that the account is associated with a network service or system process (daemon), not a specific individual.                                                                                                                                             |
| 10 | **is_privileged**           | Boolean                            | 1 | Specifies that the account has elevated privileges (i.e., in the case of root on Unix or the Windows Administrator account).                                                                                                                                       |
| 11 | **can_escalate_privs**      | Boolean                            | 1 | Specifies that the account has the ability to escalate privileges (i.e., in the case of sudo on Unix or a Windows Domain Admin account).                                                                                                                           |
| 12 | **is_disabled**             | Boolean                            | 1 | Specifies if the account is disabled.                                                                                                                                                                                                                              |
| 13 | **account_created**         | timestamp                          | 1 | Specifies when the account was created.                                                                                                                                                                                                                            |
| 14 | **account_expires**         | timestamp                          | 1 | Specifies the expiration date of the account.                                                                                                                                                                                                                      |
| 15 | **credential_last_changed** | timestamp                          | 1 | Specifies when the account credential was last changed.                                                                                                                                                                                                            |
| 16 | **account_first_login**     | timestamp                          | 1 | Specifies when the account was first accessed.                                                                                                                                                                                                                     |
| 17 | **account_last_login**      | timestamp                          | 1 | Specifies when the account was last accessed.                                                                                                                                                                                                                      |
| 18 | **spec_version**            | spec_version                       | 1 |                                                                                                                                                                                                                                                                    |
| 19 | **object_marking_refs**     | object_marking_refs                | 1 |                                                                                                                                                                                                                                                                    |
| 20 | **granular_markings**       | granular_markings                  | 1 |                                                                                                                                                                                                                                                                    |
| 21 | **defanged**                | defanged                           | 1 |                                                                                                                                                                                                                                                                    |
| 22 | **core_extensions**         | extensions                         | 1 |                                                                                                                                                                                                                                                                    |

**_Type: url (Record)_**

| ID | Name                    | Type                | # | Description                               |
|---:|:------------------------|:--------------------|--:|:------------------------------------------|
|  1 | **type**                | Url$Type            | 1 | The value of this property MUST be `url`. |
|  2 | **id**                  | Url$Id              | 1 |                                           |
|  3 | **url_value**           | Url$Url-value       | 1 | Specifies the value of the URL.           |
|  4 | **spec_version**        | spec_version        | 1 |                                           |
|  5 | **object_marking_refs** | object_marking_refs | 1 |                                           |
|  6 | **granular_markings**   | granular_markings   | 1 |                                           |
|  7 | **defanged**            | defanged            | 1 |                                           |
|  8 | **core_extensions**     | extensions          | 1 |                                           |

**_Type: windows-registry-key (Record)_**

| ID | Name                    | Type                                 | # | Description                                                                                                   |
|---:|:------------------------|:-------------------------------------|--:|:--------------------------------------------------------------------------------------------------------------|
|  1 | **type**                | Windows-registry-key$Type            | 1 | The value of this property MUST be `windows-registry-key`.                                                    |
|  2 | **id**                  | Windows-registry-key$Id              | 1 |                                                                                                               |
|  3 | **key**                 | Windows-registry-key$Key             | 1 | Specifies the full registry key including the hive.                                                           |
|  4 | **registry_values**     | Windows-registry-key$Registry-values | 1 | Specifies the values found under the registry key.                                                            |
|  5 | **modified_time**       | timestamp                            | 1 | Specifies the last date/time that the registry key was modified.                                              |
|  6 | **creator_user_ref**    | String                               | 1 | Specifies a reference to a user account, represented as a User Account Object, that created the registry key. |
|  7 | **number_of_subkeys**   | Integer{0..*}                        | 1 | Specifies the number of subkeys contained under the registry key.                                             |
|  8 | **spec_version**        | spec_version                         | 1 |                                                                                                               |
|  9 | **object_marking_refs** | object_marking_refs                  | 1 |                                                                                                               |
| 10 | **granular_markings**   | granular_markings                    | 1 |                                                                                                               |
| 11 | **defanged**            | defanged                             | 1 |                                                                                                               |
| 12 | **core_extensions**     | extensions                           | 1 |                                                                                                               |

**_Type: x509-certificate (Record)_**

| ID | Name                              | Type                                | # | Description                                                                                                                  |
|---:|:----------------------------------|:------------------------------------|--:|:-----------------------------------------------------------------------------------------------------------------------------|
|  1 | **type**                          | X509-certificate$Type               | 1 | The value of this property MUST be `x509-certificate`.                                                                       |
|  2 | **id**                            | X509-certificate$Id                 | 1 |                                                                                                                              |
|  3 | **is_self_signed**                | Boolean                             | 1 | Specifies whether the certificate is self-signed, i.e., whether it is signed by the same entity whose identity it certifies. |
|  4 | **hashes**                        | X509-certificate$Hashes             | 1 | Specifies any hashes that were calculated for the entire contents of the certificate.                                        |
|  5 | **version**                       | String                              | 1 | Specifies the version of the encoded certificate.                                                                            |
|  6 | **serial_number**                 | String                              | 1 | Specifies the unique identifier for the certificate, as issued by a specific Certificate Authority.                          |
|  7 | **signature_algorithm**           | String                              | 1 | Specifies the name of the algorithm used to sign the certificate.                                                            |
|  8 | **issuer**                        | String                              | 1 | Specifies the name of the Certificate Authority that issued the certificate.                                                 |
|  9 | **validity_not_before**           | timestamp                           | 1 | Specifies the date on which the certificate validity period begins.                                                          |
| 10 | **validity_not_after**            | timestamp                           | 1 | Specifies the date on which the certificate validity period ends.                                                            |
| 11 | **subject**                       | spec_version                        | 1 | Specifies the name of the entity associated with the public key stored in the subject public key field of the certificate.   |
| 12 | **subject_public_key_algorithm**  | String                              | 1 | Specifies the name of the algorithm with which to encrypt data being sent to the subject.                                    |
| 13 | **subject_public_key_modulus**    | String                              | 1 | Specifies the modulus portion of the subject’s public RSA key.                                                               |
| 14 | **subject_public_key_extensions** | Integer{0..*}                       | 1 | Specifies the exponent portion of the subject’s public RSA key, as an integer.                                               |
| 15 | **x509_v3_extensions**            | X509-certificate$X509-v3-extensions | 1 | Specifies any standard X.509 v3 extensions that may be used in the certificate.                                              |
| 16 | **spec_version**                  | spec_version                        | 1 |                                                                                                                              |
| 17 | **object_marking_refs**           | object_marking_refs                 | 1 |                                                                                                                              |
| 18 | **granular_markings**             | granular_markings                   | 1 |                                                                                                                              |
| 19 | **defanged**                      | defanged                            | 1 |                                                                                                                              |
| 20 | **core_extensions**               | extensions                          | 1 |                                                                                                                              |

**_Type: encryption_algorithm_enum (Enumerated)_**

| ID | Name                    | Description |
|---:|:------------------------|:------------|
|  1 | **AES-256-GCM**         |             |
|  2 | **ChaCha20-Poly1305**   |             |
|  3 | **mime-type-indicated** |             |

**_Type: mime-part-type (Record)_**

| ID | Name                    | Type   | # | Description                                                                                                                                                        |
|---:|:------------------------|:-------|--:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **body**                | String | 1 | Specifies the contents of the MIME part if the content_type is not provided OR starts with text/                                                                   |
|  2 | **body_raw_ref**        | String | 1 | Specifies the contents of non-textual MIME parts, that is those whose content_type does not start with text/, as a reference to an Artifact Object or File Object. |
|  3 | **content_type**        | String | 1 | Specifies the value of the 'Content-Type' header field of the MIME part.                                                                                           |
|  4 | **content_disposition** | String | 1 | Specifies the value of the 'Content-Disposition' header field of the MIME part.                                                                                    |


| Type Name                          | Type Definition                        | Description                                                                                                                                                                                   |
|:-----------------------------------|:---------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **email-additional-header-fields** | ArrayOf(email_additional_header_field) | Specifies any other header fields (except for date, received_lines, content_type, from_ref, sender_ref, to_refs, cc_refs, bcc_refs, and subject) found in the email message, as a dictionary. |


| Type Name                         | Type Definition                                                         | Description                                                                                                                                                                                   |
|:----------------------------------|:------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **email_additional_header_field** | MapOf(email_additional_header_fieldname, email_additional_header_value) | Specifies any other header fields (except for date, received_lines, content_type, from_ref, sender_ref, to_refs, cc_refs, bcc_refs, and subject) found in the email message, as a dictionary. |


| Type Name                             | Type Definition                                                                                                        | Description                                                                                                                                                                                   |
|:--------------------------------------|:-----------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **email_additional_header_fieldname** | String (%^((?!((^|, )(date|received_lines|content_type|from_ref|sender_ref|to_refs|cc_refs|bcc_refs|subject))+$).)*$%) | Specifies any other header fields (except for date, received_lines, content_type, from_ref, sender_ref, to_refs, cc_refs, bcc_refs, and subject) found in the email message, as a dictionary. |

**_Type: email_additional_header_value (Choice)_**

| ID | Name             | Type                                       | # | Description |
|---:|:-----------------|:-------------------------------------------|--:|:------------|
|  1 | **String_Value** | Email-additional-header-value$String-value | 1 |             |
|  2 | **String_Array** | Email-additional-header-value$String-array | 1 |             |

**_Type: windows_registry_value_type (Record)_**

| ID | Name                   | Type                   | # | Description                                                                                                                 |
|---:|:-----------------------|:-----------------------|--:|:----------------------------------------------------------------------------------------------------------------------------|
|  1 | **name**               | String                 | 1 | Specifies the name of the registry value. For specifying the default value in a registry key, an empty string MUST be used. |
|  2 | **data**               | String                 | 1 | Specifies the data contained in the registry value.                                                                         |
|  3 | **registry_data_type** | win_registry_data_type | 1 | Specifies the registry (REG_*) data type used in the registry value.                                                        |

**_Type: win_registry_data_type (Enumerated)_**

| ID | Name                               | Description |
|---:|:-----------------------------------|:------------|
|  1 | **REG_NONE**                       |             |
|  2 | **REG_SZ**                         |             |
|  3 | **REG_EXPAND_SZ**                  |             |
|  4 | **REG_BINARY**                     |             |
|  5 | **REG_DWORD**                      |             |
|  6 | **REG_DWORD_BIG_ENDIAN**           |             |
|  7 | **REG_DWORD_LITTLE_ENDIAN**        |             |
|  8 | **REG_LINK**                       |             |
|  9 | **REG_MULTI_SZ**                   |             |
| 10 | **REG_RESOURCE_LIST**              |             |
| 11 | **REG_FULL_RESOURCE_DESCRIPTION**  |             |
| 12 | **REG_RESOURCE_REQUIREMENTS_LIST** |             |
| 13 | **REG_QWORD**                      |             |
| 14 | **REG_INVALID_TYPE**               |             |

**_Type: x509_v3_extensions_type (Record)_**

| ID | Name                                    | Type      | # | Description                                                                                                                                 |
|---:|:----------------------------------------|:----------|--:|:--------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **basic_constraints**                   | String    | 1 | Specifies a multi-valued extension which indicates whether a certificate is a CA certificate.                                               |
|  2 | **name_constraints**                    | String    | 1 | Specifies a namespace within which all subject names in subsequent certificates in a certification path MUST be located.                    |
|  3 | **policy_constraints**                  | String    | 1 | Specifies any constraints on path validation for certificates issued to CAs.                                                                |
|  4 | **key_usage**                           | String    | 1 | Specifies a multi-valued extension consisting of a list of names of the permitted key usages.                                               |
|  5 | **extend_key_usage**                    | String    | 1 | Specifies a list of usages indicating purposes for which the certificate public key can be used for.                                        |
|  6 | **subject_key_identifier**              | String    | 1 | Specifies the identifier that provides a means of identifying certificates that contain a particular public key.                            |
|  7 | **authority_key_identifier**            | String    | 1 | Specifies the identifier that provides a means of identifying the public key corresponding to the private key used to sign a certificate.   |
|  8 | **subject_alternative_name**            | String    | 1 | Specifies the additional identities to be bound to the subject of the certificate.                                                          |
|  9 | **issuer_alternative_name**             | String    | 1 | Specifies the additional identities to be bound to the issuer of the certificate.                                                           |
| 10 | **subject_directory_attributes**        | String    | 1 | Specifies the identification attributes (e.g., nationality) of the subject.                                                                 |
| 11 | **crt_distribution_points**             | String    | 1 | Specifies how CRL information is obtained.                                                                                                  |
| 12 | **inhibit_any_policy**                  | String    | 1 | Specifies the number of additional certificates that may appear in the path before anyPolicy is no longer permitted.                        |
| 13 | **private_key_usage_period_not_before** | timestamp | 1 | Specifies the date on which the validity period begins for the private key, if it is different from the validity period of the certificate. |
| 14 | **private_key_usage_period_not_after**  | timestamp | 1 | Specifies the date on which the validity period ends for the private key, if it is different from the validity period of the certificate.   |
| 15 | **certificate_policies**                | String    | 1 | Specifies a sequence of one or more policy information terms, each of which consists of an object identifier (OID) and optional qualifiers. |
| 16 | **policy_mappings**                     | String    | 1 | Specifies one or more pairs of OIDs; each pair includes an issuerDomainPolicy and a subjectDomainPolicy                                     |

**_Type: file_extensions_dictionary (Record)_**

| ID | Name         | Type     | # | Description                                                                                                                                 |
|---:|:-------------|:---------|--:|:--------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **ntfs_ext** | ntfs_ext | 1 | The NTFS file extension specifies a default extension for capturing properties specific to the storage of the file on the NTFS file system. |

**_Type: ntfs_ext (Record)_**

| ID | Name                       | Type                            | # | Description                                                              |
|---:|:---------------------------|:--------------------------------|--:|:-------------------------------------------------------------------------|
|  1 | **sid**                    | String                          | 1 | Specifies the security ID (SID) value assigned to the file.              |
|  2 | **alternate_data_streams** | Ntfs-ext$Alternate-data-streams | 1 | Specifies a list of NTFS alternate data streams that exist for the file. |

**_Type: ntfs_atlternate_data_stream (Record)_**

| ID | Name       | Type                               | # | Description                                                                           |
|---:|:-----------|:-----------------------------------|--:|:--------------------------------------------------------------------------------------|
|  1 | **name**   | String                             | 1 | Specifies the name of the alternate data stream.                                      |
|  2 | **hashes** | Ntfs-atlternate-data-stream$Hashes | 1 | Specifies a dictionary of hashes for the data contained in the alternate data stream. |
|  3 | **size**   | Ntfs-atlternate-data-stream$Size   | 1 | Specifies the size of the alternate data stream, in bytes, as a non-negative integer. |

**_Type: ipfix_choice (Choice)_**

| ID | Name              | Type          | # | Description |
|---:|:------------------|:--------------|--:|:------------|
|  1 | **ipfix_string**  | String        | 1 |             |
|  2 | **ipfix_integer** | Integer{0..*} | 1 |             |

**_Type: hashes (Record)_**

| ID | Name         | Type            | # | Description                                 |
|---:|:-------------|:----------------|--:|:--------------------------------------------|
|  1 | **MD5**      | Hashes$Md5      | 1 | Specifies the MD5 message digest algorithm. |
|  2 | **SHA-1**    | Hashes$Sha-1    | 1 | Specifies the MD5 message digest algorithm. |
|  3 | **SHA-256**  | Hashes$Sha-256  | 1 | Specifies the MD5 message digest algorithm. |
|  4 | **SHA-512**  | Hashes$Sha-512  | 1 | Specifies the MD5 message digest algorithm. |
|  5 | **SHA3-256** | Hashes$Sha3-256 | 1 | Specifies the MD5 message digest algorithm. |
|  6 | **SHA3-512** | Hashes$Sha3-512 | 1 | Specifies the MD5 message digest algorithm. |
|  7 | **SSDEEP**   | Hashes$Ssdeep   | 1 | Specifies the MD5 message digest algorithm. |
|  8 | **TLSH**     | Hashes$Tlsh     | 1 | Specifies the MD5 message digest algorithm. |

**_Type: network_traffic_extensions_dictionary (Record)_**

| ID | Name                 | Type             | # | Description                                                                                                                          |
|---:|:---------------------|:-----------------|--:|:-------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **http_request_ext** | http_request_ext | 1 | The HTTP request extension specifies a default extension for capturing network traffic properties specific to HTTP requests.         |
|  2 | **icmp_ext**         | icmp_ext         | 1 | The ICMP extension specifies a default extension for capturing network traffic properties specific to ICMP.                          |
|  3 | **socket_ext**       | socket_ext       | 1 | The Network Socket extension specifies a default extension for capturing network traffic properties associated with network sockets. |
|  4 | **tcp_ext**          | tcp_ext          | 1 | The TCP extension specifies a default extension for capturing network traffic properties specific to TCP.                            |

**_Type: http_request_ext (Record)_**

| ID | Name                      | Type                            | # | Description                                                                        |
|---:|:--------------------------|:--------------------------------|--:|:-----------------------------------------------------------------------------------|
|  1 | **request_method**        | String                          | 1 | Specifies the HTTP method portion of the HTTP request line, as a lowercase string. |
|  2 | **request_value**         | String                          | 1 | Specifies the value (typically a resource path) portion of the HTTP request line.  |
|  3 | **request_version**       | String                          | 1 | Specifies the HTTP method portion of the HTTP request line, as a lowercase string. |
|  4 | **request_header**        | Http-request-ext$Request-header | 1 | Specifies the value (typically a resource path) portion of the HTTP request line.  |
|  5 | **message_body_length**   | String                          | 1 | Specifies the HTTP method portion of the HTTP request line, as a lowercase string. |
|  6 | **message_body_data_ref** | String                          | 1 | Specifies the value (typically a resource path) portion of the HTTP request line.  |

**_Type: icmp_ext (Record)_**

| ID | Name              | Type | # | Description                   |
|---:|:------------------|:-----|--:|:------------------------------|
|  1 | **icmp_type_hex** | Hex  | 1 | Specifies the ICMP type byte. |
|  2 | **icmp_code_hex** | Hex  | 1 | Specifies the ICMP code byte. |

**_Type: socket_ext (Record)_**

| ID | Name                  | Type                         | # | Description                                                                                       |
|---:|:----------------------|:-----------------------------|--:|:--------------------------------------------------------------------------------------------------|
|  1 | **address_family**    | address_family               | 1 | Specifies the address family (AF_*) that the socket is configured for.                            |
|  2 | **is_blocking**       | Boolean                      | 1 | Specifies whether the socket is in blocking mode.                                                 |
|  3 | **is_listening**      | String                       | 1 | Specifies whether the socket is in listening mode.                                                |
|  4 | **options**           | Socket-ext$Options           | 1 | Specifies any options (SO_*) that may be used by the socket, as a dictionary.                     |
|  5 | **socket_type**       | socket_type                  | 1 | Specifies the type of the socket.                                                                 |
|  6 | **socket_descriptor** | Socket-ext$Socket-descriptor | 1 | Specifies the socket file descriptor value associated with the socket, as a non-negative integer. |
|  7 | **socket_handle**     | Integer{0..*}                | 1 | Specifies the handle or inode value associated with the socket.                                   |

**_Type: tcp_ext (Record)_**

| ID | Name              | Type | # | Description                                                                                                                                                                                                  |
|---:|:------------------|:-----|--:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | **src_flags_hex** | Hex  | 1 | Specifies the source TCP flags, as the union of all TCP flags observed between the start of the traffic (as defined by the start property) and the end of the traffic (as defined by the end property).      |
|  2 | **dst_flags_hex** | Hex  | 1 | Specifies the destination TCP flags, as the union of all TCP flags observed between the start of the traffic (as defined by the start property) and the end of the traffic (as defined by the end property). |

**_Type: address_family (Enumerated)_**

| ID | Name             | Description |
|---:|:-----------------|:------------|
|  1 | **AF_UNSPEC**    |             |
|  2 | **AF_INET**      |             |
|  3 | **AF_IPX**       |             |
|  4 | **AF_APPLETALK** |             |
|  5 | **AF_NETBIOS**   |             |
|  6 | **AF_INET6**     |             |
|  7 | **AF_IRDA**      |             |
|  8 | **AF_BTH**       |             |

**_Type: socket_option (Record)_**

| ID | Name              | Type                        | # | Description |
|---:|:------------------|:----------------------------|--:|:------------|
|  1 | **socket_option** | Socket-option$Socket-option | 1 |             |
|  2 | **option_value**  | Integer{0..*}               | 1 |             |

**_Type: socket_type (Enumerated)_**

| ID | Name               | Description |
|---:|:-------------------|:------------|
|  1 | **SOCK_STREAM**    |             |
|  2 | **SOCK_DGRAM**     |             |
|  3 | **SOCK_RAW**       |             |
|  4 | **SOCK_RDM**       |             |
|  5 | **SOCK_SEQPACKET** |             |

**_Type: user_account_extensions_dictionary (Record)_**

| ID | Name                 | Type             | # | Description                                                                                                     |
|---:|:---------------------|:-----------------|--:|:----------------------------------------------------------------------------------------------------------------|
|  1 | **unix_account_ext** | unix_account_ext | 1 | The User Account Object defines the following extensions. In addition to these, producers MAY create their own. |

**_Type: unix_account_ext (Record)_**

| ID | Name    | Type         | # | Description                                    |
|---:|:--------|:-------------|--:|:-----------------------------------------------|
|  1 | **gid** | Number{0..*} | 1 | Specifies the primary group ID of the account. |

**_Type: process_extensions_dictionary (Record)_**

| ID | Name                           | Type                       | # | Description                                                                                                         |
|---:|:-------------------------------|:---------------------------|--:|:--------------------------------------------------------------------------------------------------------------------|
|  1 | **windows_proccess_extension** | windows_proccess_extension | 1 | The Windows Process extension specifies a default extension for capturing properties specific to Windows processes. |
|  2 | **windows_service_ext**        | windows_service_ext        | 1 | The Windows Service extension specifies a default extension for capturing properties specific to Windows services.  |

**_Type: windows_proccess_extension (Record)_**

| ID | Name                | Type                         | # | Description                                                                             |
|---:|:--------------------|:-----------------------------|--:|:----------------------------------------------------------------------------------------|
|  1 | **aslr_enabled**    | Boolean                      | 1 | Specifies whether Address Space Layout Randomization (ASLR) is enabled for the process. |
|  2 | **dep_enabled**     | Boolean                      | 1 | Specifies whether Data Execution Prevention (DEP) is enabled for the process.           |
|  3 | **priority**        | String                       | 1 | Specifies the current priority class of the process in Windows.                         |
|  4 | **owner_sid**       | String                       | 1 | Specifies the Security ID (SID) value of the owner of the process.                      |
|  5 | **window_title**    | String                       | 1 | Specifies the title of the main window of the process.                                  |
|  6 | **startup_info**    | startup_info_dictionary      | 1 | Specifies the STARTUP_INFO struct used by the process, as a dictionary.                 |
|  7 | **integrity_level** | windows_integrity_level_enum | 1 | Specifies the Windows integrity level, or trustworthiness, of the process.              |

**_Type: startup_info_dictionary (Array)_**

| ID | Type                                | # | Description |
|---:|:------------------------------------|--:|:------------|
|  1 | String                              | 1 | None::      |
|  2 | String                              | 1 | None::      |
|  3 | String                              | 1 | None::      |
|  4 | String                              | 1 | None::      |
|  5 | String                              | 1 | None::      |
|  6 | String                              | 1 | None::      |
|  7 | String                              | 1 | None::      |
|  8 | String                              | 1 | None::      |
|  9 | Startup-info-dictionary$Lpreserved  | 1 | None::      |
| 10 | Startup-info-dictionary$Lpreserved2 | 1 | None::      |
| 11 | Integer                             | 1 | None::      |
| 12 | Integer                             | 1 | None::      |
| 13 | Integer                             | 1 | None::      |
| 14 | Integer                             | 1 | None::      |
| 15 | Integer                             | 1 | None::      |
| 16 | Integer                             | 1 | None::      |
| 17 | Integer                             | 1 | None::      |
| 18 | Startup-info-dictionary$Cbreserved2 | 1 | None::      |

**_Type: windows_integrity_level_enum (Enumerated)_**

| ID | Name       | Description |
|---:|:-----------|:------------|
|  1 | **low**    |             |
|  2 | **medium** |             |
|  3 | **high**   |             |
|  4 | **system** |             |

**_Type: service_status (Enumerated)_**

| ID | Name                         | Description |
|---:|:-----------------------------|:------------|
|  1 | **SERVICE_CONTINUE_PENDING** |             |
|  2 | **SERVICE_PAUSE_PENDING**    |             |
|  3 | **SERVICE_PAUSED**           |             |
|  4 | **SERVICE_RUNNING**          |             |
|  5 | **SERVICE_START_PENDING**    |             |
|  6 | **SERVICE_STOP_PENDING**     |             |
|  7 | **SERVICE_STOPPED**          |             |

**_Type: service_type (Enumerated)_**

| ID | Name                            | Description |
|---:|:--------------------------------|:------------|
|  1 | **SERVICE_KERNEL_DRIVER**       |             |
|  2 | **SERVICE_FILE_SYSTEM_DRIVER**  |             |
|  3 | **SERVICE_WIN32_OWN_PROCESS**   |             |
|  4 | **SERVICE_WIN32_SHARE_PROCESS** |             |

**_Type: windows_service_ext (Record)_**

| ID | Name                 | Type                                 | # | Description                                                                           |
|---:|:---------------------|:-------------------------------------|--:|:--------------------------------------------------------------------------------------|
|  1 | **service_name**     | String                               | 1 | Specifies the name of the service.                                                    |
|  2 | **descriptions**     | Windows-service-ext$Descriptions     | 1 | Specifies the descriptions defined for the service.                                   |
|  3 | **display_name**     | String                               | 1 | Specifies the displayed name of the service in Windows GUI controls.                  |
|  4 | **group_name**       | String                               | 1 | Specifies the name of the load ordering group of which the service is a member.       |
|  5 | **start_type**       | start_type                           | 1 | Specifies the start options defined for the service. windows-service-start-enum       |
|  6 | **service_dll_refs** | Windows-service-ext$Service-dll-refs | 1 | Specifies the DLLs loaded by the service, as a reference to one or more File Objects. |
|  7 | **service_type**     | service_type                         | 1 | Specifies the type of the service. windows-service-enum                               |
|  8 | **service_status**   | service_status                       | 1 | Specifies the current status of the service. windows-service-status-enum              |

**_Type: start_type (Enumerated)_**

| ID | Name                     | Description |
|---:|:-------------------------|:------------|
|  1 | **SERVICE_AUTO_START**   |             |
|  2 | **SERVICE_BOOT_START**   |             |
|  3 | **SERVICE_DEMAND_START** |             |
|  4 | **SERVICE_DISABLED**     |             |
|  5 | **SERVICE_SYSTEM_ALERT** |             |

**_Type: spec_version (Enumerated)_**

| ID | Name    | Description |
|---:|:--------|:------------|
|  1 | **2.0** |             |
|  2 | **2.1** |             |


| Type Name               | Type Definition           | Description                                                          |
|:------------------------|:--------------------------|:---------------------------------------------------------------------|
| **object_marking_refs** | ArrayOf(identifier){1..*} | The list of marking-definition objects to be applied to this object. |

**_Type: granular_marking (Record)_**

| ID | Name          | Type       | # | Description                                                                                            |
|---:|:--------------|:-----------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **selectors** | identifier | 1 | A list of selectors for content contained within the STIX object in which this property appears.       |
|  2 | **lang**      | String     | 1 | Identifies the language of the text identified by this marking.                                        |
|  3 | **pattern**   | identifier | 1 | The marking_ref property specifies the ID of the marking-definition object that describes the marking. |


| Type Name             | Type Definition                 | Description                                             |
|:----------------------|:--------------------------------|:--------------------------------------------------------|
| **granular_markings** | ArrayOf(granular_marking){1..*} | The set of granular markings that apply to this object. |


| Type Name    | Type Definition | Description                                                                    |
|:-------------|:----------------|:-------------------------------------------------------------------------------|
| **defanged** | Boolean         | Defines whether or not the data contained within the object has been defanged. |


| Type Name      | Type Definition                                                                                                                | Description                                                                                                                                                                        |
|:---------------|:-------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **identifier** | String (%^[a-z][a-z0-9-]+[a-z0-9]--[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[1-5][0-9a-fA-F]{3}-[89abAB][0-9a-fA-F]{3}-[0-9a-fA-F]{12}$%) | Represents identifiers across the CTI specifications. The format consists of the name of the top-level object being identified, followed by two dashes (--), followed by a UUIDv4. |

**_Type: extensions (Record{1..*})_**

| ID | Name                     | Type                 | # | Description |
|---:|:-------------------------|:---------------------|--:|:------------|
|  1 | **extension**            | Extensions$Extension | 1 |             |
|  2 | **extension_definition** | extension            | 1 |             |

**_Type: properties (Array)_**

| ID | Type             | # | Description                                                                                                                                                                                                                                                                                                                                                       |
|---:|:-----------------|--:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  1 | Binary           | 1 | None::                                                                                                                                                                                                                                                                                                                                                            |
|  2 | Hex              | 1 | None:: The hex data type encodes an array of octets (8-bit bytes) as hexadecimal. The string MUST consist of an even number of hexadecimal characters, which are the digits '0' through '9' and the letters 'a' through 'f'.  In order to allow pattern matching on custom objects, all properties that use the hex type, the property name MUST end with '_hex'. |
|  3 | Properties$Array | 1 | None::                                                                                                                                                                                                                                                                                                                                                            |
|  4 | String           | 1 | None::                                                                                                                                                                                                                                                                                                                                                            |
|  5 | Integer          | 1 | None::                                                                                                                                                                                                                                                                                                                                                            |
|  6 | Boolean          | 1 | None::                                                                                                                                                                                                                                                                                                                                                            |
|  7 | Number           | 1 | None::                                                                                                                                                                                                                                                                                                                                                            |
|  8 | extensions       | 1 | None::                                                                                                                                                                                                                                                                                                                                                            |

**_Type: extension (Record{1..*})_**

| ID | Name               | Type                | # | Description            |
|---:|:-------------------|:--------------------|--:|:-----------------------|
|  1 | **extension_type** | extension_type_enum | 1 | The type of extension. |
|  2 | **properties**     | properties          | 1 |                        |

**_Type: extension_type_enum (Enumerated)_**

| ID | Name                            | Description |
|---:|:--------------------------------|:------------|
|  1 | **new-sdo**                     |             |
|  2 | **new-sco**                     |             |
|  3 | **new-sro**                     |             |
|  4 | **property-extension**          |             |
|  5 | **toplevel-property-extension** |             |


| Type Name | Type Definition                | Description |
|:----------|:-------------------------------|:------------|
| **Hex**   | String (%^([a-fA-F0-9]{2})+$%) |             |


| Type Name     | Type Definition                                                     | Description |
|:--------------|:--------------------------------------------------------------------|:------------|
| **timestamp** | String (%^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z$%) |             |


| Type Name    | Type Definition                | Description                                                                           |
|:-------------|:-------------------------------|:--------------------------------------------------------------------------------------|
| **Features** | ArrayOf(Feature){0..10} unique | An array of zero to ten names used to query a Consume for its supported capabilities. |


| Type Name     | Type Definition | Description   |
|:--------------|:----------------|:--------------|
| **Date-Time** | Integer{0..*}   | Date and Time |


| Type Name    | Type Definition | Description      |
|:-------------|:----------------|:-----------------|
| **Duration** | Integer{0..*}   | A length of time |

**_Type: Feature (Enumerated)_**

| ID | Name           | Description                                                         |
|---:|:---------------|:--------------------------------------------------------------------|
|  1 | **versions**   | List of OpenC2 Language versions supported by this Consumer         |
|  2 | **profiles**   | List of profiles supported by this Consumer                         |
|  3 | **pairs**      | List of supported Actions and applicable Targets                    |
|  4 | **rate_limit** | Maximum number of Commands per minute supported by design or policy |

**_Type: L4-Protocol (Enumerated)_**

|  ID | Name     | Description                                      |
|----:|:---------|:-------------------------------------------------|
|   1 | **icmp** | Internet Control Message Protocol - [RFC0792]    |
|   6 | **tcp**  | Transmission Control Protocol - [RFC0793]        |
|  17 | **udp**  | User Datagram Protocol - [RFC0768]               |
| 132 | **sctp** | Stream Control Transmission Protocol - [RFC4960] |

**_Type: Payload (Choice)_**

| ID | Name    | Type   | # | Description                                                 |
|---:|:--------|:-------|--:|:------------------------------------------------------------|
|  1 | **bin** | Binary | 1 | Specifies the data contained in the artifact                |
|  2 | **url** | URI    | 1 | MUST be a valid URL that resolves to the un-encoded content |


| Type Name | Type Definition | Description                                    |
|:----------|:----------------|:-----------------------------------------------|
| **Nsid**  | String{1..16}   | A short identifier that refers to a namespace. |

**_Type: Response-Type (Enumerated)_**

| ID | Name         | Description                                     |
|---:|:-------------|:------------------------------------------------|
|  0 | **none**     | No response                                     |
|  1 | **ack**      | Respond when Command received                   |
|  2 | **status**   | Respond with progress toward Command completion |
|  3 | **complete** | Respond when all aspects of Command completed   |

**_Type: Status-Code (Enumerated.ID)_**

|  ID | Description                                                                                                                                                          |
|----:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 102 | **Processing**::an interim Response used to inform the Producer that the Consumer has accepted the Command but has not yet completed it                              |
| 200 | **OK**::the Command has succeeded                                                                                                                                    |
| 201 | **Created**::the Command has succeeded and a new resource has been created as a result of it                                                                         |
| 400 | **Bad Request**::the Consumer cannot process the Command due to something that is perceived to be a Producer error (e.g., malformed Command syntax)                  |
| 401 | **Unauthorized**::the Command Message lacks valid authentication credentials for the target resource or authorization has been refused for the submitted credentials |
| 403 | **Forbidden**::the Consumer understood the Command but refuses to authorize it                                                                                       |
| 404 | **Not Found**::the Consumer has not found anything matching the Command                                                                                              |
| 500 | **Internal Error**::the Consumer encountered an unexpected condition that prevented it from performing the Command                                                   |
| 501 | **Not Implemented**::the Consumer does not support the functionality required to perform the Command                                                                 |
| 503 | **Service Unavailable**::the Consumer is currently unable to perform the Command due to a temporary overloading or maintenance of the Consumer                       |


| Type Name      | Type Definition       | Description        |
|:---------------|:----------------------|:-------------------|
| **Command-ID** | String (%^\S{0,36}$%) | Command Identifier |


| Type Name   | Type Definition | Description                |
|:------------|:----------------|:---------------------------|
| **Version** | String          | Major.Minor version number |


| Type Name       | Type Definition | Description               |
|:----------------|:----------------|:--------------------------|
| **Process$pid** | Integer{0..*}   | Process ID of the process |


| Type Name            | Type Definition                | Description                                                 |
|:---------------------|:-------------------------------|:------------------------------------------------------------|
| **Results$Versions** | ArrayOf(Version){1..10} unique | List of OpenC2 language versions supported by this Actuator |


| Type Name            | Type Definition            | Description                                 |
|:---------------------|:---------------------------|:--------------------------------------------|
| **Results$Profiles** | ArrayOf(Nsid){1..*} unique | List of profiles supported by this Actuator |


| Type Name              | Type Definition | Description                                                         |
|:-----------------------|:----------------|:--------------------------------------------------------------------|
| **Results$Rate-limit** | Number{0..*}    | Maximum number of requests per minute supported by design or policy |


| Type Name        | Type Definition | Description |
|:-----------------|:----------------|:------------|
| **Results$Args** | ArrayOf(String) |             |


| Type Name                | Type Definition | Description                            |
|:-------------------------|:----------------|:---------------------------------------|
| **Huntargs$String-args** | ArrayOf(String) | string arguments supplied as huntargs. |


| Type Name                 | Type Definition  | Description                             |
|:--------------------------|:-----------------|:----------------------------------------|
| **Huntargs$Integer-args** | ArrayOf(Integer) | integer arguments supplied as huntargs. |


| Type Name       | Type Definition | Description               |
|:----------------|:----------------|:--------------------------|
| **Process$Pid** | Integer{0..*}   | Process ID of the process |


| Type Name      | Type Definition | Description                                  |
|:---------------|:----------------|:---------------------------------------------|
| **Hashes$Md5** | Binary /x       | MD5 hash as defined in [[RFC1321]](#rfc1321) |


| Type Name       | Type Definition | Description                                   |
|:----------------|:----------------|:----------------------------------------------|
| **Hashes$Sha1** | Binary /x       | SHA1 hash as defined in [[RFC6234]](#rfc6234) |


| Type Name         | Type Definition | Description                                     |
|:------------------|:----------------|:------------------------------------------------|
| **Hashes$Sha256** | Binary /x       | SHA256 hash as defined in [[RFC6234]](#rfc6234) |


| Type Name                    | Type Definition        | Description                                   |
|:-----------------------------|:-----------------------|:----------------------------------------------|
| **Ap-results$Huntflow-info** | ArrayOf(Huntflow-Info) | Structured data returned by Query: Huntflows. |


| Type Name                     | Type Definition | Description                         |
|:------------------------------|:----------------|:------------------------------------|
| **Inv-return$String-returns** | ArrayOf(String) | String return from an investigation |


| Type Name         | Type Definition       | Description                                    |
|:------------------|:----------------------|:-----------------------------------------------|
| **Artifact$Type** | String (%^artifact$%) | The value of this property MUST be `artifact`. |


| Type Name       | Type Definition        | Description |
|:----------------|:-----------------------|:------------|
| **Artifact$Id** | String (%^artifact--%) |             |


| Type Name              | Type Definition                                                                                | Description                                                                                         |
|:-----------------------|:-----------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------|
| **Artifact$Mime-type** | String (%^(application|audio|font|image|message|model|multipart|text|video)/[a-zA-Z0-9.+_-]+%) | The value of this property MUST be a valid MIME type as specified in the IANA Media Types registry. |


| Type Name           | Type Definition | Description                                                                                                                              |
|:--------------------|:----------------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| **Artifact$Hashes** | ArrayOf(hashes) | Specifies a dictionary of hashes for the contents of the url or the payload_bin. This MUST be provided when the url property is present. |


| Type Name                  | Type Definition                | Description |
|:---------------------------|:-------------------------------|:------------|
| **Autonomous-system$Type** | String (%^autonomous-system$%) |             |


| Type Name                | Type Definition                 | Description |
|:-------------------------|:--------------------------------|:------------|
| **Autonomous-system$Id** | String (%^autonomous-system--%) |             |


| Type Name          | Type Definition        | Description |
|:-------------------|:-----------------------|:------------|
| **Directory$Type** | String (%^directory$%) |             |


| Type Name        | Type Definition         | Description |
|:-----------------|:------------------------|:------------|
| **Directory$Id** | String (%^directory--%) |             |


| Type Name              | Type Definition                         | Description                                   |
|:-----------------------|:----------------------------------------|:----------------------------------------------|
| **Directory$Path-enc** | String (%^[a-zA-Z0-9/\\.+_:-]{2,250}$%) | Specifies the observed encoding for the path. |


| Type Name                   | Type Definition       | Description                                                                                           |
|:----------------------------|:----------------------|:------------------------------------------------------------------------------------------------------|
| **Directory$Contains-refs** | ArrayOf(String){1..*} | Specifies a list of references to other File and/or Directory Objects contained within the directory. |


| Type Name            | Type Definition          | Description |
|:---------------------|:-------------------------|:------------|
| **Domain-name$Type** | String (%^domain-name$%) |             |


| Type Name          | Type Definition           | Description |
|:-------------------|:--------------------------|:------------|
| **Domain-name$Id** | String (%^domain-name--%) |             |


| Type Name                        | Type Definition       | Description                                                                                                  |
|:---------------------------------|:----------------------|:-------------------------------------------------------------------------------------------------------------|
| **Domain-name$Resolves-to-refs** | ArrayOf(String){1..*} | Specifies a list of references to one or more IP addresses or domain names that the domain name resolves to. |


| Type Name           | Type Definition         | Description |
|:--------------------|:------------------------|:------------|
| **Email-addr$Type** | String (%^email-addr$%) |             |


| Type Name         | Type Definition          | Description |
|:------------------|:-------------------------|:------------|
| **Email-addr$Id** | String (%^email-addr--%) |             |


| Type Name              | Type Definition            | Description |
|:-----------------------|:---------------------------|:------------|
| **Email-message$Type** | String (%^email-message$%) |             |


| Type Name            | Type Definition             | Description |
|:---------------------|:----------------------------|:------------|
| **Email-message$Id** | String (%^email-message--%) |             |


| Type Name                 | Type Definition       | Description                                                             |
|:--------------------------|:----------------------|:------------------------------------------------------------------------|
| **Email-message$To-refs** | ArrayOf(String){1..*} | Specifies the mailboxes that are 'To:' recipients of the email message. |


| Type Name                 | Type Definition       | Description                                                             |
|:--------------------------|:----------------------|:------------------------------------------------------------------------|
| **Email-message$Cc-refs** | ArrayOf(String){1..*} | Specifies the mailboxes that are 'CC:' recipients of the email message. |


| Type Name                  | Type Definition       | Description                                                              |
|:---------------------------|:----------------------|:-------------------------------------------------------------------------|
| **Email-message$Bcc-refs** | ArrayOf(String){1..*} | Specifies the mailboxes that are 'BCC:' recipients of the email message. |


| Type Name                        | Type Definition | Description                                                                             |
|:---------------------------------|:----------------|:----------------------------------------------------------------------------------------|
| **Email-message$Received-lines** | ArrayOf(String) | Specifies one or more Received header fields that may be included in the email headers. |


| Type Name                                  | Type Definition                         | Description                                                                    |
|:-------------------------------------------|:----------------------------------------|:-------------------------------------------------------------------------------|
| **Email-message$Additional-header-fields** | ArrayOf(email-additional-header-fields) | Specifies any other header fields found in the email message, as a dictionary. |


| Type Name                        | Type Definition         | Description                                                                                                             |
|:---------------------------------|:------------------------|:------------------------------------------------------------------------------------------------------------------------|
| **Email-message$Body-multipart** | ArrayOf(mime-part-type) | Specifies a list of the MIME parts that make up the email body. This property MAY only be used if is_multipart is true. |


| Type Name     | Type Definition   | Description                                |
|:--------------|:------------------|:-------------------------------------------|
| **File$Type** | String (%^file$%) | The value of this property MUST be `file`. |


| Type Name   | Type Definition    | Description |
|:------------|:-------------------|:------------|
| **File$Id** | String (%^file--%) |             |


| Type Name       | Type Definition | Description                                    |
|:----------------|:----------------|:-----------------------------------------------|
| **File$Hashes** | ArrayOf(hashes) | Specifies a dictionary of hashes for the file. |


| Type Name     | Type Definition | Description                                                          |
|:--------------|:----------------|:---------------------------------------------------------------------|
| **File$Size** | Integer{0..*}   | Specifies the size of the file, in bytes, as a non-negative integer. |


| Type Name         | Type Definition                         | Description                                               |
|:------------------|:----------------------------------------|:----------------------------------------------------------|
| **File$Name-enc** | String (%^[a-zA-Z0-9/\\.+_:-]{2,250}$%) | Specifies the observed encoding for the name of the file. |


| Type Name              | Type Definition       | Description                                                                           |
|:-----------------------|:----------------------|:--------------------------------------------------------------------------------------|
| **File$Contains-refs** | ArrayOf(String){1..*} | Specifies a list of references to other Observable Objects contained within the file. |


| Type Name          | Type Definition        | Description |
|:-------------------|:-----------------------|:------------|
| **Ipv4-addr$Type** | String (%^ipv4-addr$%) |             |


| Type Name        | Type Definition         | Description |
|:-----------------|:------------------------|:------------|
| **Ipv4-addr$Id** | String (%^ipv4-addr--%) |             |


| Type Name               | Type Definition                                                                                                                                      | Description |
|:------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|:------------|
| **Ipv4-addr$Ipv4-addr** | String (%^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])(\\/(3[0-2]|[1-2][0-9]|[0-9]))?$%) |             |


| Type Name                      | Type Definition       | Description |
|:-------------------------------|:----------------------|:------------|
| **Ipv4-addr$Resolves-to-refs** | ArrayOf(String){1..*} |             |


| Type Name                     | Type Definition       | Description |
|:------------------------------|:----------------------|:------------|
| **Ipv4-addr$Belongs-to-refs** | ArrayOf(String){1..*} |             |


| Type Name          | Type Definition        | Description |
|:-------------------|:-----------------------|:------------|
| **Ipv6-addr$Type** | String (%^ipv6-addr$%) |             |


| Type Name        | Type Definition         | Description |
|:-----------------|:------------------------|:------------|
| **Ipv6-addr$Id** | String (%^ipv6-addr--%) |             |


| Type Name               | Type Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Description                                                                                  |
|:------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------|
| **Ipv6-addr$Ipv6-addr** | String (%^s*((([0-9A-Fa-f]{1,4}:){7}([0-9A-Fa-f]{1,4}|:))|(([0-9A-Fa-f]{1,4}:){6}(:[0-9A-Fa-f]{1,4}|((25[0-5]|2[0-4]d|1dd|[1-9]?d)(.(25[0-5]|2[0-4]d|1dd|[1-9]?d)){3})|:))|(([0-9A-Fa-f]{1,4}:){5}(((:[0-9A-Fa-f]{1,4}){1,2})|:((25[0-5]|2[0-4]d|1dd|[1-9]?d)(.(25[0-5]|2[0-4]d|1dd|[1-9]?d)){3})|:))|(([0-9A-Fa-f]{1,4}:){4}(((:[0-9A-Fa-f]{1,4}){1,3})|((:[0-9A-Fa-f]{1,4})?:((25[0-5]|2[0-4]d|1dd|[1-9]?d)(.(25[0-5]|2[0-4]d|1dd|[1-9]?d)){3}))|:))|(([0-9A-Fa-f]{1,4}:){3}(((:[0-9A-Fa-f]{1,4}){1,4})|((:[0-9A-Fa-f]{1,4}){0,2}:((25[0-5]|2[0-4]d|1dd|[1-9]?d)(.(25[0-5]|2[0-4]d|1dd|[1-9]?d)){3}))|:))|(([0-9A-Fa-f]{1,4}:){2}(((:[0-9A-Fa-f]{1,4}){1,5})|((:[0-9A-Fa-f]{1,4}){0,3}:((25[0-5]|2[0-4]d|1dd|[1-9]?d)(.(25[0-5]|2[0-4]d|1dd|[1-9]?d)){3}))|:))|(([0-9A-Fa-f]{1,4}:){1}(((:[0-9A-Fa-f]{1,4}){1,6})|((:[0-9A-Fa-f]{1,4}){0,4}:((25[0-5]|2[0-4]d|1dd|[1-9]?d)(.(25[0-5]|2[0-4]d|1dd|[1-9]?d)){3}))|:))|(:(((:[0-9A-Fa-f]{1,4}){1,7})|((:[0-9A-Fa-f]{1,4}){0,5}:((25[0-5]|2[0-4]d|1dd|[1-9]?d)(.(25[0-5]|2[0-4]d|1dd|[1-9]?d)){3}))|:)))(%.+)?s*(\\/(12[0-8]|1[0-1][0-9]|[1-9][0-9]|[0-9]))?$%) | The IPv6 Address Object represents one or more IPv6 addresses expressed using CIDR notation. |


| Type Name                      | Type Definition | Description                                                                                                                   |
|:-------------------------------|:----------------|:------------------------------------------------------------------------------------------------------------------------------|
| **Ipv6-addr$Resolves-to-refs** | ArrayOf(String) | Specifies a list of references to one or more Layer 2 Media Access Control (MAC) addresses that the IPv6 address resolves to. |


| Type Name                     | Type Definition | Description                                                                                    |
|:------------------------------|:----------------|:-----------------------------------------------------------------------------------------------|
| **Ipv6-addr$Belongs-to-refs** | ArrayOf(String) | Specifies a reference to one or more autonomous systems (AS) that the IPv6 address belongs to. |


| Type Name         | Type Definition       | Description |
|:------------------|:----------------------|:------------|
| **Mac-addr$Type** | String (%^mac-addr$%) |             |


| Type Name       | Type Definition        | Description |
|:----------------|:-----------------------|:------------|
| **Mac-addr$Id** | String (%^mac-addr--%) |             |


| Type Name                      | Type Definition                               | Description                                                        |
|:-------------------------------|:----------------------------------------------|:-------------------------------------------------------------------|
| **Mac-addr$Mac-address-value** | String (%^([0-9a-f]{2}[:]){5}([0-9a-f]{2})$%) | Specifies one or more mac addresses expressed using CIDR notation. |


| Type Name      | Type Definition    | Description |
|:---------------|:-------------------|:------------|
| **Mutex$Type** | String (%^mutex$%) |             |


| Type Name    | Type Definition     | Description |
|:-------------|:--------------------|:------------|
| **Mutex$Id** | String (%^mutex--%) |             |


| Type Name                | Type Definition              | Description |
|:-------------------------|:-----------------------------|:------------|
| **Network-traffic$Type** | String (%^network-traffic$%) |             |


| Type Name              | Type Definition               | Description |
|:-----------------------|:------------------------------|:------------|
| **Network-traffic$Id** | String (%^network-traffic--%) |             |


| Type Name                 | Type Definition                                                    | Description                                                          |
|:--------------------------|:-------------------------------------------------------------------|:---------------------------------------------------------------------|
| **Network-traffic$Start** | String (%^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z%) | Specifies the date/time the network traffic was initiated, if known. |


| Type Name                | Type Definition                                                    | Description                                                  |
|:-------------------------|:-------------------------------------------------------------------|:-------------------------------------------------------------|
| **Network-traffic$Stop** | String (%^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z%) | Specifies the date/time the network traffic ended, if known. |


| Type Name                    | Type Definition   | Description                                                                                                             |
|:-----------------------------|:------------------|:------------------------------------------------------------------------------------------------------------------------|
| **Network-traffic$Src-port** | Integer{0..65535} | Specifies the source port used in the network traffic, as an integer. The port value MUST be in the range of 0 - 65535. |


| Type Name                    | Type Definition   | Description                                                                                                                  |
|:-----------------------------|:------------------|:-----------------------------------------------------------------------------------------------------------------------------|
| **Network-traffic$Dst-port** | Integer{0..65535} | Specifies the destination port used in the network traffic, as an integer. The port value MUST be in the range of 0 - 65535. |


| Type Name                     | Type Definition       | Description                                                                                    |
|:------------------------------|:----------------------|:-----------------------------------------------------------------------------------------------|
| **Network-traffic$Protocols** | ArrayOf(String){1..*} | Specifies the protocols observed in the network traffic, along with their corresponding state. |


| Type Name                             | Type Definition       | Description                                                  |
|:--------------------------------------|:----------------------|:-------------------------------------------------------------|
| **Network-traffic$Encapsulates-refs** | ArrayOf(String){1..*} | Specifies the bytes sent from the source to the destination. |


| Type Name        | Type Definition      | Description |
|:-----------------|:---------------------|:------------|
| **Process$Type** | String (%^process$%) |             |


| Type Name      | Type Definition       | Description |
|:---------------|:----------------------|:------------|
| **Process$Id** | String (%^process--%) |             |


| Type Name                         | Type Definition | Description                                                                              |
|:----------------------------------|:----------------|:-----------------------------------------------------------------------------------------|
| **Process$Environment-variables** | ArrayOf(String) | Specifies the list of environment variables associated with the process as a dictionary. |


| Type Name                    | Type Definition       | Description                                                                           |
|:-----------------------------|:----------------------|:--------------------------------------------------------------------------------------|
| **Process$Creator-user-ref** | ArrayOf(String){1..*} | Specifies the user that created the process, as a reference to a User Account Object. |


| Type Name              | Type Definition       | Description                                                                                                                              |
|:-----------------------|:----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| **Process$Child-refs** | ArrayOf(String){1..*} | Specifies the other processes that were spawned by (i.e. children of) this process, as a reference to one or more other Process Objects. |


| Type Name         | Type Definition       | Description |
|:------------------|:----------------------|:------------|
| **Software$Type** | String (%^software$%) |             |


| Type Name         | Type Definition | Description                         |
|:------------------|:----------------|:------------------------------------|
| **Software$Name** | String{1..*}    | Specifies the name of the software. |


| Type Name        | Type Definition                                                                                                                                                                                                                                                                                                                                   | Description                                                                                                                                                                      |
|:-----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Software$Cpe** | String (%cpe:2\\.3:[aho\\*\\-](:(((\\?*|\\*?)([a-zA-Z0-9\\-\\._]|(\\\\[\\\\\\*\\?!\"#$$%&'\\(\\)\\+,/:;<=>@\\[\\]\\^`\\{\\|}~]))+(\\?*|\\*?))|[\\*\\-])){5}(:(([a-zA-Z]{2,3}(-([a-zA-Z]{2}|[0-9]{3}))?)|[\\*\\-]))(:(((\\?*|\\*?)([a-zA-Z0-9\\-\\._]|(\\\\[\\\\\\*\\?!\"#$$%&'\\(\\)\\+,/:;<=>@\\[\\]\\^`\\{\\|}~]))+(\\?*|\\*?))|[\\*\\-])){4}%) | Specifies the Common Platform Enumeration (CPE) entry for the software, if available. The value for this property MUST be a CPE v2.3 entry from the official NVD CPE Dictionary. |


| Type Name         | Type Definition | Description                                                                             |
|:------------------|:----------------|:----------------------------------------------------------------------------------------|
| **Software$Swid** | String          | Specifies the Software Identification (SWID) Tags entry for the software, if available. |


| Type Name              | Type Definition | Description                                                                                                          |
|:-----------------------|:----------------|:---------------------------------------------------------------------------------------------------------------------|
| **Software$Languages** | ArrayOf(String) | Specifies the languages supported by the software. The value of each list member MUST be an ISO 639-2 language code. |


| Type Name           | Type Definition | Description                                       |
|:--------------------|:----------------|:--------------------------------------------------|
| **Software$Vendor** | String          | Specifies the name of the vendor of the software. |


| Type Name            | Type Definition | Description                            |
|:---------------------|:----------------|:---------------------------------------|
| **Software$Version** | String          | Specifies the version of the software. |


| Type Name             | Type Definition           | Description                                        |
|:----------------------|:--------------------------|:---------------------------------------------------|
| **User-account$Type** | String (%^user-account$%) | The value of this property MUST be `user-account`. |


| Type Name           | Type Definition            | Description |
|:--------------------|:---------------------------|:------------|
| **User-account$Id** | String (%^user-account--%) |             |


| Type Name    | Type Definition  | Description                               |
|:-------------|:-----------------|:------------------------------------------|
| **Url$Type** | String (%^url$%) | The value of this property MUST be `url`. |


| Type Name  | Type Definition | Description |
|:-----------|:----------------|:------------|
| **Url$Id** | String (%^url%) |             |


| Type Name         | Type Definition                                                      | Description                     |
|:------------------|:---------------------------------------------------------------------|:--------------------------------|
| **Url$Url-value** | String (%^(([^:/?#]+):)?(//([^/?#]*))?([^?#]*)(\?([^#]*))?(#(.*))?%) | Specifies the value of the URL. |


| Type Name                     | Type Definition                   | Description                                                |
|:------------------------------|:----------------------------------|:-----------------------------------------------------------|
| **Windows-registry-key$Type** | String (%^windows-registry-key$%) | The value of this property MUST be `windows-registry-key`. |


| Type Name                   | Type Definition                    | Description |
|:----------------------------|:-----------------------------------|:------------|
| **Windows-registry-key$Id** | String (%^windows-registry-key--%) |             |


| Type Name                    | Type Definition                                                                  | Description                                         |
|:-----------------------------|:---------------------------------------------------------------------------------|:----------------------------------------------------|
| **Windows-registry-key$Key** | String (%^((?!((^|, )(HKLM|HKCC|HKCR|HKCU|HKU|hklm|hkcc|hkcr|hkcu|hku))+$).)*$%) | Specifies the full registry key including the hive. |


| Type Name                                | Type Definition                      | Description                                        |
|:-----------------------------------------|:-------------------------------------|:---------------------------------------------------|
| **Windows-registry-key$Registry-values** | ArrayOf(windows_registry_value_type) | Specifies the values found under the registry key. |


| Type Name                 | Type Definition               | Description                                            |
|:--------------------------|:------------------------------|:-------------------------------------------------------|
| **X509-certificate$Type** | String (%^x509-certificate$%) | The value of this property MUST be `x509-certificate`. |


| Type Name               | Type Definition                | Description |
|:------------------------|:-------------------------------|:------------|
| **X509-certificate$Id** | String (%^x509-certificate--%) |             |


| Type Name                   | Type Definition | Description                                                                           |
|:----------------------------|:----------------|:--------------------------------------------------------------------------------------|
| **X509-certificate$Hashes** | ArrayOf(hashes) | Specifies any hashes that were calculated for the entire contents of the certificate. |


| Type Name                               | Type Definition                  | Description                                                                     |
|:----------------------------------------|:---------------------------------|:--------------------------------------------------------------------------------|
| **X509-certificate$X509-v3-extensions** | ArrayOf(x509_v3_extensions_type) | Specifies any standard X.509 v3 extensions that may be used in the certificate. |


| Type Name                                      | Type Definition                   | Description |
|:-----------------------------------------------|:----------------------------------|:------------|
| **Email-additional-header-value$String-value** | String (%[a-zA-Z0-9_-]{0,250}^$%) |             |


| Type Name                                      | Type Definition       | Description |
|:-----------------------------------------------|:----------------------|:------------|
| **Email-additional-header-value$String-array** | ArrayOf(String){2..*} |             |


| Type Name                           | Type Definition                      | Description                                                              |
|:------------------------------------|:-------------------------------------|:-------------------------------------------------------------------------|
| **Ntfs-ext$Alternate-data-streams** | ArrayOf(ntfs_atlternate_data_stream) | Specifies a list of NTFS alternate data streams that exist for the file. |


| Type Name                              | Type Definition | Description                                                                           |
|:---------------------------------------|:----------------|:--------------------------------------------------------------------------------------|
| **Ntfs-atlternate-data-stream$Hashes** | ArrayOf(hashes) | Specifies a dictionary of hashes for the data contained in the alternate data stream. |


| Type Name                            | Type Definition | Description                                                                           |
|:-------------------------------------|:----------------|:--------------------------------------------------------------------------------------|
| **Ntfs-atlternate-data-stream$Size** | Integer{0..*}   | Specifies the size of the alternate data stream, in bytes, as a non-negative integer. |


| Type Name        | Type Definition              | Description                                 |
|:-----------------|:-----------------------------|:--------------------------------------------|
| **Hashes$Sha-1** | String (%^[a-fA-F0-9]{40}$%) | Specifies the MD5 message digest algorithm. |


| Type Name          | Type Definition              | Description                                 |
|:-------------------|:-----------------------------|:--------------------------------------------|
| **Hashes$Sha-256** | String (%^[a-fA-F0-9]{64}$%) | Specifies the MD5 message digest algorithm. |


| Type Name          | Type Definition               | Description                                 |
|:-------------------|:------------------------------|:--------------------------------------------|
| **Hashes$Sha-512** | String (%^[a-fA-F0-9]{128}$%) | Specifies the MD5 message digest algorithm. |


| Type Name           | Type Definition              | Description                                 |
|:--------------------|:-----------------------------|:--------------------------------------------|
| **Hashes$Sha3-256** | String (%^[a-fA-F0-9]{64}$%) | Specifies the MD5 message digest algorithm. |


| Type Name           | Type Definition               | Description                                 |
|:--------------------|:------------------------------|:--------------------------------------------|
| **Hashes$Sha3-512** | String (%^[a-fA-F0-9]{128}$%) | Specifies the MD5 message digest algorithm. |


| Type Name         | Type Definition                     | Description                                 |
|:------------------|:------------------------------------|:--------------------------------------------|
| **Hashes$Ssdeep** | String (%^[a-zA-Z0-9/+:.]{1,128}$%) | Specifies the MD5 message digest algorithm. |


| Type Name       | Type Definition              | Description                                 |
|:----------------|:-----------------------------|:--------------------------------------------|
| **Hashes$Tlsh** | String (%^[a-zA-Z0-9]{70}$%) | Specifies the MD5 message digest algorithm. |


| Type Name                           | Type Definition | Description                                                                       |
|:------------------------------------|:----------------|:----------------------------------------------------------------------------------|
| **Http-request-ext$Request-header** | ArrayOf(String) | Specifies the value (typically a resource path) portion of the HTTP request line. |


| Type Name              | Type Definition        | Description                                                                   |
|:-----------------------|:-----------------------|:------------------------------------------------------------------------------|
| **Socket-ext$Options** | ArrayOf(socket_option) | Specifies any options (SO_*) that may be used by the socket, as a dictionary. |


| Type Name                        | Type Definition | Description                                                                                       |
|:---------------------------------|:----------------|:--------------------------------------------------------------------------------------------------|
| **Socket-ext$Socket-descriptor** | Integer{0..*}   | Specifies the socket file descriptor value associated with the socket, as a non-negative integer. |


| Type Name                       | Type Definition                                                | Description |
|:--------------------------------|:---------------------------------------------------------------|:------------|
| **Socket-option$Socket-option** | String (%^(SO|ICMP|ICMP6|IP|IPV6|MCAST|TCP|IRLMP)(_[A-Z]+)+$%) |             |


| Type Name                              | Type Definition | Description |
|:---------------------------------------|:----------------|:------------|
| **Startup-info-dictionary$Lpreserved** | String          |             |


| Type Name                               | Type Definition | Description |
|:----------------------------------------|:----------------|:------------|
| **Startup-info-dictionary$Lpreserved2** | String          |             |


| Type Name                               | Type Definition | Description |
|:----------------------------------------|:----------------|:------------|
| **Startup-info-dictionary$Cbreserved2** | Integer{0..*}   |             |


| Type Name                            | Type Definition       | Description                                         |
|:-------------------------------------|:----------------------|:----------------------------------------------------|
| **Windows-service-ext$Descriptions** | ArrayOf(String){1..*} | Specifies the descriptions defined for the service. |


| Type Name                                | Type Definition | Description                                                                           |
|:-----------------------------------------|:----------------|:--------------------------------------------------------------------------------------|
| **Windows-service-ext$Service-dll-refs** | ArrayOf(String) | Specifies the DLLs loaded by the service, as a reference to one or more File Objects. |


| Type Name                | Type Definition                                   | Description |
|:-------------------------|:--------------------------------------------------|:------------|
| **Extensions$Extension** | String (%^([a-z][a-z0-9]*)+(-[a-z0-9]+)*\\-ext$%) |             |


| Type Name            | Type Definition       | Description |
|:---------------------|:----------------------|:------------|
| **Properties$Array** | ArrayOf(String){1..*} |             |
