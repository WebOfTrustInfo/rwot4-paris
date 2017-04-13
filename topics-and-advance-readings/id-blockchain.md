


## ID-Blockchain : an initiative towards privacy preserving blockchain based identity

Olivier Maas, Florent Poiron, _R&amp;D, Worldline_

_Abstract__— Id-Blockchain is a joint initiative to investigate the possibilities offered by Blockchain technologies in the field of digital identity management with a particular focus on personal data protection. The goal of ID-Blockchain is to prototype a service combining strong authentication and verifiable claims management; this service will be secured using hardware devices and provide a high level of data protection. The project will design use cases, functional and technical architecture, a protocol implemented with software and hardware assets and validation through prototyping. In this paper, we present our project&#39;s vision and goals._ **Our goal for the rebooting web of trust meeting is to confront our vision and first results to the community** _._

_Index Terms : identity management system, authentication, privacy_

#### I.INTRODUCTION

Solving the issue of digital identity is a long term quest. The development of online services has resulted in subjects and service providers managing numerous credentials. Identity providers help to minimize this burden but today only social logins has reached a significant scale. Blockchain technology seems to enable a new approach to this problem. It promises to increase the level of security and privacy, the level of user control and transparency in use while decreasing costs and the level of potential malfunction. Id-Blockchain aims at exploring these challenges.

The goal of our project is to explore where and how Blockchain can provide answers to the requirements of digital identity management in a real world context. Our work encompasses several parts of the value chain of digital identity:

- Management of subject&#39;s claims across Service providers and Identity providers
- Usage of blockchain as the pivotal component of trust in the identity system
- Usage of a peer to peer approach to grow trust through social graphs and reputation
- Security of the identity system with a strong focus on the security of the subject&#39;s identity

The paper is organized as follows. Section II surveys the related work. Section III presents requirements applicable to an identity system. Section IV and V respectively details a basic use case and the architecture overview of our system. Section IV details experimental results. Finally Section VI presents the actor of our project.

#### II.Related work
A.Data protection

The EU Global Data Protection Regulation (GDPR) [2] will be introduced in 2018 in Europe and introduces significant changes in personal data protection:

- Clear justification of personal data usage and unambiguous consent
- Pseudonymisation of subject
- Data protection by design and by default (data minimalization)
- Enhanced rights : right to be forgotten, data portability rights, right to object to automated decision making


B.User centric standards on identity and authentication

- FIDO defines user centric and privacy enhanced APIs [3] enabling service providers to build secure authentication. These specifications have been submitted to the W3C for standardization. The protocol is set to become the standard web authentication protocol.
- The Bitcoin protocol [4] is the longest lasting implementation of Blockchain technology. Although primarily focused on cryptocurrency, the Bitcoin protocol can be enhanced to manage assets by storing metadata in its Op Return field.
- BitId [5] is a draft bitcoin authentication protocol which takes advantage of bitcoin&#39;s public key cryptography features to allow user authentication on websites. It does not support claims management.
- W3C has launched a working group on verifiable claims [6] to investigate user centric standard for expressing and transacting verifiable claims (eg credentials and attestations) via the Web. This work focuses on syntax and metamodel but neither on attribute exchange protocols nor browser APIs.

 C.Self sovereign identity

The concept of self sovereign identity has emerged in the continuity of the concept of user centric identity. According to C. Allen [7], the principles that govern this concept are: existence, control, access, transparency, persistence, portability, interoperability, consent, minimalization, protection.

 D.Reputation

In our work, we propose to use reputation as a way to take advantage of the subject social graph and propagate Identity Providers trust. For example, a subject can leverage existing relationships with his peers and ask them for attestations of verifiable claims. The protocol should be robust to classical attacks on reputation systems, in particular bad-mouthing, ballot-stuffing, Sybil attacks and whitewashing

E.Blockchain

Considering the requirements on transparency, persistence and portability lead us to believe that only public blockchains can offer the adequate properties to implement a global and open identity blockchain based ecosystem. Bitcoin stands out because it is open source and independent from any foundation. Still, using a public and permissionless blockchain raises issues such as how to link virtual identities of identity providers to their real life identity.

#### III.Privacy requirements on identity system

Brandão et al [1] have identified the main problems of hub based large scale identity system. We capitalize on their work to define the privacy requirements of a Blockchain identity system.

The protocol should be resilient against:

- Honest but curious actors who act honestly during transactions but curious because they derive information for the observed communications
- Malicious collusion of actors (SPs or IDPs)

The desired properties of the protocol:

