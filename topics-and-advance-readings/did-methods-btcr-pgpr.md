# DID Method Specifications / BTCR and PGPR

### Abstract

By defining DID Method Specifications using Bitcoin as an existing
distributed ledger and PGP as existing cryptographic identity
management software, we create bridges for relating two old
technologies to a new one, helping us understand all three.

Considerable responsibilities in maintaining security and privacy have
been enumerated for DIDs, but deferred to the individual method
specifications to resolve.  The first method specification to be
completed will, besides clarifying the requirements for its domain,
provide a baseline security and privacy consideration section, which
other method specifications may refer to for examples.

### Background

Self-sovereign identity offers participating entities a way to safely
separate identities, personas, and contexts that they are asked to
verify in various ways.  The central concept in maintaining this
flexibility is the creation and management of multiple separate
decentralized identifiers (DIDs) for separate roles.

Briefly, DIDs are Uniform Resource Identifiers (URIs) that are
persistent yet do not require a centralized authority to register,
that resolve to a unique specific resource (like a URL), and that can
cryptographically verify their associated metadata.  They are designed
to link to DID Descriptor Objects (DDOs).  DDOs contain key
descriptions that allow one to prove ownership and control of the DID,
and contain service endpoints describing further how to interact with
the identity owner.

October's rebooting-the-web-of-trust-fall2016 conference resulted in
the ["DID (Decentralized Identifier) Data Model and Generic Syntax
1.0"
specification](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/draft-documents/did-implementer-draft-10.md).

As the spec explains:

> To use a DID with a particular distributed ledger or network
> requires defining a **DID method** in a separate **DID method
> specification**.  A DID method specifies the set of rules for how a
> DID is registered, resolved, updated, and revoked on that specific
> ledger or network.

Now we may turn to the proposed DID methods.

----

## BTCR DID Method Specification

### Abstract

This is the DID method specification for a layer-2 protocol using
the Bitcoin ledger's properties to implement self-sovereign
identity.  It was initially imagined by Christopher Allen.

This specification covers the BTCR DID scheme and methods.

In particular, one objective is to explore building the layer on top
of the Bitcoin protocol without creating many transactions wasting
OP_RETURN space.  Another objective is to show how key rotation may be
accomplished.

### See Also

Blockstack.org also secures identities on the Bitcoin blockchain.  They have a [whitepaper](https://blockstack.org/papers).

Several other companies provide identity services anchored in other
blockchains, with varying degrees of added value through services
available through the company.

----

## PGPR DID Method Specification

### Abstract

This is the DID method specification attempting to describe a
consistent scheme for using PGP's existing toolkit to: create,
read/verify, update, delete/revoke, and resolve as explained in the
DID spec.

Although it should be possible to deliver a working implementation,
the primary goal of the PGPR method specification is pedagogical.  In
particular, one objective is to show the difficulties of key rotation
using PGP, and how the DID spec offers a framework that demands
improvement.
