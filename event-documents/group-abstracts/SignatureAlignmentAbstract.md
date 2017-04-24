# LD Signature Format Alignment

By Kim Hamilton Duffy, Rodolphe Marques, Markus Sabadello

## Abstract

Our goal was to develop working prototypes of the proposed [RSA Signature Suite 2017](https://w3c-dvcg.github.io/lds-rsa2017/) spec to answer two questions. First, is the spec sufficiently clear for implementors? Second, what is the impact to existing JSON-LD signature implementations?

Existing implementors of JSON-LD signatures expressed concerns about the impact/feasibility of JSON Web Signatures, as described in [Aligning Signature Formats](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/SignatureFormatAlignment.md). This working group aimed to investigate/derisk these concerns, as follows:

- Develop prototypes in several key languages, to ensure library support
- Ensure minimal impact on usability of Verifiable Claims and JSON-LD signatures

Note that the only algorithm supported by RSA Signature Suite 2017 is RS256 -- a subset of the [JSON Web Signature Unencoded Payload Option RFC 7797](https://datatracker.ietf.org/doc/html/rfc7797).

## Status

We delivered prototypes of the new RSA Signature Suite 2017 that provided sufficient confidence to move forward with the proposed aligned signature approach.

We verified that the impact to existing JSON-LD signature implementations -- and usability in general -- was minimal. Specifically, the RSA Signature Suite 2017 avoids the requirement of preserving the original binary form of the payload.

The major obstacle we encountered while performing this work was the lack of JSON Web Signature library support for detached paylods, which is addressed in "Next Steps"

### Implementations of LD JWS signing

- Javascript/Node.js: https://github.com/WebOfTrustInfo/jsonld-signatures (this is a fork of JSON-LD signatures official library)
- Python: https://github.com/blockchain-certificates/ld-koblitz-signatures/tree/ld-jws
- Java: https://github.com/WebOfTrustInfo/ld-signatures-java

### JSON-LD JWS Implementation Guidance (cross-platform)

We created a whitepaper to describe the precise differences between existing LD signatures and the new approach.

- [Signature Alignment Implementation](SignatureAlignmentImplementation.md)

## Next steps

Because the primary gap was lack of JWS detached payload support -- and therefore accounted for most of our development work -- we propose to recraft the prototypes as JWS detached signature libraries. Such a library would expose simple sign and verify APIs, for example:

```
signature = sign(headers: JSON, payload: STRING);

```

Where payload is assumed to be a detached payload, as described in [RFC 7797](https://tools.ietf.org/html/rfc7797)

Such a library would facilitate minimal changes to existing JSON-LD signature implementations.

Detailed list of next steps:

- Determine how to address problem that JWS implementations are lacking support for RFC 7797:
  - Recraft prototypes as JWS detached signature libraries to provide a RFC 7797 implementation (with a least RS256) to either be merged into official JWS libraries, or standalone bridges until official support is provided.
  - Double-check end-to-end samples with RS256 algorithm (not provided in RFC 7797 or PHP tests)
- Determine way to embed JSON-LD signature options `created`, `creator` and `nonce`, and `domain`. Same as in `_getDataToHash`, use JWS headers, or other.
- Add new signature suite to JSON-LD signature libraries, consuming JWS detached payload implementation
- Prototype `verify`
- Merkle proof draft spec (deprioritized)

