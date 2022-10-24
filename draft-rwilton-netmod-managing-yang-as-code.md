---
title: "Managing IETF YANG modules as code not documents"
abbrev: "YANG is code"
category: exp

docname: draft-rwilton-netmod-managing-yang-as-code-latest
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Operations and Management"
workgroup: "Network Modeling"
keyword:
 - YANG
 - Process experiment
venue:
  group: "Network Modeling"
  type: "Working Group"
  mail: "netmod@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/netmod/"
  github: "rgwilton/draft-rwilton-netmod-publishing-yang-as-code"
  latest: "https://rgwilton.github.io/draft-rwilton-netmod-publishing-yang-as-code/draft-rwilton-netmod-managing-yang-as-code.html"

author:
 -
    fullname: Robert Wilton
    organization: Cisco
    email: "rwilton@cisco.com"

normative:

informative:


--- abstract

TODO Abstract


--- middle

# Introduction

This document proposes that the IETF tries a process experiment for the management and evolution of YANG modules created and published by the IETF.  The goal is the make the process easier and more helpful, allowing YANG modules to be published more quickly without losing the benefits of having a stable and industry respected consensus process.

This is very much a -00 initial draft, and I'm seeking input from the WG as to whether these process changes make sense, input from the chairs as to whether these process changes are helpful.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Background

## Existing Process for publishing New IETF YANG Modules
Currently, IETF publishes YANG modules as extractable code assets within RFCs.  I.e., the YANG module source text is embedded directly in the RFC using CODE BEGINS/ENDS markers, and can be extracted via tooling, such as rfcstrip.  As such, the RFC should be regarded as the canonical reference to any embedded YANG Modules, but copies of the YANG modules are also available in the IANA YANG Module Names registry, YANG Catalog, and the YangModels/yang Github repository.

The key components of RFCs containing one or more YANG modules are generally:
 - An overview of the technology that the YANG module(s) cover
 - A high-level descriptions of key parts (e.g., containers and lists) of the YANG module(s),
 - YANG tree diagram {{?RFC8340}} output to show the schema structure for the YANG module(s) (sometimes snippets of the tree diagram output, potentially with a full copy in an appendix)
 - The YANG module code asset(s)
 - Relevant security considerations for the YANG module, and
 - Simple examples of using the YANG module demonstrated as instance data in XML or JSON that conforms to the YANG module schema.

## Problems with the existing Process

This section lists some of the potential problems with the existing IETF process of producing YANG models.  In some cases,  althogh the approach has issues, it has benefits also.

### Including code in the RFCs.



### Inter-dependency between YANG modules.

IETF YANG modules are being develeoped independently, but there are often dependencies between YANG modules.  Other industry efforts at creating common network management APIs take an approach of updating related version of the YANG modules at the time, ensure that any import dependencies are satisfied.

### A

YANG 1.0 and YANG 1.1 very strongly encourage only allowing backwards-compatible changes to YANG modules.  This is a good approach when modules are very stable, but has acted to slow down development of YANG modules within the IETF, where folks are trying to get them to be perfect rather than good enough.

This makes a lot of sense whe, modules are very stable and well-tested, but this approach makes it much harder to make fixes to YANG modules.


### The overall RFC process is slow.

It takes a long time, and a lot of review, to publish YANG modules within the IETF.


### Competition with Industry models.

### Alternative approaches

#### OpenConfig

OpenConfig is an industry led forum for developing network-device specific YANG modules.  There is quite a strong functional overlap  between OpenConfig and IETF YANG modules, but they have a taken a significantly different approach to solving operational state issues that means that the YANG modules produced by OpenConfig are broadly incompatible with the more approach taken by the IETF with NMDA {{?RFC8342}}.

OpenConfig has also taken a different approach to how their develop their YANG modules.  They manage their Device YANG as a versioned set of modules within a single Github project.  They allow some level of breaking changes to the YANG modules to allow the API to evolve and improve more quickly, making use of Semantic Versioning to document where breaking changes have occurred.  New versions of
the OpenConfig YANG github repository are pushed approximately every 3 months, where they ensure that all related YANG modules are updated as a cohesive set of modules.

