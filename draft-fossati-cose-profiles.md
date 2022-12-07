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
# area: AREA
# workgroup: WG Working Group
keyword:
 - COSE
 - profiling
venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "thomas-fossati/draft-fossati-cose-profile"
  latest: "https://thomas-fossati.github.io/draft-fossati-cose-profile/draft-fossati-cose-profiles.html"

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

A COSE profile:

* MUST be specified in a document
* MUST NOT change the syntax or semantics of any already defined header attribute
* MAY define new header attributes
  * if so, it MUST provide their definition in the same document
* MUST use CDDL to fully specify the syntax rules for the profile
* MUST use the `COSE_profile` header attribute in the protected header
  * The value of `COSE_profile` MUST be global unique via:
    * IANA registry
    * using an OID or URI / CRI
    * using a UUID
  * The chosen value SHOULD be appropriate for the intended usage scope (e.g., a small value when used in constrained node environments)
* MAY define its own COSE tag
* SHOULD define its complementary media-type and content-format

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
