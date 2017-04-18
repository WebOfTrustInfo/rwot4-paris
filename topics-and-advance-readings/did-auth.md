# DID Auth

*James Monaghan, 2017-04-17, Rebooting the Web of Trust #4, Paris, France*

## Introduction

Despite the advent of [password managers](https://www.lastpass.com/), [two-factor authentication](https://www.turnon2fa.com/) and [single sign-on as-a-service](https://auth0.com/), the need for a more simple, secure and interoperable form of authentication has never been stronger than it is today.

Users have a [multitude of identities](https://blog.dashlane.com/infographic-online-overload-its-worse-than-you-thought/) and associated credentials to manage, personal data is scattered across dozens of silos, and the last line of defense is almost invariably a password reset email. Within enterprises, [federation](http://openid.net/connect/) eases this burden to some extent by centralizing many of the management aspects, but in the consumer world this added convenience can come with a considerable privacy trade-off.

The list of top level requirements is not long, but a solution which addresses all of them has proved elusive:
* It should be simple for the user, not requiring them to remember different credentials for everywhere they might want to authenticate;
* It should be secure, based on public key cryptography rather than shared secrets (usernames and passwords);
* It should protect privacy, preventing multiple relying parties from colluding about a user without their explicit consent;
* It should allow the user to manage their own keys, rotating them at will or in case of loss/compromise.

## Related Work

Progress away from the use of shared secrets has been made by the [FIDO Alliance UAF Specification](https://fidoalliance.org/specifications/overview/), which offers an interoperability standard for the use of cryptographic authentication. With a FIDO-enabled client, logging in to a website can be as simple as unlocking your phone with a thumbprint but still highly secure. To authenticate, the user proves control of a private key which corresponds to a public key they have registered with the relying party by signing a unique challenge.

Where FIDO has a high degree of "pluggability" at different levels of the stack, [SQRL](https://www.grc.com/sqrl/sqrl.htm) proscribes a specific HTTP protocol and a scheme for deriving website-specific identifiers and keys from a single master key which, in its simplicity, eliminates many of the shortcomings of legacy approaches.

While promising, both of these approaches still have a credential management issue: the user has a specific public key stored at each relying party, and must invalidate or replace that in case they need to change their private key for some reason. In other words, while the user holds the key, the _identity_ itself still lives with the relying party, and as such is never fully under the user's control.

## Towards Independent Identity

The advent of distributed ledger technology has provided a means for individuals to become [self-sovereign](http://www.lifewithalacrity.com/2016/04/the-path-to-self-soverereign-identity.html) over their identity. Individuals neither have to "rent" an identity from a service provider nor somehow host their own identity provider infrastructure: they can simply assert control over an identifier on the ledger by proving control of the corresponding private key.

The difference between authenticating as the owner of an _identifier_ versus the owner of a _specific key_ is subtle but important: the extra level of indirection allows the individual to manage key rotation, delegation of authority, synchronization across devices and more in a manner which is fully under their control and transparent to the relying party. An open specification for authentication using an identifier on a distributed ledger could be highly secure and interoperable while still being easy for users and protecting their privacy.

[BitID](https://github.com/bitid/bitid/blob/master/BIP_draft.md) proposes a general-purpose authentication system quite similar to SQRL but using a Bitcoin wallet address insted of a site-specific public key. While the Bitcoin blockchain is a venerable ledger with an active developer community, it is challenging to implement an identity scheme on top of it which meets the trust, latency and privacy standards that most institutions require.

One could take a similar scheme and apply it to [Sovrin](https://www.sovrin.org/The%20Technical%20Foundations%20of%20Sovrin.pdf), which has sought to mitigate the shortcomings of public permissionless ledgers such as Bitcoin and Ethereum by creating a _public permissioned_ ledger specifically for self-sovereign identity. Like FIDO or SQRL, this would allow the user to have a different identifier for each relying party, reducing correlation risk but preserving the advantages of decentralized key management.

The recently announced [Blockstack Auth](https://blockstack.org/blog/serverless-sign-in-with-blockstack-auth) offers a glimpse of how the experience might be in the future if we had a more fully decentralized internet which users browsed using identity-aware smart clients.

## Independent and Interoperable

If in our haste to fix the centralization and security issues of legacy authentication approaches we force users to deal with a different but equally fragmented set of tools and standards (picture Bitcoin Auth, Blockstack Auth, Sovrin Auth, and so on), then we will have failed as an industry. The greatest advantages of openness and decentralization are realized when interoperability is an explicit requirement.

The [DID (decentralized identifier) specification](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/did-implementer-draft-10.pdf), partially developed at previous RWOT events and funded in part by the U.S. Department of Homeland Security, has become a defacto standard for establishing interoperable self-sovereign digital identity. Given the need for strong authentication as the foundation for any subsequent trusted peer interaction, it is proposed that a **DID Auth** specification be created to define the standard for authentication based on DIDs.

## Next Steps

If there is sufficient interest, work on drafting a DID Auth specification could begin at the Rebooting the Web of Trust #4 conference April 19-21 2017 in Paris and continue the Internet Identity Workshop May 2-4 2017 in Mountain View.