#### Vendor YANG Modules

Vendors publish YANG modules with much higher frequency and less stability than IETF YANG modules, with the expectation that providing some level of programmatic YANG API is better than none at all.  Vendors generally seem to have the expectation that they can make non-backwards-compatible changes to YANG modules between releases, as the models evolve and as they fix issues. 


### All updates to the YANG modules require a new RFC to be published.

The key aspect of the description above is that the YANG module itself is embedded within the RFC, and hence publishing any updated revision of the YANG module (even for a small fix) requires a new RFC to be issued.

### YANG versioning and backwards compatibilty

YANG 1{{?RFC6020}} and 1.1{{!RFC7950}} both adopt a model where the only changes to a module that are allowed are backwards compatible changes.  All non-backwards-compatible changes are disallowed, except via a formal deprecation and obsoletion process.  Deprecated and obsoleted nodes are retained in the modules.

### Running Code

Ideally there are implementations to validate the YANG models that are being standardized.  By definition these implementations must be done against pre-standard versions of the YANG modules.  However, the various IETF review processes can mean that there are changes to the names of data nodes, and to the overal structure of the schema before the final RFC gets published.

For IETF YANG modules, they can be pre-standard for a long period of time, meaning that live deployments may be based around them.

Generally, YANG encourages only backwards-compatible changes to YANG models, but this doesn't appy to pre-release versions.  Meaning that devices and clients have to manage these breaking changes (without the normal deprecation cycle) when moving from pre-release to published standard versions.

### Handling Errata

The RFC editor provides a mechansim for reporting errata against RFCs, but this mechanism cannot be usefully used to fix mistakes in YANG modules because accepting an errata would create an ambiguity to exact textual content of the YANG module for a given YANG module revision.  Hence, valid errata are always maked as "Hold for Doc Update" waiting for a new bis version of the RFC to be published.


high-level description of what the module covers. 


Although, a copy of these modules is made available in YANG Catalog (TODO - Ref), on Github (TODO - Ref), the canonical reference for these YANG modules is the RFCs containing the YANG module.  Other organizations (includings SDOs and Industry bodies) have moved to developing and maintaining YANG modules more directly as code assets which has allowed a more expedient development cycle.

Within the IETF, development of YANG modules is generally deferred to the WGs responsible for protocols, which have the necessary technical knowledge to ensure that the models cover the necessary protocol functionality.  In cases where there is no suitable WG is available, then development of the YANG models has come to the NETMOD WG, responsible for the YANG language.  In addition, there is a team of "YANG Doctors" of YANG language experts who perform detailed reviews of YANG modules during the standardization process to ensure that YANG modules are well modelled.

There are several advantages to the IETF process used to develop YANG modules:

Protocol experts generally ensure that the YANG modules provide good configuration coverage of the protocol in 


The IETF process of developing YANG modules has several advantages:

The work to generate these YANG models is delegated 

 Although this approach has several benefits, i.e., following established practice, and wider review of the generated YANG models it also have several downsides.

Historically, IETF has published YANG models as code assets embedded within 
TODO Introduction


# Proposals

## Take YANG modules out of RFCs

The proposal is to stop publish YANG modules in RFCs.  YANG related RFCs would still contain the descriptive prose documenting the structure and meaning of the schema defined in the YANG module, but the full YANG module text and the full YANG tree diagram would no longer be published in RFCs.  Instead, YANG modules should be managed for what they are, i.e., code assets that are used to build network management APIs and associated documentation.   The RFC would instead contain stable references to (i) the YANG module revision associated with the RFC at the time of publication, and (ii) the latest bugfixed version of the YANG module associated with the RFC.  TODO, would it be helpful to also have a reference to the latest "developmental" version of the YANG module?

