# LD Signature Format Alignment

By Kim Hamilton Duffy, Rodolphe Marques, Markus Sabadello

## Abstract

The topic focused on aligning JSON-LD signatures with JOSE JWS signatures, per the [RSA Signature Suite 2017](https://w3c-dvcg.github.io/lds-rsa2017/) specification draft. Rationale and context is provided in [Aligning Signature Formats].

Implementors of JSON-LD had concerns about the impact of JOSE on their implementations. The goal of our workgroup was to build prototypes of the specification to determine feasibility of this approach, impact on existing implementations, and clarify any ambiguities in the specification.


## Status

We have delivered prototypes of the new LD signature format using JOSE JWS in 3 languages: javascript, python, and java. These are not complete or production-ready code, but they suffice to more forward with the aligned signature approach.  TODO links.

We have deliviered a whitepaper on the precise differences between existing LD signatures and the new approach.

Omissions/Followup/Next steps:
- How to embed JSON-LD signature options `created`, `creator` and `nonce`, and `domain`? Same as in `_getDataToHash`, or can we use JWS headers?
- Implement `verify`
- JWS detached signature library (see TODO)
- check end-to-end samples with JOSE group?

