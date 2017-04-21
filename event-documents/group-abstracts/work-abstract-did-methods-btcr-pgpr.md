# Method Specification Work for did:btcr and did:pgpr

## Summary of conference progress and future plans

### Review of Discussion

Work progressed under the DID-family-of-specifications working
group, which concentrated on DKMS and understanding the implications
of DID-auth.  However, the group dedicated a little bit of time to
reviewing the general scheme for did:btcr, with an example involving
key rotation methodology.

### Work on did:btcr

An [outline of the
specification](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/draft-documents/btcr-did-method-spec.md)
was proposed, following requirements of the general DID spec.

Special attention was given to regenerating "deterministic DDOs"
(possibly to be renamed to "deterministic DID Resources") from
the DID's chain of validity, which allows conformant use of a
valid Bitcoin address so that the did:btcr method understands
ownership and control without pointing to any external data.

We reviewed key rotation methodology, finding
two methods:

* one with the tradeoff of requiring twice the transaction fees, and

* one that costs less but requires online monitoring for cases of theft.

There is [an
infographic](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/event-documents/photos/btcr-infographic-20170421.jpg)
showing how the general scheme is implemented in Bitcoin
transactions: ![alt text](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/event-documents/photos/btcr-infographic-20170421.jpg)

We discovered a way to indicate signing keys separate from the control key
(using two nSequence bits).

[rgrant 20170421 15:35 CEST] current state of colored coins
https://github.com/Colored-Coins/Colored-Coins-Protocol-Specification/wiki

### Work on did:pgpr

The specification was completely deferred.

One did:pgpr discussion revolved around the semantics of PGP
signature rotation as the closest parallel to did:btcr key
rotation.
