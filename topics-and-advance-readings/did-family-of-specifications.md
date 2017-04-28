# The DID Family of Specifications

*Drummond Reed, Chief Trust Officer, Evernym & Trustee, Sovrin Foundation
2017-04-18, Rebooting the Web of Trust #4, Paris, France*

**Acknowledgement:** Work on the DID family of specifications has been funded in part by the United States Department of Homeland Security's Science and Technology Directorate under contract HSHQDC-16-R00012-H-SB2016-1-002. The content of these specifications does not necessarily reflect the position or the policy of the U.S. Government and no official endorsement should be inferred. 

# Introduction

DIDs (decentralized identifiers) were originally identified as a critical component of decentralized identity infrastructure by Manu Sporny, David Longley, and the contributors to the W3C Web Payments Working Group and the Verifiable Claims Task Force. The first version of the DID Data Model and Generic Syntax 1.0 specification, funded in part by an SBIR grant from the U.S. DHS grant to Respect Network Corporation and incorporating input and feedback from the second and third Rebooting the Web of Trust conferences, was published on 21 November 2016. This document describes a growing family of specifications that build on DIDs to provide other vital components of an interoperable decentralized identity infrastructure.

# DID Data Model and Generic Syntax 1.0

This is the baseline specification in the DID family—the specification on which all the others build. Implementer’s Draft 01 was published on 21 November 2016 and is available in both a [PDF version](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/did-implementer-draft-10.pdf) (static) and a [Google doc version](https://docs.google.com/document/d/1Z-9jX4PEWtyRFD5fEyyzEnWK_0ir0no1JJLuRu8O9Gs/edit?usp=sharing) (active document accepting comments). Following is the abstract:

**DIDs** (decentralized identifiers) are a new type of identifier intended for verifiable digital identity that is "self-sovereign", i.e., fully under the control of the identity owner and not dependent on a centralized registry, identity provider, or certificate authority. DIDs resolve to **DDOs** (DID descriptor objects)—simple JSON documents that contain all the metadata needed to prove ownership and control of a DID. Specifically, a DDO contains a set of **key descriptions**, which are machine-readable descriptions of the identity owner’s public keys, and a set of **service endpoints**, which are resource pointers necessary to initiate trusted interactions with the identity owner. Each DID uses a specific **DID method**, defined in a separate **DID method specification**, to define how the DID is registered, resolved, updated, and revoked on a specific distributed ledger or network. 

# DKMS (Decentralized Key Management System)

The DID specification solves one critical piece of decentralized public key infrastructure (DPKI): how to quickly and easily establish a globally unique identifier and the public key(s) and service endpoint(s) bound to it in such a way that they can be verified in real time. But this first step is only the "tip of the iceberg" of decentralized identity infrastructure. The much larger "below the waterline" challenge is management of the private keys and master secrets associated with a DID. How to do this in a way that is interoperable across different ledgers, agents, apps, and vendors is the focus of the DKMS (Decentralized Key Management System) specification.

The [DKMS specification](/topics-and-advance-readings/dkms-decentralized-key-mgmt-system.md) will be based on the requirements and best practices set forth in [NIST Special Publication 800-130](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-130.pdf), "A Framework for Designing Key Management System", a 120 page specification with the following abstract:

>This Framework for Designing Cryptographic Key Management Systems (CKMS) contains topics that should be considered by a CKMS designer when developing a CKMS design specification. For each topic, there are one or more documentation requirements that need to be addressed by the design specification. Thus, any CKMS that addresses each of these requirements would have a design specification that is compliant with this Framework. 

The goal of the DKMS spec is to enable key generation, distribution, rotation, recovery, retirement, and other key management functions to be performed seamlessly and interoperably across a wide range of devices and applications—a lofty goal, but one that must be pursued if adoption of decentralized identity is to break out into the mainstream.

# DID TLS

Today's TLS infrastructure uses X.509 certs based on traditional hierarchical PKI, where certificate authorities (CAs) follow standardized best practices in order to qualify as trust roots that will be recognized by browser vendors. DID TLS decentralizes this process by enabling the X.509 cert elements required to establish a TLS session to be generated dynamically from any DID and DDO that conforms to the spec.

The DID TLS specification will enable direct encrypted P2P connections to be negotiated in real time between any two DID-identified entities (people, organizations, things). This will radically expand the protections of TLS connections and could potentially turn them into the default for all nearly all forms of Internet communication.

# DID Service Discovery

The DID specification defines how DDOs may contain service endpoints: a list of URLs for interacting with the entity identified by the DID. This means one option for service discovery is to simply use a set of standardized service type identifiers to publish the set of services supported by a particular entity directly in its DDO.

However this approach has several drawbacks. First, it requires relatively static service descriptions. Secondly, since DDOs are public, it reveals all the services supported by a particular entity. Thirdly, if the set of services supported by a particular entity are relatively unique, it increases the risk of correlation across multiple pseudonymous DIDs for that entity.

A better approach is to create a standard DID service discovery protocol that can be supported by a single service endpoint type in any DDO. This discovery service could support both public (non-permissioned) and private (permissioned) access to descriptions of the APIs supported by the underlying entity. API descriptions would be published in a standard human- and machine-readable format such as Swagger for automated discovery and dynamic negotiation of new connections.

# DID Auth

A common feature across all blockchain identity initiatives is using ledger-based identity to provide cryptographic authentication of the identity owner. The various protocols all use some form of cryptographic challenge/response similar to the [SQRL protocol](https://en.wikipedia.org/wiki/SQRL) originally proposed by Steve Gibson, i.e., a one-time challenge is issued by the relying party, signed by the identity owner's private key, and then verified by the relying party using the identity owner’s public key. Whereas SQRL uses pairwise public keys that cannot be externally verified, ledger-based identity enables verification of the public key against the ledger.

The purpose of the [DID Auth spec](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/did-auth.md) is to standardize this cryptographic challenge/response authentication protocol so it can be used with any DID that supports it. DID Auth endpoints would then become one of the standard DID identity services than can be discovered using DID service discovery.

# DID Names

The DID specification is deliberately limited to machine-generated decentralized identifiers that have no human memorability or usability. However there are use cases where it is desirable to be able to use a human-friendly semantic name to discover a DID. Although there are other ways to solve this problem, one widely used solution is a naming service similar to DNS. 

The big difference, of course, is that a DID naming service would be fully decentralized, i.e., it would not have any centralized registries and registrars. Registrations would be made by identity owners directly with the ledger itself using the same cryptographic verification as DID transactions.

The goal of the [DID Names specification](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/did-names.md) is to standardize such an interoperable decentralized naming service layer that operates on top of the DID layer. A DID name would be mapped to a DID the same way a DID is mapped to a DDO. DID names would be an optional feature of a DID method, so the governance and economics of a DID namespace must be specified by the community that defines the associated DID method.

