
![OASIS Logo](http://docs.oasis-open.org/templates/OASISLogo-v3.0.png)

-------

# OpenC2 Actuator Profile for Threat Hunting Version 1.0

## Committee Specification Draft 01

## 02 December 2022

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
This specification defines an actuator profile to automate management of cyber threat hunting activities using OpenC2. Threat hunting is the process of proactively and iteratively searching through networks and on endpoints to detect and isolate cyber observables that may indicate threats that evade existing security solutions. This actuator profile defines the OpenC2 Actions, Targets, Arguments, and Specifiers along with conformance clauses to enable the operation of OpenC2 Producers and Consumers in the context of cyber threat hunting. It covers invocation of stored hunting processes (e.g., “hunt books”), passing of hunt parameters, selection of analytics to apply to hunt data, and the expected type(s) and format(s) of information returned by hunting processes.

#### Status:
This document was last revised or approved by the OASIS Open Command and Control (OpenC2) TC on the above date. The level of approval is also listed above. Check the "Latest stage" location noted above for possible later revisions of this document. Any other numbered Versions and other technical work produced by the Technical Committee (TC) are listed at https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2#technical.

TC members should send comments on this specification to the TC's email list. Others should send comments to the TC's public comment list, after subscribing to it by following the instructions at the "[Send A Comment](https://www.oasis-open.org/committees/comments/index.php?wg_abbrev=)" button on the TC's web page at https://www.oasis-open.org/committees/openc2/.

This specification is provided under the [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr/#Non-Assertion-Mode) Mode of the OASIS IPR Policy, the mode chosen when the Technical Committee was established. For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of patent licensing terms, please refer to the Intellectual Property Rights section of the TC's web page (https://www.oasis-open.org/committees/openc2/ipr.php).

Note that any machine-readable content ([Computer Language Definitions](https://www.oasis-open.org/policies-guidelines/tc-process-2017-05-26/#wpComponentsCompLang)) declared Normative for this Work Product is provided in separate plain text files. In the event of a discrepancy between any such plain text file and display content in the Work Product's prose narrative document(s), the content in the separate plain text file prevails.

#### Key words:
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [[RFC2119](#rfc2119)] and [[RFC8174](#rfc8174)] when, and only when, they appear in all capitals, as shown here.

#### Citation format:
When referencing this specification the following citation format should be used:

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
    - [2.1.3 Type Definitions](#213-type-definitions)
    - [2.1.4 Command Arguments](#214-command-arguments)
    - [2.1.5 Actuator Specifiers](#215-actuator-specifiers)
  - [2.2 OpenC2 Response Components](#22-openc2-response-components)
    - [2.2.1 Response Status Codes](#221-response-status-codes)
  - [2.3 OpenC2 Commands](#23-openc2-commands)
    - [2.3.1 Query](#231-query)
    - [2.3.2 Investigate](#232-investigate)
- [3 Conformance](#3-conformance)
- [Appendix A. References](#appendix-a-references)
- [Appendix B. Safety, Security and Privacy Considerations](#appendix-b-safety-security-and-privacy-considerations)
- [Appendix C. Acknowledgments](#appendix-c-acknowledgments)
- [Appendix D. Revision History](#appendix-d-revision-history)
- [Appendix E. Threat Hunting Command / Response Examples](#appendix-e-threat-hunting-command--response-examples)
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

### 1.2.2 Acronyms and abbreviations

### 1.2.3 Document conventions

- Naming conventions
- Font colors and styles
- Typographic conventions

## 1.5 Overview

## 1.6 Goal

## 1.7 Purpose and Scope
-------

# 2 2 OpenC2 Language Binding for Threat Hunting

## 2.1 OpenC2 Command Components

### 2.1.1 Actions

### 2.1.2 Targets

### 2.1.3 Type Definitions

### 2.1.4 Command Arguments

### 2.1.5 Actuator Specifiers

## 2.2 OpenC2 Response Components

### 2.2.1 Response Status Codes

## 2.3 OpenC2 Commands

### 2.3.1 Query

### 2.3.2 Investigate

-------

# 3 Conformance
<!-- Required section -->

(Note: The [OASIS TC Process](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsConfClause) requires that a specification approved by the TC at the Committee Specification Public Review Draft, Committee Specification or OASIS Standard level must include a separate section, listing a set of numbered conformance clauses, to which any implementation of the specification must adhere in order to claim conformance to the specification (or any optional portion thereof). This is done by listing the conformance clauses here.
For the definition of "conformance clause," see [OASIS Defined Terms](https://www.oasis-open.org/policies-guidelines/oasis-defined-terms-2017-05-26#dConformanceClause).

See "Guidelines to Writing Conformance Clauses":  
http://docs.oasis-open.org/templates/TCHandbook/ConformanceGuidelines.html.

Remove this note before submitting for publication.)


-------

# Appendix A. References

<!-- Required section -->

This appendix contains the normative and informative references that are used in this document.

While any hyperlinks included in this appendix were valid at the time of publication, OASIS cannot guarantee their long-term validity.

## A.1 Normative References

The following documents are referenced in such a way that some or all of their content constitutes requirements of this document.

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

(Note: OASIS strongly recommends that Technical Committees consider issues that might affect safety, security, privacy, and/or data protection in implementations of their specification and document them for implementers and adopters. For some purposes, you may find it required, e.g. if you apply for IANA registration.

While it may not be immediately obvious how your specification might make systems vulnerable to attack, most specifications, because they involve communications between systems, message formats, or system settings, open potential channels for exploit. For example, IETF [[RFC3552](#rfc3552)] lists “eavesdropping, replay, message insertion, deletion, modification, and man-in-the-middle” as well as potential denial of service attacks as threats that must be considered and, if appropriate, addressed in IETF RFCs.

In addition to considering and describing foreseeable risks, this section should include guidance on how implementers and adopters can protect against these risks.

We encourage editors and TC members concerned with this subject to read _Guidelines for Writing RFC Text on Security Considerations_, IETF [[RFC3552](#rfc3552)], for more information.

Remove this note before submitting for publication.)

-------

# Appendix C. Acknowledgments

<!-- Required section -->

Note: A Work Product approved by the TC must include a list of people who participated in the development of the Work Product. This is generally done by collecting the list of names in this appendix. This list shall be initially compiled by the Chair, and any Member of the TC may add or remove their names from the list by request. Remove this note before submitting for publication.

## C.1 Special Thanks

<!-- This is an optional subsection to call out contributions from TC members. If a TC wants to thank non-TC members then they should avoid using the term "contribution" and instead thank them for their "expertise" or "assistance". -->

Substantial contributions to this document from the following individuals are gratefully acknowledged:

Participant Name, Affiliation or "Individual Member"

## C.2 Participants

<!-- A TC can determine who they list here, however, TC Observers must not be listed. It is common practice for TCs to list everyone that was part of the TC during the creation of the document, but this is ultimately a TC decision on who they want to list and not list. -->

The following individuals have participated in the creation of this specification and are gratefully acknowledged:

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
