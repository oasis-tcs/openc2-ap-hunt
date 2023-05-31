
![OASIS Logo](http://docs.oasis-open.org/templates/OASISLogo-v3.0.png)

-------

# OpenC2 Actuator Profile for Threat Hunting Version 1.0

## WIP for WD01 of Committee Specification Draft 01

## dd Month 2023

&nbsp;

<!-- URI list start (commented out except during publication by OASIS TC Admin)

#### This stage:
https://docs.oasis-open.org/openc2/ap-hunt/v1.0/csd01/ap-hunt-v1.0-csd01.md (Authoritative) \
https://docs.oasis-open.org/openc2/ap-hunt/v1.0/csd01/ap-hunt-v1.0-csd01.html \
https://docs.oasis-open.org/openc2/ap-hunt/v1.0/csd01/ap-hunt-v1.0-csd01.pdf

#### Previous stage:
N/A

#### Latest stage:
https://docs.oasis-open.org/openc2/ap-hunt/v1.0/ap-hunt-v1.0.md (Authoritative) \
https://docs.oasis-open.org/openc2/ap-hunt/v1.0/ap-hunt-v1.0.html \
https://docs.oasis-open.org/openc2/ap-hunt/v1.0/ap-hunt-v1.0.pdf

URI list end (commented out except during publication by OASIS TC Admin) -->

#### Technical Committee:
[OASIS Open Command and Control (OpenC2) TC](https://www.oasis-open.org/committees/openc2/)

#### Chairs:
Duncan Sparrell (duncan@sfractal.com), [sFractal Consulting LLC](https://www.sfractal.com/) \
Michael Rosa (mjrosa@nsa.gov), [National Security Agency](https://www.nsa.gov/)

#### Editor:
David Lemire (david.lemire@hii-tsd.com), [National Security Agency](https://www.nsa.gov/)

#### Additional artifacts:
This prose specification is one component of a Work Product that also includes:
* XML schemas: (list file names or directory name)
* Other parts (list titles and/or file names)
* `(Note: Any normative computer language definitions that are part of the Work Product, such as XML instances, schemas and Java(TM) code, including fragments of such, must be (a) well formed and valid, (b) provided in separate plain text files, (c) referenced from the Work Product; and (d) where any definition in these separate files disagrees with the definition found in the specification, the definition in the separate file prevails. Remove this note before submitting for publication.)`

#### Related work:
This specification is related to:
* _Open Command and Control (OpenC2) Language Specification Version 1.1_. Edited by Duncan Sparrell and Toby Considine. Latest stage: https://docs.oasis-open.org/openc2/oc2ls/v1.1/oc2ls-v1.1.html.

#### Abstract:
This specification defines an actuator profile to automate
management of cyber threat hunting activities using OpenC2.
Threat hunting is the process of proactively and iteratively
searching through networks and on endpoints to detect and isolate
cyber observables that may indicate threats that evade existing
security solutions. This actuator profile defines the OpenC2
Actions, Targets, Arguments, and Specifiers along with
conformance clauses to enable the operation of OpenC2 Producers
and Consumers in the context of cyber threat hunting. It covers
invocation of stored hunting processes (e.g., “hunt books”),
passing of hunt parameters, selection of analytics to apply to
hunt data, and the expected type(s) and format(s) of information
returned by hunting processes.

#### Status:
This document was last revised or approved by the OASIS Open
Command and Control (OpenC2) TC on the above date. The level of
approval is also listed above. Check the "Latest stage" location
noted above for possible later revisions of this document. Any
other numbered Versions and other technical work produced by the
Technical Committee (TC) are listed at
https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2#technical.

TC members should send comments on this specification to the TC's
email list. Others should send comments to the TC's public
comment list, after subscribing to it by following the
instructions at the "[Send A
Comment](https://www.oasis-open.org/committees/comments/index.php?wg_abbrev=)"
button on the TC's web page at
https://www.oasis-open.org/committees/openc2/.

This specification is provided under the
[Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr/#Non-Assertion-Mode)
Mode of the OASIS IPR Policy, the mode chosen when the Technical
Committee was established. For information on whether any patents
have been disclosed that may be essential to implementing this
specification, and any offers of patent licensing terms, please
refer to the Intellectual Property Rights section of the TC's web
page (https://www.oasis-open.org/committees/openc2/ipr.php).

Note that any machine-readable content ([Computer Language
Definitions](https://www.oasis-open.org/policies-guidelines/tc-process-2017-05-26/#wpComponentsCompLang))
declared Normative for this Work Product is provided in separate
plain text files. In the event of a discrepancy between any such
plain text file and display content in the Work Product's prose
narrative document(s), the content in the separate plain text
file prevails.

#### Key words:
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED",
"MAY", and "OPTIONAL" in this document are to be interpreted as
described in BCP 14 [[RFC2119](#rfc2119)] and
[[RFC8174](#rfc8174)] when, and only when, they appear in all
capitals, as shown here.

#### Citation format:
When referencing this specification the following citation format
should be used:

**[AP-Hunt-v1.0]**

_OpenC2 Actuator Profile for Threat Hunting Version 1.0_. Edited by Duncan Sparrell. 02 December 2022. OASIS Committee Specification Draft 01. https://docs.oasis-open.org/openc2/ap-hunt/v1.0/csd01/ap-hunt-v1.0-csd01.html. Latest stage: https://docs.oasis-open.org/openc2/ap-hunt/v1.0/ap-hunt-v1.0.html.

#### Notices
Copyright © OASIS Open 2022. All Rights Reserved.

Distributed under the terms of the OASIS [IPR Policy](https://www.oasis-open.org/policies-guidelines/ipr/).

The name "OASIS" is a trademark of [OASIS](https://www.oasis-open.org/), the owner and developer of this specification, and should be used only to refer to the organization and its official outputs.

For complete copyright information please see the full Notices section in an Appendix below.

-------

# Table of Contents
- [1 Introduction](#1-introduction)
  - [1.1 Changes from earlier versions](#11-changes-from-earlier-versions)
  - [1.2 Glossary](#12-glossary)
    - [1.2.1 Definitions of terms](#121-definitions-of-terms)
    - [1.2.2 Acronyms and abbreviations](#122-acronyms-and-abbreviations)
    - [1.2.3 Document conventions](#123-document-conventions)
  - [1.5 Overview](#15-overview)
  - [1.6 Goal](#16-goal)
  - [1.7 Purpose and Scope](#17-purpose-and-scope)
- [2 2 OpenC2 Language Binding for Threat Hunting](#2-2-openc2-language-binding-for-threat-hunting)
  - [2.1 OpenC2 Command Components](#21-openc2-command-components)
    - [2.1.1 Actions](#211-actions)
    - [2.1.2 Targets](#212-targets)
      - [2.1.2.1 Common Targets](#2121-common-targets)
      - [2.1.2.2 Threat Hunting Targets](#2122-threat-hunting-targets)
    - [2.1.3 Type Definitions](#213-type-definitions)
      - [Table 2.1.3-1 AP Target Types](#table-213-1-ap-target-types)
      - [Table 2.1.3-2 AP Arg Types](#table-213-2-ap-arg-types)
      - [Table 2.1.3-3 AP Huntargs Type](#table-213-3-ap-huntargs-type)
    - [2.1.4 Command Arguments](#214-command-arguments)
      - [**Table 2.1.4-1. Command Arguments Unique to Theat Hunting**](#table-214-1-command-arguments-unique-to-theat-hunting)
    - [2.1.5 Actuator Specifiers](#215-actuator-specifiers)
      - [Table 2.1.5-1 AP Huntbook Actuator Type](#table-215-1-ap-huntbook-actuator-type)
      - [Table 2.1.5-2 AP Huntbook Specifiers Type](#table-215-2-ap-huntbook-specifiers-type)
  - [2.2 OpenC2 Response Components](#22-openc2-response-components)
    - [Table 2.2-1 Threat Hunting Reponse Components](#table-22-1-threat-hunting-reponse-components)
    - [Table 2.2-2 Threat Hunting Reponse Type: Huntbook Info](#table-22-2-threat-hunting-reponse-type-huntbook-info)
    - [Table 2.2-3 Threat Hunting Reponse Type: Datasource Array](#table-22-3-threat-hunting-reponse-type-datasource-array)
    - [2.2.1 Response Status Codes](#221-response-status-codes)
  - [2.3 OpenC2 Commands](#23-openc2-commands)
    - [**Table 2.3-1 Command Matrix**](#table-23-1-command-matrix)
    - [**Table 2.3-2 Command Arguments Matrix**](#table-23-2-command-arguments-matrix)
    - [2.3.1 Query](#231-query)
      - [2.3.1.1 Query Features](#2311-query-features)
      - [2.3.1.2 Query /huntbooks](#2312-query-huntbooks)
      - [2.3.1.3 Query /datasources](#2313-query-datasources)
    - [2.3.2 Investigate /hunt](#232-investigate-hunt)
- [3 Conformance](#3-conformance)
- [Appendix A. References](#appendix-a-references)
  - [A.1 Normative References](#a1-normative-references)
          - [\[OpenC2-Lang-v1.1\]](#openc2-lang-v11)
          - [\[RFC2119\]](#rfc2119)
          - [\[RFC8174\]](#rfc8174)
  - [A.2 Informative References](#a2-informative-references)
          - [\[RFC3552\]](#rfc3552)
- [Appendix B. Safety, Security and Privacy Considerations](#appendix-b-safety-security-and-privacy-considerations)
- [Appendix C. Acknowledgments](#appendix-c-acknowledgments)
  - [C.1 Special Thanks](#c1-special-thanks)
  - [C.2 Participants](#c2-participants)
- [Appendix D. Revision History](#appendix-d-revision-history)
- [Appendix E. Threat Hunting Command / Response Examples](#appendix-e-threat-hunting-command--response-examples)
  - [E.1 Example 1: Query Features](#e1-example-1-query-features)
  - [E.2 Example 2: Query Huntbooks](#e2-example-2-query-huntbooks)
  - [E.3 Example 3: Investigate Hunt](#e3-example-3-investigate-hunt)
  - [}](#)
- [Appendix F. Notices](#appendix-f-notices)


-------

# 1 Introduction

<!-- All text is normative unless otherwise labeled -->

Introductory text.

## 1.1 Changes from earlier versions

<!-- Optional section -->

## 1.2 Glossary

<!-- Optional section with suggested subsections -->

### 1.2.1 Definitions of terms

> **NOTE:** copied from SBOM AP draft; review & update as appropriate. Remove this note when done.

_This section is normative._

* **Action**: The task or activity to be performed (e.g.,
  'deny').
* **Actuator**: The function performed by the Consumer that
  executes the Command (e.g., 'Stateless Packet Filtering').

* **Argument**: A property of a Command that provides additional
  information on how to perform the Command, such as date/time,
  periodicity, duration, etc.
* **Command**: A Message defined by an Action-Target pair that is
  sent from a Producer and received by a Consumer.
* **Consumer**: A managed device / application that receives
  Commands. Note that a single device / application can have both
  Consumer and Producer capabilities.
* **Message**: A content- and transport-independent set of
  elements conveyed between Consumers and Producers.
* **Producer**: A manager application that sends Commands.
* **Response**: A Message from a Consumer to a Producer
  acknowledging a Command or returning the requested resources or
  status to a previously received Command.
* **Specifier**: A property or field that identifies a Target or
  Actuator to some level of precision.
* **Target**: The object of the Action, i.e., the Action is
  performed on the Target (e.g., IP Address).


### 1.2.2 Acronyms and abbreviations

> **NOTE:** copied from SBOM AP draft; review & update as appropriate. Remove this note when done.

_This section is non-normative_

| Term | Expansion |
|:---|:---|
| AP | Actuator Profile |
| IPR | Intellectual Property Rights |
| JADN | JSON Abstract Data Notation |
| JSON | JavaScript Object Notation |
| OASIS | Organization for the Advancement of Structured Information Standards |
| RFC | Request for Comment |
| TC | Technical Committee |
| TH | Threat Hunting |
| URI | Uniform Resource Identifier |

### 1.2.3 Document conventions

- Naming conventions
- Font colors and styles
- Typographic conventions

## 1.5 Overview

## 1.6 Goal

## 1.7 Purpose and Scope
-------

# 2 2 OpenC2 Language Binding for Threat Hunting

> **NOTE:** copied from SBOM AP draft; review & update as
> appropriate. Remove this note when done.

_This section is normative_

This section defines the set of Actions, Targets, Specifiers, and
Arguments that are meaningful in the context of theat hunting.
This section also describes the appropriate format for the status
and properties of a Response frame. This section is organized
into three major subsections; Command Components, Response
Components and Commands.

Extensions to the Language Specification are defined in
accordance with [[OpenC2-Lang-v1.0]](#openc2-lang-v10), Section
3.1.5, where:

1. The unique name of the threat hunting schema is
   `oasis-open.org/openc2/v1.0/ap-hunt`.
2. The namespace identifier (nsid) referring to the threat
   hunting schema is:  `th`.
3. The definitions of and conformance requirements for these
   types are contained in this document.

## 2.1 OpenC2 Command Components

> **NOTE:** copied from SBOM AP draft; review & update as appropriate. Remove this note when done.

The components of an OpenC2 Command include Actions, Targets,
Actuators and associated Arguments and Specifiers. Appropriate
aggregation of the components will define a Command-body that is
meaningful in the context of threat hunting.

This specification identifies the applicable components of an
OpenC2 Command. The components of an OpenC2 Command include:

* Action:  A subset of the Actions defined in the OpenC2 Language
  Specification that are meaningful in the context of threat
  hunting.
    * This profile SHALL NOT define Actions that are external to
      Version 1.0 of the [OpenC2 Language
      Specification](#openc2-lang-v10)
    * This profile MAY augment the definition of the Actions in
      the context of threat hunting
    * This profile SHALL NOT define Actions in a manner that is
      inconsistent with version 1.0 of the OpenC2 Language
      Specification
* Target:  A subset of the Targets and Target-Specifiers defined
  in Version 1.0 of the OpenC2 Language Specification that are
  meaningful in the context of threat hunting and several Targets
  (and associated Specifiers) that are defined in this
  specification
* Arguments:  A subset of the Arguments defined in the Language
  Specification and a set of Arguments defined in this
  specification

> **NOTE:** Per [LS PR
> #404](https://github.com/oasis-tcs/openc2-oc2ls/pull/404), when
> the v2 LS progresses "Actuator" should become "Profile"

* Actuator:  A set of specifiers defined in this specification
  that are meaningful in the context of threat hunting

### 2.1.1 Actions

Table 2.1.1-1 presents the OpenC2 Actions defined in version 1.0
of the Language Specification which are meaningful in the context
of threat hunting. The particular Action/Target pairs that are
required or are optional are presented in [Section
2.3](#23-openc2-commands).

**Table 2.1.1-1. Actions Applicable to Threat Hunting**

**_Type: Action (Enumerated)_**

| ID | Name            | Description                                                                                            |
|---:|:----------------|:-------------------------------------------------------------------------------------------------------|
|  3 | **query**       | Initiate a request for information.                                                                    |
| 30 | **investigate** | Task the recipient to aggregate and report information as it pertains to a security event or incident. |

### 2.1.2 Targets

Table 2.1.2-1 summarizes the Targets defined in Version 1.0 of
the [[OpenC2-Lang-v1.0]](#openc2-lang-v10) as they relate to
threat hunting functionality. Table 2.1.2-2 summarizes the
Targets that are defined in this specification.

#### 2.1.2.1 Common Targets
Table 2.1.2-1 lists the Targets defined in the OpenC2 Language
Specification that are applicable to threat hunting. The
particular Action/Target pairs that are required or are optional
are presented in [Section 2.3](#23-openc2-commands).

**Table 2.1.2-1. Targets Applicable to Threat Hunting**

**_Type: Target (Choice)_**

| ID | Name | Type | Description |
| :--- | :--- | :--- | :--- |
| 9 | **features** | Features | A set of items such as Action/Target pairs, profiles versions, options that are supported by the Actuator. The Target is used with the query Action to determine an Actuator's capabilities |
| 1036 | **th** | Theat Hunting | Hunts, Huntbooks, Data sources |

The semantics/ requirements as they pertain to common targets:
* fill in if we have any

#### 2.1.2.2 Threat Hunting Targets
The list of common Targets is extended to include the additional
Targets defined in this section and referenced with the `th`
namespace.

**Table 2.1.2-2. Targets Unique to Threat Hunting**

**_Type: Target (Choice)_**

**_Type: AP-Target (Choice)_**

| ID | Name            | Type                | # | Description                                                                                            |
|---:|:----------------|:--------------------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **hunt**        | String              | 1 | A procedure to find a set of entities in the monitored environment that associates with a cyberthreat. |
|  2 | **huntbooks**   | Huntbook-Specifiers | 1 | TH Huntbook specifiers.                                                                                |
|  3 | **datasources** | String              | 1 |                                                                                                        |


### 2.1.3 Type Definitions

#### Table 2.1.3-1 AP Target Types

**_Type: AP-Target (Choice)_**

| ID | Name            | Type                | # | Description                                                                                            |
|---:|:----------------|:--------------------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **hunt**        | String              | 1 | A procedure to find a set of entities in the monitored environment that associates with a cyberthreat. |
|  2 | **huntbooks**   | Huntbook-Specifiers | 1 | TH Huntbook specifiers.                                                                                |
|  3 | **datasources** | String              | 1 |                                                                                                        |
#### Table 2.1.3-2 AP Arg Types

**_Type: AP-Args (Map)_**

| ID | Name         | Type     | # | Description                                                    |
|---:|:-------------|:---------|--:|:---------------------------------------------------------------|
|  1 | **huntargs** | Huntargs | 1 | Arguments for use in conjunction with huntbook implementation. |

#### Table 2.1.3-3 AP Huntargs Type


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


| Type Name               | Type Definition   | Description                                      |
|:------------------------|:------------------|:-------------------------------------------------|
| **Specified-Arg-Types** | ArrayOf(Arg-Type) | Return huntbooks that take these argument types. |


| Type Name               | Type Definition   | Description                                            |
|:------------------------|:------------------|:-------------------------------------------------------|
| **Specified-Arg-Names** | ArrayOf(Arg-Name) | Return huntbooks that take arguments with these names. |

Time ranges are used to specify the time period over which the
hunt invoked with an `investigate /hunt` command should examine
data.

| Type Name      | Type Definition    | Description                                  |
|:---------------|:-------------------|:---------------------------------------------|
| **Timeranges** | ArrayOf(Timerange) | a timerange used in the execution of a hunt. |

Time ranges may be be specified in absolute terms, with a
specific start and end time, or for a relative duration leading
up to the present time.

**_Type: Timerange (Choice)_**

| ID | Name                   | Type          | # | Description                                                             |
|---:|:-----------------------|:--------------|--:|:------------------------------------------------------------------------|
|  1 | **timerange_absolute** | Timerange-Abs | 1 | Absolute timerange, defined by a start and end time in ISO 8601 format. |
|  2 | **timerange_relative** | Timerange-Rel | 1 | Relative timerange, example '3, Days' for last 3 days.                  |

**_Type: Timerange-Abs (Record{2..*})_**

| ID | Name                | Type   | # | Description                        |
|---:|:--------------------|:-------|--:|:-----------------------------------|
|  1 | **hunt_start_time** | sco:timerange | 1 | Start time, as a STIX time string. |
|  2 | **hunt_stop_time**  | sco:timerange | 1 | Stop time, as a STIX time string.  |


Relative time ranges can be specified in units ranging from
seconds to days.

**_Type: Time-Unit (Enumerated)_**

| ID | Name        | Description |
|---:|:------------|:------------|
|  1 | **Days**    |             |
|  2 | **Hours**   |             |
|  3 | **Minutes** |             |
|  4 | **Seconds** |             |

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

### 2.1.4 Command Arguments

The list of common Command Arguments is extended to include the
additional Command Arguments defined in this section and
referenced with the `th` namespace.

#### **Table 2.1.4-1. Command Arguments Unique to Theat Hunting**

Standard OpenC2 Language arguments are available for using in threat hunting commands.

**_Type: Args (Enumerated)_**

|   ID | Name                   | Description |
|-----:|:-----------------------|:------------|
|    1 | **start_time**         |             |
|    2 | **stop_time**          |             |
|    3 | **duration**           |             |
|    4 | **response_requested** |             |
| 1036 | **th**                 |             |

### 2.1.5 Actuator Specifiers

#### Table 2.1.5-1 AP Huntbook Actuator Type

**_Type: Actuator (Enumerated)_**

|   ID | Name   | Description |
|-----:|:-------|:------------|
| 1036 | **th** |             |


#### Table 2.1.5-2 AP Huntbook Specifiers Type

**_Type: Huntbook-Specifiers (Map)_**

| ID | Name              | Type                | # | Description                                                             |
|---:|:------------------|:--------------------|--:|:------------------------------------------------------------------------|
|  1 | **path**          | String              | 1 | Return huntbooks at and below this filesystem location (absolute path). |
|  2 | **tags**          | Tags                | 1 | Return huntbooks with these keywords.                                   |
|  3 | **arg_types**     | Specified-Arg-Types | 1 | Return huntbooks that take these argument types.                        |
|  4 | **arg_names**     | Specified-Arg-Names | 1 | Return huntbooks that take these argument types.                        |
|  5 | **format_types**  | Return-Type         | 1 | Return huntbooks that produce these output types.                       |
|  6 | **return_format** | Huntbook-Sections   | 1 | For each huntbook returned, include these data items.                   |


## 2.2 OpenC2 Response Components

### Table 2.2-1 Threat Hunting Reponse Components

**_Type: AP-Results (Map{1..*})_**

| ID | Name              | Type                     | # | Description                                              |
|---:|:------------------|:-------------------------|--:|:---------------------------------------------------------|
|  1 | **huntbook_info** | Ap-results$Huntbook-info | 1 | Structured data returned by Query: Huntbooks.            |
|  2 | **datasources**   | Datasource-Array         | 1 | Datasource names and info returned by Query Datasources. |
|  3 | **stix_returns**  | sco:STIX-Cybersecurity-Observables | 1 | STIX SCO object returns                        |

### Table 2.2-2 Threat Hunting Reponse Type: Huntbook Info


| Type Name                    | Type Definition        | Description                                   |
|:-----------------------------|:-----------------------|:----------------------------------------------|
| **Ap-results$Huntbook-info** | ArrayOf(Huntbook-Info) | Structured data returned by Query: Huntbooks. |

### Table 2.2-3 Threat Hunting Reponse Type: Datasource Array


| Type Name            | Type Definition     | Description                                                  |
|:---------------------|:--------------------|:-------------------------------------------------------------|
| **Datasource-Array** | ArrayOf(Datasource) | An Array of Datasources, with multiple uses in Threathunting |

### 2.2.1 Response Status Codes

## 2.3 OpenC2 Commands

An OpenC2 Command consists of an Action/Target pair and
associated Specifiers and Arguments. This section enumerates the
allowed Commands and presents the associated Responses.

Table 2.3-1 defines the Commands that are valid in the context of
the threat huntung profile. An Action (the top row in Table
2.3-1) paired with a Target (the first column in Table 2.3-1)
defines a valid Command. The subsequent subsections provide the
property tables applicable to each OpenC2 Command.


### **Table 2.3-1 Command Matrix**

|                  | **query** | **investigate** |
|------------------|:---------:|:---------------:|
| **features**     |   valid   |                 |
| **/huntbooks**   |   valid   |                 |
| **/datasources** |   valid   |                 |
| **/hunt**        |           |      valid      |


Table 2.3-2 defines the Command Arguments that are valid for each
of the commands defines in the threat huntung profile. A Command
(the top row in Table 2.3-2) paired with an Argument (the first
column in Table 2.3-2) defines an allowable combination. The
subsection identified at the intersection of the Command/Argument
provides details applicable to each Command as influenced by the
Argument.

### **Table 2.3-2 Command Arguments Matrix**

|                        | **query <br>features** | **query<br>/huntbooks** | **query<br>/datasources** | **investigate<br>/hunt** |
|------------------------|:----------------------:|:-----------------------:|:-------------------------:|:------------------------:|
| **response_requested** |                        |                         |                           |                          |
| other argument #1      |                        |                         |                           |                          |
| other argument #2      |                        |                         |                           |                          |
|         **...**        |                        |                         |                           |                          |
| other argument _n_     |                        |                         |                           |                          |


### 2.3.1 Query

#### 2.3.1.1 Query Features

The `query features` Command MUST be implemented in accordance
with Version 1.0 of the [[OpenC2-Lang-v1.0]](#openc2-lang-v10).

#### 2.3.1.2 Query /huntbooks

The `query /huntbooks` command is used to identify the set of
huntbooks available from a specific threat hunting consumer.


#### 2.3.1.3 Query /datasources

The `query /datasources` command is used to identify the set of
data sources available from a specific threat hunting consumer.

### 2.3.2 Investigate /hunt

The `investigate /hunt` command is used to instigate the use of a
selected huntbook in combination with a specified set of threat
hunting arguments.

-------

# 3 Conformance
<!-- Required section -->

(Note: The [OASIS TC
Process](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsConfClause)
requires that a specification approved by the TC at the Committee
Specification Public Review Draft, Committee Specification or
OASIS Standard level must include a separate section, listing a
set of numbered conformance clauses, to which any implementation
of the specification must adhere in order to claim conformance to
the specification (or any optional portion thereof). This is done
by listing the conformance clauses here. For the definition of
"conformance clause," see [OASIS Defined
Terms](https://www.oasis-open.org/policies-guidelines/oasis-defined-terms-2017-05-26#dConformanceClause).

See "Guidelines to Writing Conformance Clauses":  
http://docs.oasis-open.org/templates/TCHandbook/ConformanceGuidelines.html.

Remove this note before submitting for publication.)


-------

# Appendix A. References

<!-- Required section -->

This appendix contains the normative and informative references
that are used in this document.

While any hyperlinks included in this appendix were valid at the
time of publication, OASIS cannot guarantee their long-term
validity.

## A.1 Normative References

The following documents are referenced in such a way that some or
all of their content constitutes requirements of this document.

(Reference sources:
For references to IETF RFCs, use the approved citation formats at:  
http://docs.oasis-open.org/templates/ietf-rfc-list/ietf-rfc-list.html.  
For references to W3C Recommendations, use the approved citation formats at:  
http://docs.oasis-open.org/templates/w3c-recommendations-list/w3c-recommendations-list.html.  
Remove this note before submitting for publication.)

###### [OpenC2-Lang-v1.1]
_Open Command and Control (OpenC2) Language Specification Version 1.1_. Edited by Duncan Sparrell and Toby Considine. Latest stage: https://docs.oasis-open.org/openc2/oc2ls/v1.1/oc2ls-v1.1.html
<!--
###### [OpenC2-HTTPS-v1.1]
_Specification for Transfer of OpenC2 Messages via HTTPS Version 1.1_. Edited by David Lemire. Latest stage: https://docs.oasis-open.org/openc2/open-impl-https/v1.1/open-impl-https-v1.1.html
###### [OpenC2-SLPF-v1.1]
_Open Command and Control (OpenC2) Profile for Stateless Packet Filtering Version 1.1_. Edited by Joe Brule, Duncan Sparrell, and Alex Everett. Latest stage: https://docs.oasis-open.org/openc2/oc2slpf/v1.1/oc2slpf-v1.1.html
-->
###### [RFC2119]
Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997, http://www.rfc-editor.org/info/rfc2119.
###### [RFC8174]
Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174, May 2017, http://www.rfc-editor.org/info/rfc8174.

## A.2 Informative References

###### [RFC3552]
Rescorla, E. and B. Korver, "Guidelines for Writing RFC Text on Security Considerations", BCP 72, RFC 3552, DOI 10.17487/RFC3552, July 2003, https://www.rfc-editor.org/info/rfc3552.

-------

# Appendix B. Safety, Security and Privacy Considerations

<!-- Optional section -->

(Note: OASIS strongly recommends that Technical Committees
consider issues that might affect safety, security, privacy,
and/or data protection in implementations of their specification
and document them for implementers and adopters. For some
purposes, you may find it required, e.g. if you apply for IANA
registration.

While it may not be immediately obvious how your specification
might make systems vulnerable to attack, most specifications,
because they involve communications between systems, message
formats, or system settings, open potential channels for exploit.
For example, IETF [[RFC3552](#rfc3552)] lists “eavesdropping,
replay, message insertion, deletion, modification, and
man-in-the-middle” as well as potential denial of service attacks
as threats that must be considered and, if appropriate, addressed
in IETF RFCs.

In addition to considering and describing foreseeable risks, this
section should include guidance on how implementers and adopters
can protect against these risks.

We encourage editors and TC members concerned with this subject
to read _Guidelines for Writing RFC Text on Security
Considerations_, IETF [[RFC3552](#rfc3552)], for more
information.

Remove this note before submitting for publication.)

-------

# Appendix C. Acknowledgments

<!-- Required section -->

Note: A Work Product approved by the TC must include a list of
people who participated in the development of the Work Product.
This is generally done by collecting the list of names in this
appendix. This list shall be initially compiled by the Chair, and
any Member of the TC may add or remove their names from the list
by request. Remove this note before submitting for publication.

## C.1 Special Thanks

<!-- This is an optional subsection to call out contributions from TC members. If a TC wants to thank non-TC members then they should avoid using the term "contribution" and instead thank them for their "expertise" or "assistance". -->

Substantial contributions to this document from the following
individuals are gratefully acknowledged:

Participant Name, Affiliation or "Individual Member"

## C.2 Participants

<!-- A TC can determine who they list here, however, TC Observers must not be listed. It is common practice for TCs to list everyone that was part of the TC during the creation of the document, but this is ultimately a TC decision on who they want to list and not list. -->

The following individuals have participated in the creation of
this specification and are gratefully acknowledged:

**OpenC2 TC Members:**

| First Name | Last Name | Company |
| :--- | :--- | :--- |
Philippe | Alman | Something Networks
Alex | Amirnovman | Company B
Kris | Anderman | Mini Micro
Darren | Anstman | Big Networks

-------

# Appendix D. Revision History

<!-- Optional section -->

| Revision | Date | Editor | Changes Made |
| :--- | :--- | :--- | :--- |
| ap-hunt-v1.0-wd01 | yyyy-mm-dd | Editor Name | Initial working draft |

-------

# Appendix E. Threat Hunting Command / Response Examples

## E.1 Example 1: Query Features

{
  "action": "query",
  "target": {
    "features": [
      "pairs"
    ]
  }
}

A Language Specification command, Query: Features is used to gather information from consumers about their OpenC2 capabilities. A Response may 

{
  "results": {
    "pairs": [
      "query: features, /huntbooks, /datasources",
      "investigate: /hunt"
    ]
  },
  "status": "OK"
}

## E.2 Example 2: Query Huntbooks

{
    "action": "query",
    "target": {
        "th": {
            "huntbooks": {
                "tags": "searchable_tag",
                "format_types": {
                    "var_name": "desired_return_variable"
                }
            }
        }
    }
}

Query is extended in this profile to include additional targets. Huntbooks and Datasources are available as Targets to provide data to gather information about Threat Hunting processes. 
This command makes use of the "tags" and "format_types" specifiers (with example values) to filter the list of threathunting processes are listed as available from the consumer.
This example command also makes use of the optional command_id field, that is not required to be sent in every command, but is supported in the OpenC2 Language Specification.

## E.3 Example 3: Investigate Hunt

{
    "action": "investigate",
    "target": {
        "th": {
            "hunt": {
                "path_relative": "path/name/example"
            }
        }
    },
    "args": {
        "response_requested": "status",
        "th": {
            "huntargs": {
                "timerange": {
                    "timerange_relative": {
                        "number": "15",
                        "time_unit": "Minutes"
                    }
                },
                "datasource": "Datasource_Name",
                "hunt_process": {
                    "uuid": "1234567890"
                }
            }
        }
    }
}
-------

# Appendix F. Notices

<!-- Required section. Do not modify. -->

Copyright © OASIS Open 2022. All Rights Reserved.

All capitalized terms in the following text have the meanings assigned to them in the OASIS Intellectual Property Rights Policy (the "OASIS IPR Policy"). The full [Policy](https://www.oasis-open.org/policies-guidelines/ipr/) may be found at the OASIS website.

This document and translations of it may be copied and furnished to others, and derivative works that comment on or otherwise explain it or assist in its implementation may be prepared, copied, published, and distributed, in whole or in part, without restriction of any kind, provided that the above copyright notice and this section are included on all such copies and derivative works. However, this document itself may not be modified in any way, including by removing the copyright notice or references to OASIS, except as needed for the purpose of developing any document or deliverable produced by an OASIS Technical Committee (in which case the rules applicable to copyrights, as set forth in the OASIS IPR Policy, must be followed) or as required to translate it into languages other than English.

The limited permissions granted above are perpetual and will not be revoked by OASIS or its successors or assigns.

This document and the information contained herein is provided on an "AS IS" basis and OASIS DISCLAIMS ALL WARRANTIES, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO ANY WARRANTY THAT THE USE OF THE INFORMATION HEREIN WILL NOT INFRINGE ANY OWNERSHIP RIGHTS OR ANY IMPLIED WARRANTIES OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE.

As stated in the OASIS IPR Policy, the following three paragraphs in brackets apply to OASIS Standards Final Deliverable documents (Committee Specification, Candidate OASIS Standard, OASIS Standard, or Approved Errata).

\[OASIS requests that any OASIS Party or any other party that believes it has patent claims that would necessarily be infringed by implementations of this OASIS Standards Final Deliverable, to notify OASIS TC Administrator and provide an indication of its willingness to grant patent licenses to such patent claims in a manner consistent with the IPR Mode of the OASIS Technical Committee that produced this deliverable.\]

\[OASIS invites any party to contact the OASIS TC Administrator if it is aware of a claim of ownership of any patent claims that would necessarily be infringed by implementations of this OASIS Standards Final Deliverable by a patent holder that is not willing to provide a license to such patent claims in a manner consistent with the IPR Mode of the OASIS Technical Committee that produced this OASIS Standards Final Deliverable. OASIS may include such claims on its website, but disclaims any obligation to do so.\]

\[OASIS takes no position regarding the validity or scope of any intellectual property or other rights that might be claimed to pertain to the implementation or use of the technology described in this OASIS Standards Final Deliverable or the extent to which any license under such rights might or might not be available; neither does it represent that it has made any effort to identify any such rights. Information on OASIS' procedures with respect to rights in any document or deliverable produced by an OASIS Technical Committee can be found on the OASIS website. Copies of claims of rights made available for publication and any assurances of licenses to be made available, or the result of an attempt made to obtain a general license or permission for the use of such proprietary rights by implementers or users of this OASIS Standards Final Deliverable, can be obtained from the OASIS TC Administrator. OASIS makes no representation that any information or list of intellectual property rights will at any time be complete, or that any claims in such list are, in fact, Essential Claims.\]

The name "OASIS" is a trademark of [OASIS](https://www.oasis-open.org/), the owner and developer of this specification, and should be used only to refer to the organization and its official outputs. OASIS welcomes reference to, and implementation and use of, specifications, while reserving the right to enforce its marks against misleading uses. Please see https://www.oasis-open.org/policies-guidelines/trademark/ for above guidance.
