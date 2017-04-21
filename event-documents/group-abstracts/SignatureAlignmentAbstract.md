# LD Signature Format Alignment

By Kim Hamilton Duffy, Rodolphe Marques, Markus Sabadello

## Abstract

The topic focused on aligning JSON-LD signatures with JOSE JWS signatures, per the [RSA Signature Suite 2017](https://w3c-dvcg.github.io/lds-rsa2017/) specification draft. Rationale and context is provided in [Aligning Signature Formats](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/SignatureFormatAlignment.md).

Implementors of JSON-LD had concerns about the impact of JOSE on their implementations. The goal of our workgroup was to build prototypes of the specification to determine feasibility of this approach, impact on existing implementations, and clarify any ambiguities in the specification.

We wanted to also tackle the W3c draft spec for Merkle proofs, but did not get to this.


## Status

We have delivered prototypes of the new LD signature format using JOSE JWS in 3 languages: javascript, python, and java. These are not complete or production-ready code, but they suffice to more forward with the aligned signature approach.

### Implementations of LD JWS signing

- Node.js: https://github.com/blockchain-certificates/jsonld-signatures (this is a fork of LD signature official library)
- Python: https://github.com/blockchain-certificates/ld-koblitz-signatures/tree/ld-jws
- Java: https://github.com/WebOfTrustInfo/ld-signatures-java

### LD JWS Implementation Guidance (cross-platform) 
We have created 2 whitepapers on the precise differences between existing LD signatures and the new approach.

- [[SignatureAlignmentImplementation.md]]
- [[SignatureAlignmentImplementation-part2.md]]

## Next steps

Our biggest obstacle was lack of JWS library support for detached headers. For this reason, we couldn't directly use any JWS libraries; instead we implemented the steps directly, which the rest of this document clarifies.

We propose that these steps be broken out into simple JWS detached signature libraries, which JSON-LD signatures can use a simple API like the following, where payload is assumed to be a detached payload, as described in [RFC 7797](https://tools.ietf.org/html/rfc7797)

```
signature = sign(headers: JSON, payload: STRING);
```

Full list:

- How to embed JSON-LD signature options `created`, `creator` and `nonce`, and `domain`? Same as in `_getDataToHash`, or can we use JWS headers?
- Implement `verify`
- JWS detached signature library (see TODO)
- check end-to-end samples with JOSE group?
- JWS detached signature libraries
- Merkle proof draft spec
