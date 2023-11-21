
![OASIS Logo](http://docs.oasis-open.org/templates/OASISLogo-v3.0.png)

-------

# OpenC2 Actuator Profile for Threat Hunting Version 1.0

## WD01 of Committee Specification Draft 01

## 24 September 2023

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

_OpenC2 Actuator Profile for Threat Hunting Version 1.0_. Edited by David Lemire. 02 December 2022. OASIS Committee Specification Draft 01. https://docs.oasis-open.org/openc2/ap-hunt/v1.0/csd01/ap-hunt-v1.0-csd01.html. Latest stage: https://docs.oasis-open.org/openc2/ap-hunt/v1.0/ap-hunt-v1.0.html.

#### Notices
Copyright © OASIS Open 2022. All Rights Reserved.

Distributed under the terms of the OASIS [IPR Policy](https://www.oasis-open.org/policies-guidelines/ipr/).

The name "OASIS" is a trademark of [OASIS](https://www.oasis-open.org/), the owner and developer of this specification, and should be used only to refer to the organization and its official outputs.

For complete copyright information please see the full Notices section in an Appendix below.

-------

# Table of Contents
- [OpenC2 Actuator Profile for Threat Hunting Version 1.0](#openc2-actuator-profile-for-threat-hunting-version-10)
  - [WD01 of Committee Specification Draft 01](#wd01-of-committee-specification-draft-01)
  - [24 September 2023](#24-september-2023)
      - [Technical Committee:](#technical-committee)
      - [Chairs:](#chairs)
      - [Editor:](#editor)
      - [Additional artifacts:](#additional-artifacts)
      - [Related work:](#related-work)
      - [Abstract:](#abstract)
      - [Status:](#status)
      - [Key words:](#key-words)
      - [Citation format:](#citation-format)
      - [Notices](#notices)
- [Table of Contents](#table-of-contents)
- [1 Introduction](#1-introduction)
  - [1.1 Changes from earlier versions](#11-changes-from-earlier-versions)
  - [1.2 Glossary](#12-glossary)
    - [1.2.1 Definitions of terms](#121-definitions-of-terms)
      - [1.2.1.1  OpenC2 Terms](#1211--openc2-terms)
      - [1.2.1.2  Threat Hunting Terms](#1212--threat-hunting-terms)
    - [1.2.2 Acronyms and abbreviations](#122-acronyms-and-abbreviations)
    - [1.2.3 Document conventions](#123-document-conventions)
  - [1.5 Overview](#15-overview)
  - [1.6 Purpose and Scope](#16-purpose-and-scope)
- [2 OpenC2 Language Binding for Threat Hunting](#2-openc2-language-binding-for-threat-hunting)
  - [2.1 OpenC2 Command Components](#21-openc2-command-components)
    - [2.1.1 Actions](#211-actions)
        - [**Table 2.1.1-1. Actions Applicable to Threat Hunting**](#table-211-1-actions-applicable-to-threat-hunting)
    - [2.1.2 Targets](#212-targets)
      - [2.1.2.1 Common Targets](#2121-common-targets)
        - [**Table 2.1.2-1. Targets Applicable to Threat Hunting**](#table-212-1-targets-applicable-to-threat-hunting)
      - [2.1.2.2 Threat Hunting Targets](#2122-threat-hunting-targets)
        - [**Table 2.1.2-2. Targets Unique to Threat Hunting**](#table-212-2-targets-unique-to-threat-hunting)
    - [2.1.3 Type Definitions](#213-type-definitions)
        - [Table 2.1.3-1 Hunt Target Types](#table-213-1-hunt-target-types)
        - [Table 2.1.3-2 Hunt Arg Types](#table-213-2-hunt-arg-types)
        - [Table 2.1.3-3 Hunt Huntargs Type](#table-213-3-hunt-huntargs-type)
    - [2.1.4 Command Arguments](#214-command-arguments)
        - [**Table 2.1.4-1. Command Arguments Unique to Theat Hunting**](#table-214-1-command-arguments-unique-to-theat-hunting)
    - [2.1.5 Actuator Specifiers](#215-actuator-specifiers)
        - [Table 2.1.5-1 AP Hunt Actuator Type](#table-215-1-ap-hunt-actuator-type)
        - [Table 2.1.5-2 AP huntflow Specifiers Type](#table-215-2-ap-huntflow-specifiers-type)
  - [2.2 OpenC2 Response Components](#22-openc2-response-components)
        - [Table 2.2-1 Threat Hunting Reponse Components](#table-22-1-threat-hunting-reponse-components)
        - [Table 2.2-2 Threat Hunting Reponse Type: Huntflow Info](#table-22-2-threat-hunting-reponse-type-huntflow-info)
        - [Table 2.2-3 Threat Hunting Reponse Type: Datasource Array](#table-22-3-threat-hunting-reponse-type-datasource-array)
        - [Table 2.2-4 Threat Hunting Reponse Type: Inv-Returns](#table-22-4-threat-hunting-reponse-type-inv-returns)
        - [Table 2.2-5 Threat Hunting Reponse Type: Inv-Return](#table-22-5-threat-hunting-reponse-type-inv-return)
    - [2.2.1 Response Status Codes](#221-response-status-codes)
  - [2.3 OpenC2 Commands](#23-openc2-commands)
        - [**Table 2.3-1 Command Matrix**](#table-23-1-command-matrix)
        - [**Table 2.3-2 Command Arguments Matrix**](#table-23-2-command-arguments-matrix)
    - [2.3.1 Query](#231-query)
      - [2.3.1.1 Query Features](#2311-query-features)
      - [2.3.1.2 Query /huntflows](#2312-query-huntflows)
      - [2.3.1.3 Query /datasources](#2313-query-datasources)
    - [2.3.2 Investigate /hunt](#232-investigate-hunt)
- [3 Conformance](#3-conformance)
  - [3.1 Conformance Targets](#31-conformance-targets)
  - [3.2 Conformance Requirements](#32-conformance-requirements)
    - [3.2.1 General TH Conformance Requirements](#321-general-th-conformance-requirements)
    - [3.2.2 TH Producer Conformance Requirements](#322-th-producer-conformance-requirements)
  - [3.2.3 TH Consumer Conformance Requirements](#323-th-consumer-conformance-requirements)
- [Annex A. Schemas](#annex-a-schemas)
- [Appendix A. References](#appendix-a-references)
  - [A.1 Normative References](#a1-normative-references)
          - [\[OpenC2-Arch-v1.0\]](#openc2-arch-v10)
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
  - [E.2 Example 2: Query huntflows](#e2-example-2-query-huntflows)
  - [E.3 Example 3: Investigate Hunt](#e3-example-3-investigate-hunt)
- [Appendix F. Notices](#appendix-f-notices)


-------

# 1 Introduction

_The content in this section is non-normative, except where it is marked normative._

**Note:** This Actuator profile is consistent with Version 1.0 of
the OpenC2 Language Specification
([[OpenC2-Lang-v1.0]](#openc2-lang-v10)).

OpenC2 is a suite of specifications that enables command and
control of cyber defense systems and components. OpenC2 typically
uses a request-response paradigm where a Command is encoded by a
Producer (managing application) and transferred to a Consumer
(managed device or virtualized function) using a secure transfer
protocol, and the Consumer acts on the request and responds with
status and any other requested information. An overview of the concepts
that underlie OpenC2 and the structure of the suite of
specifications can be found in the OpenC2 Architecture
Specification [[OpenC2-Arch-v1.0](#openc2-arch-v10)].

This specification defines an Actuator profile for **Threat
Hunting (TH)**. In particular, the specification comprises a set
of Actions, Targets and Target Specifiers, Command Arguments, and
Actuator Specifiers that integrates TH functionality with the
OpenC2 Command set. Through this Command set, cyber security
orchestrators may gain visibility into and provide control over
TH functionality in a manner that is independent of the instance
of the TH function. 

All components, devices, and systems that provide TH
functionality MUST implement the identified OpenC2 Actions,
Targets, Specifiers, and Arguments as specified in the
Conformance section of this specification. 

Though cyber defense components, devices, systems and/or
instances may implement multiple Actuator profiles, a particular
OpenC2 Message may reference at most a single Actuator profile.
The scope of this document is limited to TH. 

---

The rest of the specification is organized as follows: 

The remaining of [Section One](#1-introduction) includes
infomation about the terminology used, document conventions, and
purpose of this Actuator profile specification.

[Section Two](#2-openc2-language-binding) (normative) binds this
particular profile to the OpenC2 Language Specification. Section
Two enumerates the components of the language specification that
are meaningful in the context of TH and defines components that
are applicable to this distinct profile. Section Two also defines
the Commands (i.e., the Action/Target pairs) that are permitted
in the context of TH.

[Section Three](#3-conformance-statements) (normative) presents
definitive criteria for conformance so that cyber security
stakeholders can be assured that their products, instances and/or
integrations are compatible with OpenC2.

> **NOTE** - fill in information about annexes / appendices as they are defined.


## 1.1 Changes from earlier versions

<!-- Optional section -->

## 1.2 Glossary

<!-- Optional section with suggested subsections -->

### 1.2.1 Definitions of terms

_This section is normative._

#### 1.2.1.1  OpenC2 Terms

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

#### 1.2.1.2  Threat Hunting Terms

* **Threat Hunting**: Cyber threat hunting is a proactive security search
  through networks, endpoints, and datasets to hunt malicious, suspicious, or
  risky activities that have evaded detection by existing tools.<br>
Source: https://www.trellix.com/en-us/security-awareness/operations/what-is-cyber-threat-hunting.html

* **Huntbook**: ...
* **Huntflow**: ...
* **Datasource**: ...
* **Hunt Arguments**: ...


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
| SCO | STIX Cyber-observable Objects |
| STIX | Structured Threat Information eXpression |
| TC | Technical Committee |
| TH | Threat Hunting |
| URI | Uniform Resource Identifier |

### 1.2.3 Document conventions

- Naming conventions
- Font colors and styles
- Typographic conventions

## 1.5 Overview

Cyber threat hunting is a proactive security search through
networks, endpoints, and datasets to hunt malicious, suspicious,
or risky activities that have evaded detection by existing tools.
Various aspects of threat hunting can be manual,
machine-assisted, or automated. This AP defines the use of OpenC2
to invoke machine-assisted or automated threat hunting activities
and return associated results.  It assumes the availability to
the OpenC2 Consumer of relevant data sources that can be accessed
and defined huntflows that can be invoked, and applies the OpenC2
introspection model to enable an OpenC2 Producer to determine the
data sources and huntflows available from a particular Consumer. 

> Research links for threat hunting background:
> 
> * https://www.ibm.com/topics/threat-hunting
> * https://www.crowdstrike.com/cybersecurity-101/threat-hunting/
> * https://www.trellix.com/en-us/security-awareness/operations/what-is-cyber-threat-hunting.html 



## 1.6 Purpose and Scope

This Actuator profile specifies the set of Actions, Targets,
Specifiers, and Command Arguments that integrates the
investigation capabilities of threat hunting (TH) systems  with
the OpenC2 Command set. Through this Command set, cyber security
orchestrators may gain visibility into and provide control over
TH functionality in a manner that is independent of the instance
of the threat hunting solution.

All components, devices and systems that provide TH functionality
will implement the OpenC2 Actions, Targets, Specifiers and
Arguments identified as required in this document. Actions that
are applicable, but not necessarily required, for TH will be
identified as optional.

The purpose of this document is to:

* Identify the required OpenC2 Actions for Consumers with TH
  functionality
* Identify the required and optional Target types for each Action
  in the TH class of Actuators
* Identify Actuator-Specifiers and Arguments for each
  Action/Target pair that are applicable and/or unique to TH 
* Annotate each Action/Target pair with a justification and
  example, and provide sample OpenC2 Commands to a TH with
  corresponding Responses

This TH profile:

* Does not define or implement Actions beyond those defined in Version 1.0 of the [[OpenC2-Lang-v1.0]](#openc2-lang-v10)
* Is consistent with Version 1.0 of the OpenC2 Language Specification

-------

# 2 OpenC2 Language Binding for Threat Hunting

_This section is normative_

This section defines the set of Actions, Targets, Specifiers, and
Arguments that are meaningful in the context of TH. This section
also describes the appropriate format for the status and
properties of a Response frame. This section is organized into
three major subsections; Command Components, Response Components
and Commands.

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
      Version 1.0 of the [OpenC2 Language Specification](#openc2-lang-v10)
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

##### **Table 2.1.1-1. Actions Applicable to Threat Hunting**

**_Type: Action (Enumerated)_**

| ID | Name            | Description                                                                                            |
|---:|:----------------|:-------------------------------------------------------------------------------------------------------|
|  3 | **query**       | Initiate a request for information.                                                                    |
| 30 | **investigate** | Task the recipient to aggregate and report information as it pertains to a security event or incident. |



### 2.1.2 Targets

This threat hunting AP employs Targets defined by the OpenC2
Language Specification and Targets specific to threat hunting
functionality. The particular Action/Target pairs that are
required or are optional are presented in [Section 2.3](#23-openc2-commands).

#### 2.1.2.1 Common Targets
Table 2.1.2-1 lists the Targets defined in the OpenC2 Language
Specification that are applicable to threat hunting.

##### **Table 2.1.2-1. Targets Applicable to Threat Hunting** 


**_Type: Target (Choice)_**

|   ID | Name         | Type        | # | Description |
|-----:|:-------------|:------------|--:|:------------|
|    9 | **features** | ls:Features | 1 | A set of items such as Action/Target pairs, profiles versions, options that are supported by the Actuator. The Target is used with the query Action to determine an Actuator's capabilities.            |
| 1036 | **th**       | TH-Target   | 1 | Hunts, Huntflows, Data sources.            |





#### 2.1.2.2 Threat Hunting Targets
The list of common Targets is extended to include the additional
Targets defined in this section and referenced with the `th`
namespace.

##### **Table 2.1.2-2. Targets Unique to Threat Hunting**

**_Type: AP-Target (Choice)_**

> **NOTE:** Need better description for huntflows (or a
> definition in 1.2.1.2) and a description for data sources (or a
> definition in 1.2.1.2)
> **NOTE**: updated to v0.7 schema content

| ID | Name            | Type                | # | Description                                                                                            |
|---:|:----------------|:--------------------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **hunt**        | String              | 1 | A procedure to find a set of entities in the monitored environment that associates with a cyberthreat. |
|  2 | **huntflows**   | Huntflow-Specifiers | 1 | TH Huntflow specifiers.                                                                                |
|  3 | **datasources** | String              | 1 |                                                                                                        |


### 2.1.3 Type Definitions

Common data types are defined in [[OpenC2-Lang-V11](#openc2-lang-v11)]. This section defines data types associated with TH activities.

##### Table 2.1.3-1 Hunt Target Types

**_Type: TH-Target (Choice)_**

| ID | Name            | Type                | # | Description                                                                                            |
|---:|:----------------|:--------------------|--:|:-------------------------------------------------------------------------------------------------------|
|  1 | **hunt**        | String              | 1 | A procedure to find a set of entities in the monitored environment that associates with a cyberthreat. |
|  2 | **huntflows**   | Huntflow-Specifiers | 1 | TH Huntflow specifiers.                                                                                |
|  3 | **datasources** | String              | 1 |                                                                                                     


##### Table 2.1.3-2 Hunt Arg Types

**_Type: TH-Args (Map)_**

| ID | Name         | Type     | # | Description                                                |
|---:|:-------------|:---------|--:|:-----------------------------------------------------------|
|  1 | **huntargs** | Huntargs | 1 | Arguments for use in conjunction with hunt implementation. |






##### Table 2.1.3-3 Hunt Huntargs Type


**_Type: Huntargs (Record{1..*})_**

| ID | Name                | Type                               | # | Description                                                                                                      |
|---:|:--------------------|:-----------------------------------|--:|:-----------------------------------------------------------------------------------------------------------------|
|  1 | **string_args**     | ArrayOf(String)                    | 1 | string arguments supplied as huntargs.                                                                           |
|  2 | **integer_args**    | ArrayOf(Integer)                   | 1 | integer arguments supplied as huntargs.                                                                          |
|  3 | **typed_args**      | Typed-Arguments                    | 1 | Paired strings of named arguments.                                                                               |
|  4 | **native_oc2**      | OC2-Data                           | 1 | OC2 Language types supplied as huntargs.                                                                         |
|  5 | **stix**            | sco:STIX-Cybersecurity-Observables | 1 | STIX arguments supplied as huntargs.                                                                             |
|  6 | **stix_extensions** | oca:OCA-Extensions                 | 1 | STIX arguments extended with OCA extensions supplied as huntargs. TODO add a custom stix for oca-asset and event |
|  7 | **timeranges**      | Timeranges                         | 1 | Timeranges used in the execution of a hunt.                                                                      |
|  8 | **datasources**     | Datasource-Array                   | 1 | Available data sources for hunting. These may be a host monitor, an EDR, a SIEM, a firewall, etc.                |



| Type Name    | Type Definition                    | Description                                                                   |
|:-------------|:-----------------------------------|:------------------------------------------------------------------------------|
| **OC2-Data** | ArrayOf(Language-Spec-Types){1..*} | OC2-Data is an array of one or more types defined in the OpenC2 language spec |

**_Type: Language-Spec-Types (Record)_**

| ID | Name                  | Type               | # | Description                                                                                              |
|---:|:----------------------|:-------------------|--:|:---------------------------------------------------------------------------------------------------------|
|  1 | **artifact**          | ls:Artifact        | 1 | An array of bytes representing a file-like object or a link to that object.                              |
|  2 | **device**            | ls:Device          | 1 | The properties of a hardware device.                                                                     |
|  3 | **domain_name**       | ls:Domain-Name     | 1 | A network domain name.                                                                                   |
|  4 | **email-address**     | ls:Email-Addr      | 1 | A single email address                                                                                   |
|  5 | **file**              | ls:File            | 1 | Properties of a file.                                                                                    |
|  6 | **hashes**            | ls:Hashes          | 1 | Not used as an entity; use inside File or other attribute of another type. May be used as a query value. |
|  7 | **hostname**          | ls:Hostname        | 1 | Value must be a hostname as defined in [RFC1034], Section 3.1                                            |
|  8 | **idn_domain_name**   | ls:IDN-Domain-Name | 1 | An internationalized domain name.                                                                        |
|  9 | **idn_email_address** | ls:IDN-Email-Addr  | 1 | A single internationalized email address.                                                                |
| 10 | **ipv4_address**      | ls:IPv4-Addr       | 1 | IPv4 address as defined in [RFC0791].                                                                    |
| 11 | **ipv6_address**      | ls:IPv6-Addr       | 1 | IPv6 address as defined in [RFC8200].                                                                    |
| 12 | **ipv4_network**      | ls:IPv4-Net        | 1 | IPv4 network targeted by hunt activity.                                                                  |
| 13 | **ipv6_network**      | ls:IPv6-Net        | 1 | IPv6 network targeted by hunt activity.                                                                  |
| 14 | **ipv4_connection**   | ls:IPv4-Connection | 1 | A 5-tuple of source and destination IPv4 address ranges, source and destination ports, and protocol.     |
| 15 | **ipv6_connection**   | ls:IPv6-Connection | 1 | A 5-tuple of source and destination IPv6 address ranges, source and destination ports, and protocol.     |
| 16 | **iri**               | ls:IRI             | 1 | An internationalized resource identifier (IRI).                                                          |
| 17 | **mac_address**       | ls:MAC-Addr        | 1 | A Media Access Control (MAC) address - EUI-48 or EUI-64 as defined in [EUI].                             |
| 18 | **port**              | ls:Port            | 1 | Transport Protocol Port Number, [RFC6335]                                                                |
| 19 | **process**           | ls:Process         | 1 | Common properties of an instance of a computer program as executed on an operating system.               |
| 20 | **uri**               | ls:URI             | 1 | A uniform resource identifier (URI).                                                           


| Type Name               | Type Definition   | Description                                      |
|:------------------------|:------------------|:-------------------------------------------------|
| **Specified-Arg-Types** | ArrayOf(Arg-Type) | Return huntflows that take these argument types. |


| Type Name               | Type Definition   | Description                                            |
|:------------------------|:------------------|:-------------------------------------------------------|
| **Specified-Arg-Names** | ArrayOf(Arg-Name) | Return huntflows that take arguments with these names. |


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

| ID | Name                | Type      | # | Description                        |
|---:|:--------------------|:----------|--:|:-----------------------------------|
|  1 | **hunt_start_time** | timestamp | 1 | Start time, as a STIX time string. |
|  2 | **hunt_stop_time**  | timestamp | 1 | Stop time, as a STIX time string.  |


| Type Name     | Type Definition                                                     | Description |
|:--------------|:--------------------------------------------------------------------|:------------|
| **timestamp** | String (%^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}Z$%) |             |


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



| Type Name           | Type Definition           | Description                                           |
|:--------------------|:--------------------------|:------------------------------------------------------|
| **Typed-Arguments** | MapOf(Arg-Name, Arg-Type) | Argument names and types tied to a specific Huntflow. |



| Type Name    | Type Definition | Description                                                                                                                                                                         |
|:-------------|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Arg-Type** | String          | Argument types used by a Huntflow. Follow STIX naming conventions, with lowercase characters and hyphens replacing spaces. Common types include process, file, and network-traffic. |


| Type Name    | Type Definition | Description                                                                                                                |
|:-------------|:----------------|:---------------------------------------------------------------------------------------------------------------------------|
| **Arg-Name** | String          | Argument names used by a Huntflow. Follow C variable naming conventions. Examples include name, src_port, and x_unique_id. |

### 2.1.4 Command Arguments

The list of common Command Arguments is extended to include the
additional Command Arguments defined in this section and
referenced with the `th` namespace.

##### **Table 2.1.4-1. Command Arguments Unique to Theat Hunting**

Standard OpenC2 Language arguments are available for using in threat hunting commands.

**_Type: Args (Map{1..*})_**

|   ID | Name                   | Type                  | # | Description |
|-----:|:-----------------------|:----------------------|--:|:------------|
|    1 | **start_time**         | ls:Date-Time          | 1 |             |
|    2 | **stop_time**          | ls:Date-Time          | 1 |             |
|    3 | **duration**           | ls:Duration           | 1 |             |
|    4 | **response_requested** | ls:Response-Requested | 1 |             |
| 1036 | **th**                 | TH-Args               | 1 |             |

### 2.1.5 Actuator Specifiers

##### Table 2.1.5-1 AP Hunt Actuator Type

**_Type: Actuator (Enumerated)_**

|   ID | Name   | Description |
|-----:|:-------|:------------|
| 1036 | **th** |             |


##### Table 2.1.5-2 AP huntflow Specifiers Type

**_Type: Huntflow-Specifiers (Map)_**

| ID | Name              | Type                | # | Description                                                             |
|---:|:------------------|:--------------------|--:|:------------------------------------------------------------------------|
|  1 | **path**          | String              | 1 | Return huntflows at and below this filesystem location (absolute path). |
|  2 | **tags**          | Tags                | 1 | Return huntflows with these keywords.                                   |
|  3 | **arg_types**     | Specified-Arg-Types | 1 | Return huntflows that take these argument types.                        |
|  4 | **arg_names**     | Specified-Arg-Names | 1 | Return huntflows that take these argument types.                        |
|  5 | **format_types**  | Return-Type         | 1 | Return huntflows that produce these output types.                       |
|  6 | **return_format** | Huntflow-Sections   | 1 | For each huntflow returned, include these data items.                   |


| Type Name | Type Definition | Description                                 |
|:----------|:----------------|:--------------------------------------------|
| **Tags**  | ArrayOf(String) | Tags applied for search or filter purposes. |


**_Type: Return-Type (Record{2..*})_**

| ID | Name         | Type     | # | Description                                      |
|---:|:-------------|:---------|--:|:-------------------------------------------------|
|  1 | **var_name** | Arg-Name | 1 | Variable name to be returned by use of Huntflow. |
|  2 | **var_type** | Arg-Type | 1 | Type of data to be returned by use of Huntflow.  |


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





## 2.2 OpenC2 Response Components


**_Type: Results (Map{1..*})_**

|   ID | Name           | Type             | # | Description                                                 |
|-----:|:---------------|:-----------------|--:|:------------------------------------------------------------|
|    1 | **versions**   | ls:Version       | 1 | List of OpenC2 language versions supported by this Actuator |
|    2 | **profiles**   | ArrayOf(ls:Nsid) | 1 | List of profiles supported by this Actuator                 |
|    3 | **pairs**      | Pairs            | 1 | List of targets applicable to each supported Action         |
|    4 | **rate_limit** | Number{0..*}     | 1 |                                                             |
| 1036 | **th**         | TH-Results       | 1 |                                                             |



##### Table 2.2-1 Threat Hunting Reponse Components

**_Type: TH-Results (Map{1..*})_**

| ID | Name              | Type             | # | Description                                              |
|---:|:------------------|:-----------------|--:|:---------------------------------------------------------|
|  1 | **huntflow_info** | Huntflow-Array   | 1 | Structured data returned by Query: Huntflows.            |
|  2 | **datasources**   | Datasource-Array | 1 | Datasource names and info returned by Query Datasources. |
|  3 | **inv_returns**   | Inv-Returns      | 1 | STIX SCO object returns.                                 |

##### Table 2.2-2 Threat Hunting Reponse Type: Huntflow Info


| Type Name          | Type Definition        | Description                                   |
|:-------------------|:-----------------------|:----------------------------------------------|
| **Huntflow-Array** | ArrayOf(Huntflow-Info) | Structured data returned by Query: Huntflows. |



**_Type: Huntflow-Info (Record{1..*})_**

| ID | Name                 | Type            | # | Description                                           |
|---:|:---------------------|:----------------|--:|:------------------------------------------------------|
|  1 | **path**             | String          | 1 | Path used to identify a Huntflow in place of a name.  |
|  2 | **uniqueId**         | Integer{0..*}   | 1 | Unique ID associated with a specified Huntflow.       |
|  3 | **version**          | String          | 1 | Unique ID associated with a specified Huntflow.       |
|  4 | **args_required**    | Typed-Arguments | 1 | List of arguments used in the specified Huntflow.     |
|  5 | **expected_returns** | Typed-Arguments | 1 | Data returned by the specified Huntflows.             |
|  6 | **script**           | String          | 1 | Text of Hunt logic implemented by specified Huntflow. |




##### Table 2.2-3 Threat Hunting Reponse Type: Datasource Array

| Type Name            | Type Definition     | Description                                                  |
|:---------------------|:--------------------|:-------------------------------------------------------------|
| **Datasource-Array** | ArrayOf(Datasource) | An Array of Datasources, with multiple uses in Threathunting |


**_Type: Datasource (Record{1..*})_**

| ID | Name        | Type   | # | Description                                                 |
|---:|:------------|:-------|--:|:------------------------------------------------------------|
|  1 | **ds_name** | String | 1 | Name of a Datasource used by a Huntflow in Kestrel runtime. |
|  2 | **ds_tags** | Tags   | 1 | Tags applied to a Datasource for search or filter purposes. |


##### Table 2.2-4 Threat Hunting Reponse Type: Inv-Returns

| Type Name       | Type Definition           | Description                                       |
|:----------------|:--------------------------|:--------------------------------------------------|
| **Inv-Returns** | ArrayOf(Inv-Return){1..*} | Array of returns from threat hunt investigations. |


##### Table 2.2-5 Threat Hunting Reponse Type: Inv-Return

**_Type: Inv-Return (Record)_**

| ID | Name               | Type                               | # | Description                         |
|---:|:-------------------|:-----------------------------------|--:|:------------------------------------|
|  1 | **string_returns** | ArrayOf(String)                    | 1 | String return from an investigation |
|  2 | **stix_sco**       | sco:STIX-Cybersecurity-Observables | 1 | STIX SCO object returns             |


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


##### **Table 2.3-1 Command Matrix**

|                  | **query** | **investigate** |
|------------------|:---------:|:---------------:|
| **features**     |   valid   |                 |
| **/huntflows**   |   valid   |                 |
| **/datasources** |   valid   |                 |
| **/hunt**        |           |      valid      |


Table 2.3-2 defines the Command Arguments that are valid for each
of the commands defines in the threat huntung profile. A Command
(the top row in Table 2.3-2) paired with an Argument (the first
column in Table 2.3-2) defines an allowable combination. The
subsection identified at the intersection of the Command/Argument
provides details applicable to each Command as influenced by the
Argument.

##### **Table 2.3-2 Command Arguments Matrix**

|  |  | **query <br>features** | **query<br>/huntflows** | **query<br>/datasources** | **investigate<br>/hunt** |  |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
|  | **response_requested** | [2.3.1.1](#2311-query-features) | [2.3.1.2](#2312-query-huntflows) | [2.3.1.3](#2313-query-datasources) | [2.3.2](#232-investigate-hunt) |  |
|  | other argument #1 |  |  |  |  |  |
|  | other argument #2 |  |  |  |  |  |
|  | **...** |  |  |  |  |  |
|  | other argument _n_ |  |  |  |  |  |

### 2.3.1 Query

#### 2.3.1.1 Query Features

The `query features` Command MUST be implemented in accordance
with Version 1.0 of the [[OpenC2-Lang-v1.0]](#openc2-lang-v10).

#### 2.3.1.2 Query /huntflows

The `query /huntflows` command is used to identify the set of
huntflowss available from a specific threat hunting consumer.

OpenC2 Consumers that receive a `query /huntflows` Command:

 *  but cannot parse or process the Command
    -  MUST NOT respond with a OK/200
    -  SHOULD respond with status code 400
    -  MAY respond with the 500 status code
 *  but do not support the `/huntflows` Target
    -  MUST NOT respond with a OK/200
    -  SHOULD respond with status code 501
    -  SHOULD respond with "Command not supported" in the status text
    -  MAY respond with status code 500


#### 2.3.1.3 Query /datasources

The `query /datasources` command is used to identify the set of
data sources available from a specific threat hunting consumer.

OpenC2 Consumers that receive a `query /datasources` Command:

 *  but cannot parse or process the Command
    -  MUST NOT respond with a OK/200
    -  SHOULD respond with status code 400
    -  MAY respond with the 500 status code
 *  but do not support the `/datasources` Target
    -  MUST NOT respond with a OK/200
    -  SHOULD respond with status code 501
    -  SHOULD respond with "Command not supported" in the status text
    -  MAY respond with status code 500


### 2.3.2 Investigate /hunt

The `investigate /hunt` command is used to instigate the use of a
selected huntflow in combination with a specified set of threat
hunting arguments.

OpenC2 Producers that send `investigate /hunt` Commands:

 * MAY populate the Command Arguments field with _fill in with appropriate TH arguments_
 
OpenC2 Consumers that receive a `investigate /hunt` Command:

 *  but cannot parse or process the Command
    -  MUST NOT respond with a OK/200
    -  SHOULD respond with status code 400
    -  MAY respond with the 500 status code
 *  but do not support the `/hunt` Target
    -  MUST NOT respond with a OK/200
    -  SHOULD respond with status code 501
    -  SHOULD respond with "Command not supported" in the status text
    -  MAY respond with status code 500

-------

# 3 Conformance

_This section is normative._

========================================
>  The following rough approach to conformance was discussed and
>  approved at the 7 June 2023 working meeting. Delete this
>  material once the text in 3.1 and 3.2 is approved.

* Define 
  * Producer conformance target
  * Consumer conformance target
* Each conformance target:
  * MUST
    * conform to the Architecture and LS
    * implement `query features` (per LS)
    * implement `query /huntflows`, `investigate /hunt` (per AP)
  * SHOULD
    * implement at least one approved transfer spec
    * implement `query /datasources` (per AP)
  * make adjustments for argument handling as need determined

========================================

## 3.1 Conformance Targets

This AP defines two conformance targets:

 - **TH Producer** -- an OpenC2 Producer that creates and
   transmits requests consistent with this AP
 - **TH Consumer** -- an OpenC2 Consumer that receives and
   processes requests consistent with this AP and returns
   corresponding responses

## 3.2 Conformance Requirements

### 3.2.1 General TH Conformance Requirements

All TH Producers and Consumers MUST:

  1. Conform to the requirements of the [OpenC2 Architecture Specification](#openc2-arch-v10)
  2. Conform to the requirements of the [OpenC2 Language Specification](#openc2-lang-v11)

### 3.2.2 TH Producer Conformance Requirements

TH Producers MUST:

 1. Generate and transmit the `"query features"` command as
    defined in Section 4.1 of the [OpenC2 Language
    Specification](#openc2-lang-v11).
 2. Generate and transmit the `"query /huntflows"` command as
    defined in this specification and process corresponding
    responses.
 3. Generate and transmit the `"investigate /hunt"` command as
    defined in this specification and process corresponding
    responses.

TH Producers SHOULD:
 
 1. Conform with at least one OpenC2 transfer specification.
 2. Generate and transmit the `"query /datasources"` command as
    defined in this specification and process corresponding
    responses.
 
 
### 3.2.3 TH Consumer Conformance Requirements

TH Consumers MUST:

 1. Receive and process the `"query features"` command as defined
    in Section 4.1 of the [OpenC2 Language
    Specification](#openc2-lang-v11) and return corresponding
    responses. 
 2. Receive and process the `"query /huntflows"` command as
    defined in this specification and return corresponding
    responses.
 3. Receive and process the `"investigate /hunt"` command as
    defined in this specification and return corresponding
    responses.

TH Producers SHOULD:
 
 1. Conform with at least one OpenC2 transfer specification.
 2. Receive and process the `"query /datasources"` command as
    defined in this specification and return corresponding
    responses.
-------

# Annex A. Schemas

> **NOTE:**  This will become a standard section of OpenC2 APs to
> align with the ITU-T convention that an Annex is part of the
> normative content, whereas an Appendix is not.

This AP specification is composed of:
 * This specification document
 * The JADN schema for the TH AP, in the seperate file `ap-hunt.jadn`
 * The JADN schema for the TH AP in JDIL format, in the separate file `ap-hunt.jidl`

In the event of any conflict among these represenations, the contents of `ap-hunt.jadn` SHALL be considered authoritative.

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

###### [OpenC2-Arch-v1.0]

_Open Command and Control (OpenC2) Architecture Specification Version 1.0_. Edited by Duncan Sparrell. 30 September 2022. OASIS Committee Specification 01. https://docs.oasis-open.org/openc2/oc2arch/v1.0/cs01/oc2arch-v1.0-cs01.html. Latest stage: https://docs.oasis-open.org/openc2/oc2arch/v1.0/oc2arch-v1.0.html.

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

###### [TTP-Hunting]
Daszczyszak, R., Ellis, D., Luke, S., and Whitley, S, "TTP-Based Hunting", The MITRE Corporation, March 2019, https://www.mitre.org/sites/default/files/2021-11/prs-19-3892-ttp-based-hunting.pdf 

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

```{
  "action": "query",
  "target": {
    "features": [
      "pairs"
    ]
  }
}
```

A Language Specification command, Query: Features is used to gather information from consumers about their OpenC2 capabilities. A Response may 

```{
  "results": {
    "pairs": [
      "query: features, /huntflows, /datasources",
      "investigate: /hunt"
    ]
  },
  "status": "OK"
}
```
## E.2 Example 2: Query huntflows

```{
    "action": "query",
    "target": {
        "th": {
            "huntflows": {
                "tags": "searchable_tag",
                "format_types": {
                    "var_name": "desired_return_variable"
                }
            }
        }
    }
}
```
Query is extended in this profile to include additional targets. huntflows and Datasources are available as Targets to provide data to gather information about Threat Hunting processes. 
This command makes use of the "tags" and "format_types" specifiers (with example values) to filter the list of threathunting processes are listed as available from the consumer.
This example command also makes use of the optional command_id field, that is not required to be sent in every command, but is supported in the OpenC2 Language Specification.

## E.3 Example 3: Investigate Hunt

```
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
```
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
