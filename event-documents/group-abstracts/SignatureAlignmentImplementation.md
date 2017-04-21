# Implementing the LD RSA Signature Suite 2017

By Kim Hamilton Duffy, Rodolphe Marques, Markus Sabadello

## Context

This describes how we adapted LD signatures to the proposed [RSA Signature Suite 2017](https://w3c-dvcg.github.io/lds-rsa2017/) specification, which uses JOSE JWS. This assumes familiarity with LD signatures, and focuses on the specific changes to the algorithm to generate RSA Signature Suite 2017 signatures.

Our biggest obstacle was lack of JWS library support for detached headers. For this reason, we couldn't directly use any JWS libraries; instead we implemented the steps directly, which the rest of this document clarifies.

We propose that these steps be broken out into simple JWS detached signature libraries, which JSON-LD signatures can use a simple API like the following, where payload is assumed to be a detached payload, as described in [RFC 7797](https://tools.ietf.org/html/rfc7797)

```
signature = sign(headers: JSON, payload: STRING);
```

## Steps, Overview

The signing flow follows that of the [JSON-LD signature library](https://github.com/digitalbazaar/jsonld-signatures), the only implementation details being in the createSignature function. A new algorithm, `RsaSignature2017`, was added to implement the new signature suite.

inputs:

- same as before, but algorithm can be `RsaSignature2017` 


At a high level, this flow is:

- ensure algorithm is in accepted set
- add 'created' date of now, if not supplied
- canonicalize using the `GCA2015` algorithm, formerly known as `URDNA2015`
- **Perform RSA Signature Suite 2017 signing**
- compact the signature
- return the JSON-LD document with the signature block added

## RSA Signature Suite 2017 signatures

**Note/TODO** Our prototypes omit the call to `_getDataToHash`, which prefixes the JSON-LD normalized document with the sorted header key/values `created`, `domain`, and `nonce` (all that are supplied). We will follow up on this.


This approach uses JOSE JWS detached payload signing, as described in [RFC 7797](https://tools.ietf.org/html/rfc7797). The JWS headers to use are:

```
protectedHeaders = {
    "alg":"RS256",
    "b64":false,
    "crit":["b64"]
}
```

This will be a protected header, meaning it is part of the signature. JOSE JWS detached payload signing expects the following input:

```
ASCII(BASE64URL(UTF8(JWS Protected Header)) || '.' || JWS Payload  
```

Let's break apart the protected header handling into the steps:

- stringify the protected header JSON, sorting the keys. 
	- sorting is an implementation choice to allow predictability
- encode the stringified header as follows:
	- utf-8 encode
	- base64 url encode
	- ascii encode


To sign, we do the following steps, where `input` is the normalized JSON-LD.

- form the JWS input to sign as <header> + "." + <input>
- RSASHA256 sign the JWS input.
- base64 url encode the signature value
- form the complete signature to be placed in `signatureValue` as <header> + ".." + <base64Signature>
	- In JWS, the payload would normally be between the middle 2 dots, but this is a detached payload
	- Note that the header is included in the signature, so the sorting done in the first step isn't technically necessarily. Verification would need to ensure it uses the same encoded header.

## Reference

JSON-LD signature modification to `_createSignature` to support `RsaSignature2017`

```

if(options.algorithm === 'RsaSignature2017') {
	var crypto = api.use('crypto');
	var signer = crypto.createSign('RSA-SHA256');

	// detached signature headers for JWS
	var protectedHeader = {"alg":"RS256","b64":false,"crit":["b64"]};

	// ensure the stringified version of the protected header has a consistent ordering
	var stringifiedHeader = JSON.stringify(protectedHeader, Object.keys(protectedHeader).sort());

	// utf-8 encode and base64 url encode the protected header.
	// Note that base64url.encode does the following, and Buffer(str) default encoding is utf-8:
	// new Buffer(str).toString('base64')
	var b64UrlEncodedHeader = base64url.encode(stringifiedHeader);

	// ensure resulting string is ascii
	var asciiHeader = Buffer.from(b64UrlEncodedHeader, 'utf-8').toString('ascii');

	// jws input to sign
	var to_sign = asciiHeader + "." + input;

	signer.update(to_sign);
	var signatureBytes = signer.sign(options.privateKeyPem);

	var base64Signature = base64url.encode(signatureBytes);

	// JWS signature is encoded proctected header + '..' + signature
	// .. is because this is a detached payload
	signature = b64UrlEncodedHeader + ".." + base64Signature;
}
```
