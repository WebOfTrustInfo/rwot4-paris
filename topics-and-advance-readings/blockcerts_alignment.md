# Blockcerts and Open Badges as Verifiable Claims

Note on terminology:
This uses the term "document" to refer to a credential being issued to a recipient. This is to avoid confusion with terms that already have precise meanings in the Verifiable Claims data model](https://opencreds.github.io/vc-data-model/). Note that the existing Open Badges/Blockcerts formats roughly correspond to a set of Claims and Identity Profiles in the VC definitions.

## Context

Blockcerts is an open standard and set of open source libraries enabling blockchain issuing and verification of documents. Blockcerts is Open Badge compliant, with extensions for Blockchain verification. With the OBI team, these extensions will be contributed as official OBI extensions, to enable blockchain verification for the broader open badge community.

The Blockcerts and Open Badge communities are interested in participating in the Verifiable Claims ecosystem and community, and aligning standards accordingly.

## Rebooting Web of Trust Spring 2017 topics

The following are smaller in scope and could feasibly be addressed at RWOT. Optionally, these can be rolled into existing topics.
- Alignment of signatures and verification techniques
- Proof of publication-style Merkle proofs

The following topics are very likely too large in scope (mostly because the problem statement is not yet broken down) to take as topics for RWOT, but would be interesting topics of conversation.
- Decentralized identity
- Longevity 
- Broader alignment of Open Badges into claims

## Blockcerts Issuing

- Input is a batch of json-formatted documents (currently content of each is an OBI-compliant badge)
- For each document:
   - perform JSON-LD normalization
   - take SHA256 hash of normalized result
   - add hash to Merkle tree
- Issue Merkle root on blockchain. The transaction is signed with issuer's cryptographic key (e.g. bitcoin blockchain uses a bitcoin public address)
- Additionally, for each document, sign the JSON-LD normalized payload consistent with JSON-LD signatures 

The resulting Blockcert contains the original document and the signature/merkle proof. JSON-LD normalization, along with merkle proof allows predictable verification of the issued document

Note that the last JSON-LD signature step is unnecessary. Because each document is sha256 hashed and placed into a merkle tree, issued on the blockchain, and the issuer signing key is the one performing the blockchain transaction, the separate signatureValue is actually unnecessary. 

Why we are using blockchain issuing and verification. Source of trusted timestamp (see details)

## Aligning signature schema and techniques

Concerns with current approach:
- Redundancy in signature schema:
	- open badges/blockcerts allows specification of Issuer Key URI ('creator' field)
	  - https://web-payments.org/vocabs/security#Key
	- 'created' is less important than the blockchain timestamp
- We use Chainpoint schema for merkle proofs in the 'signature' section, but are interested in aligning with other proof techniques, e.g. Proof of Publication
- Generalization of 'signature' for blockchain receipts
	- Remove 'signatureValue' as required field?
	- Per (XXX) thread, there are additional concerns with relying on Koblitz signature as standalone. 
- Dropping of additional fields in JSON-LD normalization
  - Blockcerts addresses this through use of the '@vocab' keyword to detect fields not present in any JSON-LD context.

Concerns with JOSE/JWS:
We are very interested in alignment of json-ld signatures with JWS. Some concerns:
- They are not JSON
https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/6674642d88aaeee07489d98ddd75bf89aff5ecee/topics-and-advance-readings/blockchain-extensions-for-linked-data-signatures.md#json-normalized-clear-text-signatures

## Blockcerts Verification

- Fetch blockchain transaction info
	- issuing address
	- op_return field (or similar anchor)
	- time
 - Issuer profile/Issuer key


Steps:

- Check integrity; has not been tampered with
	- Ensure local hash matches value in proof
	- Ensure value in blockchain transaction matches value in proof
	- Check merkle proof: essentially verification of the intermediate steps in the merkle path
- Signature/authenticity
	- Establish 2-way link between issuer's profile and issuing key. I.e. is this issuing key actually claimed by the issuer? 
	- Establish that the transaction was issued WHEN issuer key was valid
	- JSON-LD signature (EcdsaKoblitzSignature2016) -- technically unnecessary
- Not revoked
	- The Open Badge format expects a revocationList URI, currently expected to be hosted URL in a certain format. See long term notes
- Not expired
	- Open badges standard supplies an expiration date field, which is currently used by verification. See long term notes.


Merkle proofs:
	Currently uses chainpoint library to check correctness of merkle proof. We are interested in generalizing to enable other styles, e.g. [Peter Todd's Open Timestamps](https://petertodd.org/2016/opentimestamps-announcement) and [Proof of Publication](https://web-payments.org/specs/source/pop2016/)
  
## Long term questions
- Anything that is assumed to be hosted (issuer profiles, etc) should have high confidence of permanence (e.g. IPFS hosting)
- Key rotation?
- DID
- Putting recipient in the communication
