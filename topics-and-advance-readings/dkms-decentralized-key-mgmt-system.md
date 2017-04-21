# Decentralized Key Management System

*Drummond Reed, Chief Trust Officer, Evernym; Trustee, Sovrin Foundation; 2017-04-18; Rebooting the Web of Trust #4, Paris, France*

# Overview

DKMS (Decentralized Key Management System) is a new approach to cryptographic key management intended for use with blockchain and distributed ledger technologies (DLTs) where there are no centralized authorities. DKMS inverts a core assumption of conventional PKI (public key infrastructure) architecture, namely that public key certificates will be issued by a relatively small number of centralized or federated certificate authorities (CAs). With DKMS, the initial “root of trust” for all participants is a distributed ledger that supports a new form of root identity record called a DID (decentralized identifier).

A DID is a globally unique identifier generated cryptographically so it requires no central registration authority. Each DID points a DDO (DID descriptor object), a JSON-LD object containing the associated public verification key(s) and a pointer to off-ledger agent(s) supporting peer-to-peer interactions with the identity owner. From this baseline, trust between peers can be built up in two ways:

1. Challenge/response messages for real-time verification of public keys.
1. Exchange of identity attribute claims signed by other trusted peers (“verifiable claims”) whose public keys can also be verified against the ledger. 

This decentralized “web of trust” model leverages the security, privacy, and resiliency properties of distributed ledgers to provide highly scalable key distribution, verification, and recovery, finally making PKI accessible to everyone.

# Customer Need

X.509 public key certificates, as used in the TLS/SSL protocol for HTTPS secure Web browsing, have become the most widely adopted PKI in the world. Yet the difficulty of generating public/private key pairs and obtaining and managing X.509 certificates means that only the smallest fraction of Internet users are currently in position to use public/private key cryptography for their own identity, security, privacy, and trust management.

This inability for people and organizations to interact privately as independent, verifiable peers on their own terms has many consequences. First, it forces individuals and smaller organizations to rely on large federated identity providers and certificate authorities who are in a position to dictate security, privacy and business policies. Secondly, it limits a peer’s degrees of freedom to interact outside of the federations and policies supported by these providers. Third, it restricts the number of ways in which peers can discover each other and build new trust relationships—which in turn limits the health and resiliency of the digital economy.

To overcome these barriers, individuals and organizations need new infrastructure that provides a simple, secure, painless way to generate strong public/private key pairs, register them for easy discovery and verification, and rotate and retire them as needed to maintain strong security and privacy. They also need the ability to build trust in the associated digital identities through the exchange of verifiable claims. And finally they need key recovery that is as easy as the “forgot password?” link on most web login pages yet an order of magnitude more secure.

# Approach

The foundation for DKMS is laid by the [DID specification](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/did-implementer-draft-10.pdf). As globally unique identifiers, DIDs are patterned after URNs (Uniform Resource Names): colon-delimited strings consisting of a scheme name followed by a DID method name followed by a method-specific identifier. Here is an example DID that uses the Sovrin DID method:

```did:sov:21tDAKCERh95uGgKbJNHYp```

Each DID method specification defines:

1. The specific ledger against which the DID method operates;
1. The format of the method-specific identifier;
1. The CRUD operations (create, read, update, delete) for DIDs and DDOs on that ledger. 

DID resolver code can then be written to perform these CRUD operations on that ledger with respect to any DID conforming to that specification.

The DID specification covers the bottom layer of a decentralized public key infrastructure. The DKMS spec will cover the two layers above it: the **edge layer**, where most private keys are generated and stored, and the **agent layer**, where encrypted peer-to-peer communications takes place to exchange and verify DIDs, public keys, and verifiable claims.

![DKMS Layer Diagram](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/dkms-layers-diagram.png)

At the edge layer, devices (mobile phones, laptops, desktops, firewalled servers) run one or more apps that maintain DMKS-compliant wallet(s) for storage of private keys and master secrets. These apps are where the primary user interface challenges of DKMS will be met—especially key recovery, since a decentralized identity owner is the sole authority for his/her own private keys.
Apps communicate with each other—and often with the ledger layer—via the agent layer. Agents offer a host of services that enable core DKMS functions: DID resolution, encrypted wallet backup and synchronization, push notifications, real-time public key verification, off-ledger exchange and verification of verifiable claims, and bootstrapping of encrypted private P2P communications channels.

# Benefits

1. **No single point of failure.** With DKMS, there is no central CA or other registration authority whose failure can jeopardize large swaths of users.
1. **Interoperability.** DKMS will enable any two apps and identity owners to perform key exchange and create encrypted P2P connections without reliance on proprietary software or service providers.
1. **Resilience.** DKMS incorporates all the advantages of distributed ledger technology for decentralized access to cryptographically verifiable data, and then builds on top of it a distributed web of trust where any peer can exchange keys, form connections, and issue/accept verifiable claims from any other peer.
1. **Key recovery.** Rather than app-specific or domain-specific key recovery solutions, DKMS can build key robust key recovery directly into the infrastructure, including agent-automated encrypted backup, DKMS key escrow services, and social recovery of keys sharded across trusted DKMS connections.

# Next Steps

Work by Evernym on the DKMS specification is funded by the U.S. Department of Homeland Security Science & Technology Directorate (DHS S&T). Any opinions contained herein are those of Evernym and do not necessarily reflect those of DHS S&T. The specification will be based on [NIST Special Publication 800-130: A Framework for Cryptographic Key Management Systems](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-130.pdf). Interested contributors are invited to contact the authors via the [Sovrin Forum](http://forum.sovrin.org/).
