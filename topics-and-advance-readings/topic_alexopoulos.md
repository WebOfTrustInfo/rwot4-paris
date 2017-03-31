# Trust for Security and Security for Trust
### A topic paper proposed by Nikolaos Alexopoulos, Technische Universität Darmstadt and SFB CROSSING

## Security needs trust

Many cryptographic and security-critical systems implicitly or explicitly depend on a notion of
trust towards entities and devices. Some of the applications of these systems are:

* Authentication
* Access Control
* Secure Service Provision (aka reputation systems for marketplaces etc.)
* Secure Routing
* Collaborative Intrusion Detection, etc.

Probabilistic trust values (belief theory - subjective logic) can be calculated and propagated through the network.

Blockchain technology (or Open Distributed Ledgers in general - ODLs as we like
to call them)
cannot alleviate the need for trust in entities altogether, but can help secure these
trust infrastructures.

## Trust needs security (and Privacy)

Trust infrastructures need to be secure against threats and single points of
failure. Transparency and global synchronization can offer a lot to
a variety of problems. First, e.g. concerning a PKI, registering an identity
as a global identifier is not enough. As suggested in the DPKI paper of the
first design workshop, ODLs can offer increased security in this domain.
However, a web of trust is still needed to authenticate the identity and
the attributes associated with an entity, e.g. for use in a distributed
attribute-based access control schema. Smart contracts could also be used
to encode access-control rules.

Privacy is also a major challenge and solutions need to be identified.
Privacy-preserving cryptocurrencies like Zerocash (also related Zerocoin and Pinocchio Coin) and Monero can offer
insights to the techniques that can contribute to this goal (ZK proofs, ring signatures etc.).

Challenges like the choice of blockchain, thin clients etc. are also prevalent
as in most similar designs. Formalization is also something generally
missing.

## Towards a multipurpose trust infrastructure for security 

* Provide the ability to store directed probabilistic trust assessments
in ODLs, forming webs of trust
* Investigate and analyze security implications of using ODLs
* Calibrate overhead with security guarantees
* What kind of ODL? Bitcoin-based, ethereum, new altcoin?
* Privacy? Selective disclosure of attributes and credentials?
