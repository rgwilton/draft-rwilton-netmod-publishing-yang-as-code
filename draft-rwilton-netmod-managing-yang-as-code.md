---
title: "Managing IETF YANG modules as code not documents"
abbrev: "YANG as code"
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

The document highlights some of the issues with how the IETF standardizes YANG modules and proposes some alternative approaches for the YANG module standardization process within the IETF.  Some of these approaches could be developed into process experiments to gain more experience and gradually evolve the processes for managing IETF YANG modules.

--- middle

# Introduction

This document proposes that the IETF tries some process experiments for the management and evolution of YANG modules created and published by the IETF.  The goal is the make the process easier and more helpful, allowing YANG modules to be published more quickly without losing the benefits of having a stable and industry respected consensus process.

This is very much an early draft, and the author(s) are seeking input from the community as to whether any of these proposed process changes are likely to be helpful.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# The Current Process for Publishing IETF YANG Modules
IETF currently publishes YANG modules as extractable code assets within RFCs.  I.e., the YANG module source text is embedded directly in the RFC using CODE BEGINS/ENDS markers, and can be extracted via tooling, such as rfcstrip.  As such, the RFC should be regarded as the definitive source reference for any embedded YANG Modules.  However, copies of the YANG modules are also available in the IANA YANG Module Names registry, YANG Catalog, and the YangModels/yang Github repository.

The key components of RFCs containing one or more YANG modules are:

* An overview of the technology that the YANG module(s) cover,
* High-level descriptions of key parts (e.g., containers and lists) of the YANG module(s),
* YANG tree diagram {{?RFC8340}} output to illustrate the schema structure for the YANG module(s).  Note, sometimes this is included as snippets of the module tree diagram output, potentially with a full copy of the module tree output in an appendix.
* The YANG module code asset(s),
* Relevant security considerations for using the YANG module, and
* Simple examples of using the YANG module, demonstrated as instance data in XML or JSON that conforms to the YANG module schema.

Within the IETF, development of YANG modules is generally deferred to the WGs responsible for protocols, which have the necessary technical knowledge to ensure that the models cover the necessary protocol functionality.  In cases where no suitable WG is available, then development of the YANG models has traditionally come to the NETMOD WG, responsible for the YANG language.  In addition, there is a team of "YANG Doctors" of YANG language experts who perform detailed reviews of YANG modules during the standardization process to ensure that YANG modules are well modelled.

The process for updating existing published IETF YANG modules with new content is similar to the IETF process for publishing new YANG modules.  The new additions can be put into updated revision of the original YANG module or as a new augmenting YANG module that only contains the new functionality.  If updating the original YANG module then the normal IETF process would be to create a bis version of the original YANG module RFC.  If the additions are being developed as augmentions in a separate extension YANG module then there is a choice of creating a bis version of the original YANG module RFC to also include the extension YANG module(s), or creating a separate new RFC just for the extensions.

Fixing errors in the YANG module must be handled the same way as updating the original YANG module via a bis version of the original YANG module RFC.


# Benefits and Downsides of IETF Standardization Process for YANG

## Benefits

Some of the benefits of the existing IETF YANG module standardization process are:

* Domain experts help create the YANG modules
* The work is distributed across more WGs and individuals
* There is only a very gradual change to the YANG modules (due to the latency in the IETF standardization process)
* It follow the same process as for all other IETF output, i.e., the output is RFCs.

## Downsides

There are also some downsides of the existing IETF YANG module standarization process:

* The process take a very long time to standard IETF YANG modules, significantly damaging market adoption.
* IETF YANG modules for different protocols and features are being develeoped semi-independently, but there are often dependencies between YANG modules which are hard to manage within the current IETF process.
* There is little effective work to ensure that IETF YANG modules work together as a coherent network management configuration API with all of the extra (not protocol configuration) also modelled.
* The RFC errata mechanism doesn't really work effectively for YANG modules because accepting an errata would create an ambiguity to exact textual content of the YANG module for a given YANG module revision.  Hence, valid errata in IETF YANG modules are always maked as "Hold for Doc Update" waiting for a new bis version of the RFC to be published with an updated YANG module revision.
* Including the code in the RFCs imposes a lower line length limit that would normally be used on code assets, potentially reducing their readability.  E.g., if the YANG modules were not being put in RFCs, then I doubt that anyone would format them to anything less than 80 characters.

