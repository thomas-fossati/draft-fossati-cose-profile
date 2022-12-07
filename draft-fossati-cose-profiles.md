---

title: "COSE Profiles"
abbrev: "COSE Profiles"
category: std

docname: draft-fossati-cose-profiles-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: AREA
workgroup: WG Working Group
keyword:
 - COSE
 - profiling
venue:
  group: WG
  type: Working Group
  mail: WG@example.com
  arch: https://example.com/WG
  github: USER/REPO
  latest: https://example.com/LATEST

author:
 -
    fullname: Thomas Fossati
    organization: Arm Limited
    email: thomas.fossati@arm.com
 -
    fullname: Henk Birkholz
    organization: Fraunhofer SIT
    email: henk.birkholz@sit.fraunhofer.de

normative:

informative:


--- abstract

This document lays a set of rules for how to define COSE profiles.

--- middle

# Introduction

TODO Introduction


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Rules

1. MUST NOT change already defined header attributes
2. MAY define new header attributes
   a. if so, MUST define them in the same document
4. MUST use CDDL to fully specify the syntax rules for the profile
5. MUST use the COSE_profile header attribute in the protected header
   a. value of COSE_profile MUST be global unique via:
        - IANA registry
        - using an oid or [cu]ri
        - using a uuid
   b. type of value SHOULD be application appropriate (e.g., constrained node environments)
5. MAY be tagged in front of COSE tag
6. SHOULD define its complementary media-type/content-format

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
