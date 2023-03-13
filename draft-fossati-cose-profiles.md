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
area: "Security"
workgroup: "CBOR Object Signing and Encryption"
keyword:
 - COSE
 - profiling
venue:
  group: "CBOR Object Signing and Encryption"
  type: "Working Group"
  mail: "cose@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/cose/"
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
  RFC8610: cddl
  STD66:
    -: uri
    =: RFC3986
  STD96:
    -: cose
    =: RFC9052
  I-D.ietf-core-href: cri
  I-D.ietf-sacm-coswid: coswid
  RFC4122: uuid
  RFC9090: oid
  RFC8126: ianacons

informative:
  GlueCOSE:
    title: Test Vectors
    author:
      org: The GlueCOSE Community
    date: false
    target: https://github.com/gluecose/test-vectors

entity:
  SELF: "RFCthis"

--- abstract

COSE (STD96) is not an end-to-end system with guaranteed interoperability.
It is designed to serve a range of use cases and therefore it has a lot of options.
In general, two COSE implementations that want to interoperate require an agreement on which subset of COSE features they will use.
This document provides a set of rules for specifying such agreements as a "COSE profiles" and registers a new COSE header parameter for in-band signalling profile information.

--- middle

# Introduction

COSE {{-cose}} is not an end-end system with guaranteed interoperability.
It is designed to serve a range of use cases and therefore it has a lot of options.
In general, two COSE implementation that want to interoperate need to agree on which subset of COSE features they will be using.

This document provides a set rules for defining COSE profiles and registers a new COSE header parameter for in-band signalling of profile information.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Profiling Rules

A COSE profile:

* MUST be specified in a document
* MUST NOT change the syntax or semantics of any already defined
  header attribute
  * but does allow restricting their values
* MAY define new header attributes
  * if so, it MUST provide their definition in the same document
* MUST use CDDL {{-cddl}} to fully specify the syntax rules for the profile
* MUST use the `cose-profile` header attribute (see {{hdr-param}}) in the protected header
  * The value of `cose-profile` MUST be globally unique.  Possible choices include:
    * IANA registry ({{sec-profile-registry}})
    * using an OID {{-oid}}, URI {{-uri}} or CRI {{-cri}}
    * using a UUID {{-uuid}}
  * The chosen value SHOULD be appropriate for the intended usage scope (e.g., a short value when used in constrained node environments)
* MAY define its own CBOR tag that can be used together with, or in lieu of, the underlying COSE CBOR tag (Table 1, {{Section 2 of -cose}})
* SHOULD define its complementary media-type and content-format

[^tag]: (see https://github.com/thomas-fossati/draft-fossati-cose-profile/issues/3)

# COSE profile header parameter {#hdr-param}

~~~ cddl
COSE-profile = registered-profile / oid-profile / uri-profile
             / cri-profile / uuid-profile
registered-profile = int
oid-profile = oid ; tagged
uri-profile = ~uri ; unwrapped -- any tstr is a uri
cri-profile = cri
uuid-profile = uuid ; naked bstr is a UUID

uuid = bstr .size 16

; imported from RFC 9090
oid = #6.111(bstr)
; import from CRI spec when ready
cri = [*any]
~~~

# Profile Registration Template

* What is the profile identifier?
* Requires certain header keys?
* Constrains any header keys?
* Constrains any header values?
* Defines new header keys?
* Defines its own CBOR Tag?
* Defines its own Media Type?
* What payload(s) allows?

# CoSWID COSE Profile Definition

This section defines the COSE profile for CoSWID {{-coswid}}.

This definition is semantically and syntactically equivalent with what is
described in {{Section 7 of -coswid}}, with the exception of the explicit
CoSWID COSE profile indicator that is added to the protected header.



## CDDL Definition

~~~ cddl
protected-signed-coswid-header = {
  &(alg: 1) => int
  &(content-type: 3) => "application/swid+cbor"
  &(cose-profile-CPA: 13) => &(CoSWID-COSE-profile-CPA: 0)
  * cose-label => cose-values
}

cose-label = int / text
cose-values = any
~~~

## Checklist

* Mandatory header keys? YES
* Constrains header keys? NO
* Constrains header values? YES (alg is only int)
* New header keys? NO
* Defines its own CBOR Tag? YES
* Defines its own Media Type? YES

# Security Considerations

TODO Security

# IANA Considerations

## New COSE Profile Header Parameter

This document requests IANA to allocate a new header parameter
`cose-profile-CPA` (suggested value 13) in the "COSE Header Parameters"
{{!IANA.cose}} registry.

## COSE Profile Sub-registry {#sec-profile-registry}

This specification requests IANA to create a new sub-registry for COSE
{{!IANA.cose}}, with the policy "specification required" ({{Section 4.6 of
-ianacons}}).

Each entry in the registry must include:

{:vspace}
Key value:
: integer value for the profile

Brief description:
: a brief description

Change Controller:
: (see {{Section 2.3 of -ianacons}})

Reference:
: a reference document

The expert is requested to assign the shortest key values (1+0 and
1+1 encoding) to registrations that are likely to enjoy wide use and
can benefit from short encodings.

--- back

# GlueCOSE Test Cases

The community effort {{GlueCOSE}} provides test vectors for the COSE specification.

The CDDL definition for the test vector format used for COSE profiles will be provided in a future version of this document.

[^issue] https://github.com/ietf-rats-wg/draft-ietf-rats-corim/issues/4

# Acknowledgments
{:numbered="false"}

Laurence Lundblade who - unknowingly :-) - provided the introduction.

[^issue]: Tracked at:
