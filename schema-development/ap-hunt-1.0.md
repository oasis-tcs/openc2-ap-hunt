## Schema
|                . | .                                                                                                         |
|-----------------:|:----------------------------------------------------------------------------------------------------------|
|     **package:** | https://github.com/oasis-tcs/openc2-ap-hunt                                                               |
|     **version:** | 0-wd01                                                                                                    |
|       **title:** | Threat Hunting Profile                                                                                    |
| **description:** | Data definitions for Threat Hunting (TH) functions                                                        |
|  **namespaces:** | **ls**: http://oasis-open.org/openc2/oc2ls-types/v1.1 **th**: https://github.com/oasis-tcs/openc2-ap-hunt |
|     **exports:** | AP-Target, AP-Args, AP-Specifiers, AP-Results, Huntargs, StixObject                                       |

**_Type: Action (Enumerated)_**

| ID | Name            | Description |
|---:|:----------------|:------------|
|  3 | **query**       |             |
| 30 | **investigate** |             |

**_Type: Target (Enumerated)_**

| ID | Name         | Description |
|---:|:-------------|:------------|
|  9 | **features** |             |
|  0 | **th**  |             |

**_Type: Args (Enumerated)_**

| ID | Name                   | Description |
|---:|:-----------------------|:------------|
|  1 | **start_time**         |             |
|  2 | **stop_time**          |             |
|  3 | **duration**           |             |
|  4 | **response_requested** |             |
|  0 | **th**            |             |

**_Type: Actuator (Enumerated)_**

| ID | Name        | Description |
|---:|:------------|:------------|
|  0 | **ap_name** |             |

**_Type: Results (Enumerated)_**

| ID | Name           | Description |
|---:|:---------------|:------------|
|  1 | **versions**   |             |
|  2 | **profiles**   |             |
|  3 | **pairs**      |             |
|  4 | **rate_limit** |             |
|  5 | **args**       |             |
|  0 | **th**    |             |

**_Type: Pairs (Enumerated)_**

| ID | Name                                             | Description |
|---:|:-------------------------------------------------|:------------|
|  3 | **query: features, /huntbooks, /datasources**                              |             |
| 30 | **investigate: /hunt** |             |

**_Type: AP-Target (Choice)_**

| ID | Name            | Type   | # | Description      |
|---:|:----------------|:-------|--:|:-----------------|
|  1 | **hunt**        | String | 1 | description here |
|  2 | **huntbooks**   | String | 1 | description here |
|  3 | **datasources** | String | 1 | description here |

**_Type: AP-Args (Map{1..*})_**

| ID | Name         | Type     | # | Description                                                   |
|---:|:-------------|:---------|--:|:--------------------------------------------------------------|
|  1 | **huntargs** | Huntargs | 1 | Arguments for use in conjunction with huntbook implementation |

**_Type: AP-Specifiers (Map{1..*})_**

| ID | Name | Type | # | Description |
|---:|:-----|:-----|--:|:------------|

**_Type: AP-Results (Map{1..*})_**

| ID | Name            | Type                   | # | Description                                          |
|---:|:----------------|:-----------------------|--:|:-----------------------------------------------------|
|  1 | **huntbooks**   | Ap-results$Huntbooks   | 1 | Huntbook names returned by query huntbooks           |
|  2 | **datasources** | Ap-results$Datasources | 1 | Datasource identifiers returned by query datasources |

**_Type: Huntargs (Map{1..*})_**

| ID | Name            | Type                 | # | Description                            |
|---:|:----------------|:---------------------|--:|:---------------------------------------|
|  1 | **string_arg**  | Huntargs$String_arg  | 1 | string arguments supplied as huntargs  |
|  2 | **integer_arg** | Huntargs$Integer_arg | 1 | integer arguments supplied as huntargs |
|  3 | **stix**        | Huntargs$Stix        | 1 | stix arguments supplied as huntargs    |

**_Type: StixObject (Map{1..*})_**

| ID | Name | Type | # | Description |
|---:|:-----|:-----|--:|:------------|


| Type Name               | Type Definition       | Description                           |
|:------------------------|:----------------------|:--------------------------------------|
| **Huntargs$String_arg** | ArrayOf(String){1..*} | string arguments supplied as huntargs |


| Type Name                | Type Definition        | Description                            |
|:-------------------------|:-----------------------|:---------------------------------------|
| **Huntargs$Integer_arg** | ArrayOf(Integer){1..*} | integer arguments supplied as huntargs |


| Type Name         | Type Definition           | Description                         |
|:------------------|:--------------------------|:------------------------------------|
| **Huntargs$Stix** | ArrayOf(StixObject){1..*} | stix arguments supplied as huntargs |


| Type Name                | Type Definition | Description                                |
|:-------------------------|:----------------|:-------------------------------------------|
| **Ap-results$Huntbooks** | ArrayOf(String) | Huntbook names returned by query huntbooks |


| Type Name                  | Type Definition | Description                                          |
|:---------------------------|:----------------|:-----------------------------------------------------|
| **Ap-results$Datasources** | ArrayOf(String) | Datasource identifiers returned by query datasources |
