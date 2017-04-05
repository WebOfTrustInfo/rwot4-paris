# Aligning Signature Formats

by Manu Sporny, Christopher Allen, Jason Law, and Ryan Shea

As the Verifiable Claims work proceeds, it is important to ensure that all
of the signature formats that are used by Verifiable Claims continue to
follow a coherent design approach. Recent discussions at IETF 98 and WWW2017
have resulted in a breakthrough related to the design approach and
standardization timeline related to Linked Data Signatures. The Rebooting
Web of Trust community should discuss how their use of the signature
formats in Verifiable Claims could benefit from the design changes outlined
in the rest of this paper.

## JOSE JWS and Linked Data Signatures

One of the reasons that Linked Data Signatures, which are used by Verifiable
Claims, did not initially reuse the JSON Web Signing (JWS) specification was
due to a variety of issues outlined in Analysis of JWS and Linked Data
Signatures[1]. We met with Mike Jones and John Bradly,
who were the core designers for JWS, at IETF 98 and worked together to align
the needs of Verifiable Claims and Linked Data Signatures with what the JOSE
stack is capable of providing. In doing so, we found a way that Linked Data
Signatures can re-use JWS to achieve its goals by using a profile of
JSON Web Signatures.

This new approach has the advantage of almost entirely aligning the
Linked Data Signatures specification and the RSA Signature Suite with the
JOSE stack, thus making standardizing the approach far less contentious than
the previous approach.

## Koblitz Curve and Linked Data Signatures

The Koblitz Signature Suite is not capable of re-using the JOSE work because
JWS does not support Koblitz curve signatures. A deep analysis by the
Crypto Forum Research Group does not exist for the secp256k1 curve. The
signature suite can continue to use the current approach listed in the
specification, but we may want to use this opportunity to discuss how the
secp256k1 analysis could progress at the IETF's CRFG.

## Next Steps

We desire to discuss this approach with other organizations that rely on
digital signatures for their products and determine if this new approach is
acceptable to those organizations.
