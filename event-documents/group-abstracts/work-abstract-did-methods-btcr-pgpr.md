# Method Specification Work for did:**btcr** and did:**pgpr**

## Summary of conference progress and future plans

### What do did:**btcr** and did:**pgpr** stand for?

<dl>
  <dt>did:<b>btcr</b>:</dt>
  <dd><i>Reference</i> Decentralized Identifier Method for the Bitcoin Blockchain.</dd>

  <dt>did:<b>pgpr</b>:</dt>
  <dd><i>Reference</i> Decentralized Identifier Method for <a href="https://en.wikipedia.org/wiki/Pretty_Good_Privacy">Pretty Good Privacy</a></dd>
</dl>

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
(Disclaimer: CLTV in the image should be CSV.)

We discovered a way to indicate signing keys separate from the control key
(using two nSequence bits).

### Work on did:pgpr

The specification was completely deferred.

One did:pgpr discussion revolved around unplanned loss of a master
key, with the semantics of PGP signature rotation (requiring creating
a new fingerprint and gathering new trust signatures) as the closest
parallel to did:btcr key rotation (where a quorum of cold storage
control keys may be marshalled to prevent revocation of the did:btcr).
Since the purpose of the did:pgpr method specification is primarilly
pedagogical, this technique will be described in the method
specification without judgement.
