# Project Vouch - A decentralized identity network based on public attestation, reputation, and approval of identity attributes

_Angus Champion de Crespigny_

This discussion paper outlines Project Vouch, the project name for a public network being built for establishing and verifying self sovereign identities based on attestations and reputation, independent of any central parties.
This paper covers the basic technical concepts on which the network is being built, how it addresses digital self sovereign identity principles, applications, and the points for discussion at the Rebooting Web of Trust April 2017 workshop.

## Overview
Project Vouch is the project name for an open access, reputation and peer attestation-based, self sovereign, secure identity network. In this network, a user’s identity profile resides in a data structure stored in a secure location under the control of the user but off the network itself. This identity profile contains attributes, each of which have been attested for by other users on the network, which uses a blockchain to verify that attestations and reputation scores are aggregated across the network correctly. An attestation from a user with a high reputation will be considered to have greater weight than an attestation from a user with a low reputation.
Users are rewarded for making claims via attestations against other user’s credentials, but only if they are determined to be accurate. Users are punished for making inaccurate claims. Entities can then reveal selective identity attributes, or the results of attribute conditions, to other parties on the network.
The solution is being implemented using five main components:
  1.	**A blockchain.** This records commitments that attestations and the reputations of the peers on the network have been recorded correctly without being manipulated.
  2.	**Private, secure, off-chain channels.** These are established between users when one is attesting to the identity attribute of the other. This ensures that encrypted identity credentials are kept private between the attestor and the attestee.
  3.	**A private, secure, data store.** This ensures that identity information is kept private to only the individual. The implementation of this may be left to be user defined, however it is likely that initial implementations will be provided by services or mobile apps. Future implementations may involve specific hardware.
  4.	**Cryptographic commitments.** These record attestations made via the private channel on the blockchain and allow network participants to verify the correct aggregation of attestations and user reputations, while keeping the contents of the attestation private by only storing a hash on the blockchain.
  5.	**Reward mechanism.** This ensures that attestations are performed accurately and Sybil attacks are avoided.

## Characteristics
The network addresses eight of the ten principles of self sovereign identity as laid out by [Christopher Allen](http://www.lifewithalacrity.com/2016/04/the-path-to-self-soverereign-identity.html). The principle of Existence is understood in this context to be dependent on the final implementation and integration of the network into user facing applications, and consequently cannot be addressed at the network layer. There are no known violations of the principle of Protection in the current system design, however as it has not been explicitly addressed in the design I have not highlighted it below. 
  1.	**Control.** _Users must control their identities._ This is done by users maintaining their identity profile in a private data store. User interfaces to the network will allow users to define the identity attributes they wish to have validated.
  2.	**Access.** _Users must have access to their own data._ This is achieved through the private data store. Users may also record their attestation history if they wish from the private communication channels. 
  3.	**Transparency.** _Systems and algorithms must be transparent._ The algorithms will be free, open-source, well-known, and their correct operation will be verified through consensus on the blockchain. The integrity of the data store will also be confirmed through commitments recorded on the blockchain.
  4.	**Persistence.** _Identities must be long-lived._ The identity profile can exist as long as the user wishes to maintain their data store.
  5.	**Portability.** _Information and services about identity must be transportable._ As the data store is implementation-independent, it can be as portable or as static as the user wishes.
  6.	**Interoperability.** _Identities should be as widely usable as possible._ With the end goal being a public network, it will be accessible by all. Alignment with global identity standards is one of the points of discussion at the workshop.
  7.	**Consent.** _Users must agree to the use of their identity._ While access to the identity profile can be automatic, it will require a transaction to be executed or smart contract to be established by the individual or entity who owns the profile.
  8.	**Minimalization.** _Disclosure of claims must be minimized._ As identity attributes are revealed by transactions or via smart contracts, only the attributes or conditions that the user wishes to reveal are revealed.

## Applications
  1.	**Government.** Countries looking to implement national identity systems can incur an enormous expense in doing so, particularly in large developing nations with little established infrastructure on which individuals’ credentials can be based. Additionally, storing such data centrally can pose a significant national security risk. Enabling citizens to verify other citizen’s identities and be in charge of the security of their own data can decentralize the cost and security concerns.
  2.	**Customer onboarding for financial services.** Financial regulations require financial institutions to validate the identity of all customers, which requires significant paperwork and typically in person meetings to verify physical identity documents. While these identity documents could be digitized to streamline the customer onboarding process, their validity would be difficult to verify without an authoritative source verifying the accuracy and uniqueness of the digital copy. The establishment of a network that can demonstrate a high level of confidence in the validity of key identity attributes in a purely digital form could remove significant friction from customer onboarding without increasing the risk.
  3.	**Money for data.** By allowing users to define smart contracts to access their data, customers can sell their verified personal data and identity attributes to other parties in an automated manner for some sort of return. 

## Points for discussion at RWoT
  1.	What other decentralized identity initiatives are ongoing which could be symbiotic with Project Vouch? How can they best coordinate?
  2.	Other than verified credentials standards, are there any others which should be incorporated into the design?
  3.	What is the best method for scaling the network from private/government-initiated to fully public and open?