## Alternative industry approaches

### OpenConfig

OpenConfig is an industry led forum for developing network-device specific YANG modules.  There is quite a strong functional overlap  between OpenConfig and IETF device YANG modules, but they have a taken a significantly different approach to solving operational state issues meaning that the YANG modules produced by OpenConfig are broadly incompatible with the approach taken by the IETF with NMDA {{?RFC8342}}.

OpenConfig has also taken a different approach to how they develop their YANG modules.  They manage their Device YANG as a versioned set of modules within a single Github project.  They allow some level of breaking changes to the YANG modules to allow the API to evolve and improve more quickly, making use of Semantic Versioning to document where breaking changes have occurred.  New versions of the OpenConfig YANG github repository are pushed approximately every 3 months, where they ensure that all related YANG modules are updated as a cohesive set of modules that work together.  Specifically, implementations are expected to use a coherent set of OpenConfig YANG modules that are known to be compatible with each other.


# Alternative Suggestions for how IETF could manage YANG

This section contains proposals on changing the IETF process for managing YANG modules that may be more effect than the current process.

## Take YANG modules out of RFCs

The core proposal is to stop publish YANG modules verbatim in RFCs.  YANG related RFCs would still contain the descriptive prose documenting the structure and meaning of the schema defined in the YANG modules, but the full YANG module texts and the full YANG tree diagrams would no longer be published in RFCs.  Instead, YANG modules should be managed for what they are, i.e., code assets that are used to build network management APIs and associated documentation.  Hence, the RFC would only contain stable references to the code assets and generated tree diagrams rather than having them embedded directly in the document, where they cannot change.

Hence, the proposal is that RFCs defining YANG modules would contain:

* An overview of the technology that the YANG module(s) cover,
* High-level descriptions of key parts (e.g., containers and lists) of the YANG module(s),
* Snippets of tree output that describe the structure,
* A stable reference  to the YANG module revision in IANA associated with the RFC at the time of publication,
* A stable reference to the latest bugfixed version of the YANG module in IANA associated with the RFC - logically the YANG module with errata applied,
* A reference to the tree output (automatically generated) associated with the latest version of hte YANG module,
* Security considerations relevant to the use of the YANG module,
* Examples for using the YANG module.

One additional minor benefit of taking the YANG module out of the RFC could be to increase the column length limit for IETF YANG modules (perhaps to something between 80 and 120 characters), which may faciliate a minor improvement to YANG module readability.

The obvious downside of managing the YANG modules outside the RFC is that depending on how the modules are updated, then the descriptive text in the RFC must be kept up to date with changes in the YANG module.  Possibly this could be handled by keeping a living bis version of the YANG module going in the WG until the YANG module(s) reach a high level of stability.

### Alternatives

One alternative would be to keep the original YANG modules published as part of the RFC in the appendix, but retain the stable references for where to find fixed revisions of the YANG modules.  However, this potentially creates some ambiguity as to where is the best reference to fetch the YANG module.

## Maintaining stable references (IANA)

IANA already maintains the "YANG Module Names" Registry.

The IANA YANG Module Names registry contains:

* An entry for the latest revision of each IANA maintained YANG module (e.g., iana-if-types.yang)
* An entry for every revision of each YANG module published in an RFC. (e.g., there are 2 copies of ietf-interfaes.yang, published in {{?RFC7223}} and {{?RFC8343}})

Each entry in the IANA YANG Module Names registry has fields that include:

* the module name (not necessarily unique),
* a link to a specific YANG module revision source file,
* a reference to the RFC that specifies the given module revision.

The proposal is to evolve the IANA registries for YANG modules to acheive the following goals:

* Allow IANA to become the permanent canonical reference for YANG modules associated with RFCs, both the initial revision published at the same time as the RFC, and any version updated to include bugfixes or errata.
* Allow IANA to track all YANG module revisions associated with a given RFC, i.e., if bugfixes have been applied to any YANG modules defined in the RFC.
* Allow IANA to provide a per RFC, per YANG module, stable reference to the latest bugfixed version of the YANG module.  I.e., so that the RFC can always point to the latest fixed stable version of the YANG module.
* TODO - IANA should also maintain tree diagram information, but need to consider which imported module versions are used to construct the tree output.