Hence, the proposal is that RFCs defining YANG modules would contain:
- An overview of the technology that the YANG module(s) cover.
- High-level descriptions of key parts (e.g., containers and lists) of the YANG module(s) 
- Snippets of tree output that describe the structure
- A reference to latest version of the YANG module associated with the RFC (held in IANA)
- A reference to the tree output (automatically generated) associated with the latest version of hte YANG module.
- Security considerations relevant to the use of the YANG module.
- Examples for using the YANG module.

One additional minor benefit of taking the YANG module out of the RFC could be to increase the column length limit for IETF YANG modules (perhaps to 80 or 120 characters), which may faciliate a minor improvement to YANG module readability.

# Procedures for managing YANG modules within the IETF

## Maintaining stable references (IANA)

IANA already maintains the "YANG Module Names" Registry.

The YANG Module Names registry contains:
- An entry for the latest revision of each IANA maintained YANG module (e.g., iana-if-types.yang)
- An entry for every revision of each YANG module published in an RFC. (e.g., there are 2 copies of ietf-interfaes.yang, published in {{?RFC7223}} and {{?RFC8343}})

Each entry in the YANG Module Names registry has fields that include:
- the module name (not necessarily unique)
- a link to the module revision YANG module source code
- a reference to the RFC that contains the module.

It would be helpful to have an IANA registry that contains a reference to every revision of a YANG module published by the IETF or IANA.


that maintains separate entries for each version of 

a registry of the latest version of YANG modules

## Standardizing new YANG modules within the IETF

New YANG modules would follow the same process that is followed today, with the same level of technical review and consensus check at each phase, with the only differnce being that the module and tree diagrams are referenced rather than included.

TODO, possibly for review purposes, the tooling could include a copy of the YANG module and module tree ouptut in an appendix, that it automatically removed when the document is published.  TODO, would this reintroduce the line limit issue again?

## Enhancing existing YANG modules with new functionality

## Applying small fixes to IETF YANG modules

The goal is to define a lightweight process (similar to how errata against RFCs are handled) should be able to apply small bugfix sized changes to published YANG modules.  A key observation is that processing errata does not require a WG or IETF last call, or IESG review.  The decision to approve errata is taken by the AD, judging the consensus of the WG, and in particular the authors of the RFC.

The process for making fixes to IETF YANG modules (including small non-backwards-compatible changes) should follow an equivalent level of review and consensus check as for processing errata against RFCs.

Not all WGs have to follow exactly the same process, but defining a common, best practice approach, should generally make it easier for everyone.

An alternative process.

The proposed experiment would use github to track. 

Errata are processed.

The proposal is to make use of the existing.

The existing RFC errata process can be used to track bugs against stable published YANG modules.

Small fixes to published IETF YANG modules are processed in a similar fashion to how the IETF processes errata.  I.e., the responsible Area Director has authority to approve minor fixes.


although there is also an IANA registry that eferences and.

embedded the YANG module source in RFCs, where they cannot be updated without publishing a new RFC, not even for a bugfix or an errata.  Instead, the YANG modules would only be stored in an IANA registery, with the draft only maintaining a reference to the latest published version of the YANG module associated with the RFC.



URL to an updateable reference to the latest published version of the YANG modules associated with the RFC.

If we enact this change then there are further changes that would go along side it:

### IANA YANG Module References

If a YANG module changes significantly, e.g., a large quantity of new functionality is added to the 

## Living Bis Documents

The proposal to move the YANG module 

The draft would hold 

 IANA & Github rather than in RFCs.

## M

One added benefit 



# Security Considerations

For the purposes of this document, the pertinent security considerations are really about managing the code assets and related 

Really about whether it is possible for a bad actor to modify the YANG modules that are published as having some level of IETF consensus without



# IANA Considerations

TBD.


This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

# Random stuff

TODO.

YANG Catalog is maintained by the IETF, but the YangModels/yang Github repository contains YANG Modules from other sources, and is industry maintained.