- No public storage of personal information
- Selective disclosure of claims to cope with data minimalization principle
- Unlinkability of subject against colluding SPs associated with pseudonyms
- SP identity hidden from IDP
- IDP identity may be hidden from SP, depending on the use case
- Resilience against impersonation

#### IV.Basic Use cases

The basic use cases covered by the ID-Blockchain project ​​are:

- Installation and registration by the subject of an ID-Blockchain compatible mobile application
- Pairing of an hardware device for enhanced credential security
- Self-registration of new pseudo identity
- Interaction between the subject and the identity providers to link pseudo identity to verifiable claims: the identity provider validates the subject&#39;s claims, the subject links claims to pseudo identities.
- Interaction between the subject and his peers: the peers validates the subject&#39;s claims, the subject links claims to pseudo identities.
- Interaction between the subject and the service providers : the subject provides claims or proof of claims
- Verification by the service providers of claims
- Strong authentication of the subject when accessing a service in Challenge / Response mode with public identifier / key
- Management by the subject of his pseudo identities and personal claims

Non nominal use cases will also be studied such as renewal, revocation, of credentials.

#### V.Deliverables and prototype

Our deliverables will consist of:

- An API definition to manage interactions between third parties involved
- A Blockchain storage protocol definition
- Assets:
  - Subject software wallet
  - Subject hardware token

The prototype will offer to subjects digital identity management and strong authentication services, with physical and logical access control devices

The ID-BLOCKCHAIN ​​prototype will include:

1. A hardware device owned and controlled by the subjects ensuring:

	a.  communication via BLE (Bluetooth Low Energy) with its environment (PC, smartphone, personal connected object, car computer, home automation center, ..)

	b. logical and physical protection of confidential information (encryption keys, identity and personal attribute, etc.)

2. A mobile application enabling:

	a. the management by the subject of its claims and relationship with providers and peers,

	b. the implementation of interfaces with the hardware device, the blockchain, providers and peers

3. Verifiable claims management services:

	a. Online enrollment of the subject based either on legacy trusted third party relationship or on the concept of personal relationship, filiation and e-reputation,

	b. Service Providers and identity providers APIs to interact with subjects and the blockchain.

#### VI.About the Id-Blockchain project
   A.Context of the project

Id-Blockchain is a project supported in part by the French government, under the &#39;programme d&#39;investissement d&#39;avenir&#39; framework launched in 2016.

[http://www.gouvernement.fr/investissements-d-avenir-cgi](http://www.gouvernement.fr/investissements-d-avenir-cgi).

 B.Partners

The ID-BLOCKCHAIN project partners are:

- Worldline, [https://worldline.com](https://worldline.com), is an actor in the payments and transaction services industry. Worldline leads the project,

- Ledger brings its range of secured hardware products of protection of cryptographic keys and its expertise FIDO U2F,

- Paymium, [https://www.paymium.com/](https://www.paymium.com/), brings its experience of public blockchain technologies,

- Greyc, [https://www.greyc.fr](https://www.greyc.fr), Group of Research in Computer Science, Image, Automatic and Instrumentation of Caen; is an academic laboratory in the field of computer science and cryptography

- Liris, [https://liris.cnrs.fr/](https://liris.cnrs.fr/), Laboratory of InfoRmatics in Images and Information Systems - National Institute of Applied Sciences (INSA) Lyon), is an academic laboratory and brings in expertise in the field of e-reputation, particularly in collaborative systems.

References

[1]                Brandão, L., Christin, N., Danezis, G., et al. (2015). Toward Mending Two Nation-Scale Brokered Identification Systems. _Proceedings on Privacy Enhancing Technologies_, 2015(2), pp. 135-155.

[2]                        Council of the European Union, Interinstitutional file: 2012/0011 (COD) 5419/1/16 REV1, 2016.

[3]                        FIDO Alliance, FIDO Privacy FIDO Alliance White Paper, 2016.

[4]                        Nakamoto, S., Bitcoin: A Peer-to-Peer Electronic Cash System, 2008.

[5]                        Larchevêque, E.,  [https://github.com/bitid/bitid/blob/master/BIP\_draft.md](https://github.com/bitid/bitid/blob/master/BIP_draft.md), 2016.

[6]                 W3C,   [https://www.w3.org/2017/vc/charter](https://www.w3.org/2017/vc/charter), 2016.

[7]                        Allen, C., The Path to Self-Sovereign Identity, 2016.

This paper is submitted for review to the Rebooting Web of Trust Workshop organized in Paris in April 2017. This work is supported in part by the French government  under the &#39;Programme d&#39;investissement d&#39;Avenir&#39; - Grant N° P141199-2863529-DOS0043349/00.