## Ensure that models don't change at late phases of the IETF review cycle

Ideally there are implementations to validate the YANG models that are being standardized.  By definition these implementations must be done against pre-standard versions of the YANG modules.  However, the various IETF review processes can mean that there are changes to the names of data nodes, and to the overal structure of the schema before the final RFC gets published.

For IETF YANG modules, they can be pre-standard for a long period of time, meaning that live deployments may be based around them.

Generally, YANG encourages only backwards-compatible changes to YANG models, but this doesn't appy to pre-release versions.  Meaning that devices and clients have to manage these breaking changes (without the normal deprecation cycle) when moving from pre-release to published standard versions.

Hence, we should consider if there is a way that we can manage the IETF consensus process such that YANG modules that have reached WG consensus can be regarded as having stable names and structure.

## Make use of YANG versioning and allow breaking changes

YANG 1{{?RFC6020}} and 1.1{{!RFC7950}} both adopt a model where the only changes to a module that are allowed are backwards compatible changes.  All non-backwards-compatible changes are disallowed, except via a formal deprecation and obsoletion process.  Deprecated and obsoleted nodes are retained in the modules.   This is a good approach when modules are very stable, but has acted to slow down development of YANG modules within the IETF, where folks are trying to get them to be perfect rather than good enough.

This makes a lot of sense whe, modules are very stable and well-tested, but this approach makes it much harder to make fixes to YANG modules.

TODO - We should make use of YANG Semantic version numbers for IETF YANG modules, and allow some level of breaking changes, particularly for bugfixes or flaws in the original YANG modules.

## Make use of YANG packages to build

TODO - We should make use of YANG packages to combine sets of YANG modules together into usable higher layer functionality, and ensure that those modules interoperate and work together.

## Manage development versions of IETF YANG modules on github.

TODO - We should investigate whether we can maintain a set of 'latest development' versions of YANG modules, that can then periodically be released to be more stable, before eventually being written into RFCs.

## Living YANG documents and Living YANG bis documents.

TODO - If we allow for 'latest development' versions of YANG modules, then we may also need associated living documents that contain the equivalent documentation associated with the YANG modules.

# New Procedures for managing YANG modules within the IETF

TODO - Further updates required.

## Standardizing new YANG modules within the IETF

New YANG modules would follow the same process that is followed today, with the same level of technical review and consensus check at each phase, with the only differnce being that the module and tree diagrams are referenced rather than included.

TODO, possibly for review purposes, the tooling could include a copy of the YANG module and module tree ouptut in an appendix, that it automatically removed when the document is published.  TODO, would this reintroduce the line limit issue again?

## Enhancing existing YANG modules with new functionality

TODO

## Applying small fixes to IETF YANG modules

The goal is to define a lightweight process (similar to how errata against RFCs are handled) should be able to apply small bugfix sized changes to published YANG modules.  A key observation is that processing errata does not require a WG or IETF last call, or IESG review.  The decision to approve errata is taken by the AD, judging the consensus of the WG, and in particular the authors of the RFC.

The process for making fixes to IETF YANG modules (including small non-backwards-compatible changes) should follow an equivalent level of review and consensus check as for processing errata against RFCs.

Not all WGs have to follow exactly the same process, but defining a common, best practice approach, should generally make it easier for everyone.

TODO

# Security Considerations

For the purposes of this document, the pertinent security considerations are really about ensuring the canonical code references for YANG modules are stable and safe from being manipulated by bad actors.  When the canonical version of the YANG module source text was in RFCs then any copies could always be checked against the RFC, that never changes.

Does IANA provide the same level of security guarantee as an RFC does?


# IANA Considerations

TBD, probably quite a few, depending on what we do.  Once we have firmed up a bit within the WG, then we should consult with IANA on an early review to see if they are comfortable with the proposed experiments.


--- back

# Acknowledgments
{:numbered="false"}
