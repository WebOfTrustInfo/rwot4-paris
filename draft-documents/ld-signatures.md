# LD Signature Format Alignment

By Kim Hamilton Duffy, Rodolphe Marques, Markus Sabadello, Manu Sporny

## Abstract

The goal of the "LD Signature Format Alignment" Working Group at Rebooting the Web of Trust IV was to investigate the feasibility and impact of the proposed [2017 RSA Signature Suite](https://w3c-dvcg.github.io/lds-rsa2017/) spec, which brings JSON-LD signatures into alignment with the JOSE JSON Web Signature (JWS) standards.

The 2017 RSA Signature Suite is based on [RFC 7797](https://tools.ietf.org/html/rfc7797), the JSON Web Signature (JWS) Unencoded Payload Option specification. The unencoded payload options that avoids [past concerns about use of JWS](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/topics-and-advance-readings/blockchain-extensions-for-linked-data-signatures.md), and achieves the following:

 * Re-uses a signature format that has already been approved by IETF, and therefore no new security review is needed
 * Digitally signs JSON
 * Digitally signs Linked Data
 * Avoids base64 encodings of the payload (through the unencoded payload option)
 * Re-uses the same signature format that Verifiable Claims use.

Our working group had two primary questions about the proposed 2017 RSA Signature Suite:

1. Is the specification sufficiently clear for implementors?
2. Is there a negative usability impact to LD signature implementations using this signature suite?

To answer these questions, we developed prototypes for the suite in several key programming languages to assess:

- Availability of library support for JWS unencoded payload options
- Impact to existing LD signature implementations, e.g. [jsonld-signatures library](https://github.com/digitalbazaar/jsonld-signatures)
- Impact to usability of Verifiable Claims (and others) using JSON-LD signatures with this signature suite.


## Status

We accomplished our goals as follows:

1. We delivered prototypes for 2017 RSA Signature Suite that provided sufficient confidence to move forward with the proposed aligned signature approach. 
2. We verified that there was no significant impact to existing LD signature implementations — and usability in general. Specifically, use of the unencoded payload option avoids the requirement of preserving the original binary form of the payload.

The major obstacle we encountered while performing this work was the lack of JSON Web Signature library support for unencoded payloads, which is addressed in "Next Steps".


### Implementations of LD JWS signing

The following prototypes were developed:

- For Javascript/Node.js: https://github.com/WebOfTrustInfo/ld-signatures-js (this is a fork of JSON-LD signatures official library)
- For Python: https://github.com/WebOfTrustInfo/jsonld-signatures-python (TODO: pending rename)
- For Java: https://github.com/WebOfTrustInfo/ld-signatures-java

### JSON-LD JWS Implementation Guidance (cross-platform)

A white paper, which follows, describes the precise differences between existing LD signatures and the new approach.

## Next Steps

The primary gap in developing these prototypes, which accounted for most of our development work, was lack of library support for JWS unencoded payloads. To work around this limitation, our implementations mirrored the only implementation we found, available in the [JOSE PHP library](https://github.com/Spomky-Labs/josePHP). A cleaner solution we propose is to recraft our prototypes as JWS unencoded payload libraries. 

Such a library would expose simple sign-and-verify APIs, for example:
```
signature = sign(headers: JSON, payload: STRING);
```
In this example, payload is assumed to be a detached payload, as described in [RFC 7797](https://tools.ietf.org/html/rfc7797).

This library would facilitate minimal changes to existing JSON-LD signature implementations.

### Detailed List of Next Steps

- Determine how to address problem that JWS implementations lack support for RFC 7797:
  - Recraft prototypes as JWS detached-signature libraries to provide a RFC 7797 implementation (with a least RS256) to either be merged into official JWS libraries or to act as standalone bridges until official support is provided.
  - Double-check end-to-end samples with RS256 algorithm (not provided in RFC 7797 or PHP tests).
- Determine way to embed JSON-LD signature options `created`, `creator` and `nonce`, and `domain`. Same as in `_getDataToHash`, use JWS headers, or other.
- Prototype `verify`.
- - Add 2017 RSA Signature suite to JSON-LD signature libraries, consuming JWS detached payload implementation.

==========================================================================================================================================

# Implementing the 2017 RSA Signature Suite in a LD signature library

By Kim Hamilton Duffy, Rodolphe Marques, Markus Sabadello

This document describes specific steps and issues with implementing the 2017 RSA Signature Suite in an existing LD signature library.

## Source of Truth 

RFC 7797 does not include an RS256 testcase, so we created a source of truth using the JOSE [implementation](https://github.com/Spomky-Labs/jose) (PHP) that implements the RFC 7797 spec. We created a detached payload / RS256 unit test to obtain a source of truth.

```php

    public function testCompactJSONWithUnencodedDetachedPayloadRS256()
    {
        $payload = '$.02';
        $protected_header = [
            'alg'  => 'RS256',
            'b64'  => false,
            'crit' => ['b64'],
        ];

        $key = JWKFactory::createFromKeyFile(
            __DIR__.'/../Unit/Keys/RSA/private.encrypted.key',
            'tests', // password for key
            [
                'kid' => 'My Private RSA key',
                'use' => 'sig',
            ] // these options do not affect outcome of this test
        );

        $jws = JWSFactory::createJWSWithDetachedPayloadToCompactJSON($payload, $key, $protected_header);
        $this->assertEquals('eyJhbGciOiJSUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..fZRkjTTrcXdUovHjghM6JvlMhJuR1s8X1F4Uy_F4oMhZ9KtF2Zp78lYSOI7OxB5uoTu8FpQHvy-dz3N4nLhoSWAi2_HrxZG_2DyctUUB_8pRKYBmIdIgpOlEMjIreOvXyM6A32gR-PdbzoQq14yQbbfxk12jyZSwcaNu29gXnW_uO7ku1GSV_juWE5E_yIstvEB1GG8ApUGIuzRJDrAAa8KBkHN7Rdfhc8rJMOeSZI0dc_A-Y7t0M0RtrgvV_FhzM40K1pwr1YUZ5y1N4QV13M5u5qJ_lBK40WtWYL5MbJ58Qqk_-Q8l1dp6OCmoMvwdc7FmMsPigmyklqo46uyjjw', $jws);


        $loader = new Loader();
        $loaded = $loader->loadAndVerifySignatureUsingKeyAndDetachedPayload(
            $jws,
            $key,
            ['RS256'],
            $payload,
            $index
        );

        $this->assertInstanceOf(JWSInterface::class, $loaded);
        $this->assertEquals(0, $index);
        $this->assertEquals($protected_header, $loaded->getSignature(0)->getProtectedHeaders());

    }

```

Note this test uses the `{"alg":"RS256","b64":false,"crit":["b64"]}` header and `$.02` as the unencoded payload.

The input of the signing function should match `eyJhbGciOiJSUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19.$.02`
and the resulting signature should match `eyJhbGciOiJSUzI1NiIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..fZRkjTTrcXdUovHjghM6JvlMhJuR1s8X1F4Uy_F4oMhZ9KtF2Zp78lYSOI7OxB5uoTu8FpQHvy-dz3N4nLhoSWAi2_HrxZG_2DyctUUB_8pRKYBmIdIgpOlEMjIreOvXyM6A32gR-PdbzoQq14yQbbfxk12jyZSwcaNu29gXnW_uO7ku1GSV_juWE5E_yIstvEB1GG8ApUGIuzRJDrAAa8KBkHN7Rdfhc8rJMOeSZI0dc_A-Y7t0M0RtrgvV_FhzM40K1pwr1YUZ5y1N4QV13M5u5qJ_lBK40WtWYL5MbJ58Qqk_-Q8l1dp6OCmoMvwdc7FmMsPigmyklqo46uyjjw`

Our prototypes successfully matched this testcase, and matched results on JSON-LD claim inputs.

## LD signature flow

### Overview

The signing flow for the 2017 RSA Signature Suite is identical to other signature suites in the [JSON-LD signature library](https://github.com/digitalbazaar/jsonld-signatures); the processing required to implement 2017 RSA Signatures is confined to step #4 bolded below (all other steps are unchanged). A new algorithm, `RsaSignature2017`, was added to implement this signature suite.

The LD signature algorithm works as follows:

Inputs:
- JSON-LD headers (nonce, created, creator, ...) same as before, algorithm should be `RsaSignature2017` 
- JSON-LD document

JSON-LD Signing Algorithm:

1. Ensure algorithm is in accepted set
2. Add `created` date of now, if not supplied
3. Canonicalize using the `GCA2015` algorithm, as specified in the 2017 RSA Signature Suite specification (NOTE: `GCA2015` was formerly called `URDNA2015`)
4. **Sign with the 2017 RSA Signature Suite** (details in next section)
5. Compact the signature

Outputs:
- JSON-LD document with the signature block added


### Signing with the 2017 RSA Signature Suite

This section drills into step #4 above.

To extend the [JSON-LD signature library](https://github.com/digitalbazaar/jsonld-signatures) to support the 2017 RSA Signature Suite, we added a new algorithm type -- `RsaSignature2017` -- and a new processing case for this type in the function `createSignature`.

First, suppose a JWS library with unencoded payload support were available. If so, then the steps would be:

1. Form the JWS Headers

Per [RFC 7797](https://tools.ietf.org/html/rfc7797), creating a JWS signature using the unencoded payload option requires the JWS Header parameters `"b64":false` and `"crit":["b64"]`. In addition to these parameters, `RsaSignature2017` specifies using RSA Signatures with SHA-256. This corresponds to a JWS signing algorithm of `RS256`.

In sum the complete set of JWS headers used for a 2017 RSA Signature is:
```
{
    "alg":"RS256",
    "b64":false,
    "crit":["b64"]
}
```

2. Call the JWS library with headers from #1 (parameter 1: `headers`) and the JSON-LD canonicalized payload (parameter 2: `payload`)

```
result = sign(headers: JSON, payload: STRING);
```

3. Update the LD `signature` block to contain `signatureValue=<result>`

#### Implementing JWS unencoded payload signing

In step #2 above, we assumed the availabilty of a JWS library supporting unencoded payloads. Because we only found a PHP library supporting unencoded payloads, we needed to reimplement those steps.

Per [RFC 7797](https://tools.ietf.org/html/rfc7797), when the `b64` header parameter is used, it must be integrity protected. Therefore it must occur within the JWS Protected Header (meaning it is part of the input that is signed). Also, per RFC7797, the expected input to sign is formatted as follows:

`ASCII(BASE64URL(UTF8(JWS Protected Header)) || '.' || JWS Payload`

In our case, `JWS Payload` is the normalized JSON-LD.

This yields the following steps:

1. Format the input to sign: 
    1. Stringify the protected header JSON, sorting the keys. 
	    - Note: sorting is an implementation choice to allow predictability
    2. Encode the stringified header as follows:
	    1. utf-8 encode
	    2. base64 url encode
	    3. ascii encode
	3. Form the JWS input to sign as `<header> + "." + <payload>`
	    - The critical distinction here is that `payload` is not base64 encoded, per the b64=false argument. 
2. Sign::
    1. RSASHA256-sign the JWS input
    2. base64-url-encode the signature value
3. Return the signature result `<header> + ".." + <base64Signature>`
    - The `..` indicates a JWS detached payload. Note that typically in in JWS, the payload be between the middle 2 dots.

Notes:
1. Note that the header is included in the signature, so the sorting done during the protected header handling isn't technically necessarily. Verification would need to ensure it uses the same encoded header.
2. Our prototypes omit the call to `_getDataToHash`, which prefixes the JSON-LD normalized document with the sorted header key/values `created`, `domain`, and `nonce` (all that are supplied). We need to decide whether to use that approach, or to rely on JWS headers (if protected headers, they are part of the signed payload).


## Steps to Verify

The verification algorithm has not yet been implemented, so this is just a tentative description of what should happen:

1. Remove the `signature` from the JSON-LD document.
2. Normalize the resulting JSON-LD document (without the `signatureValue` key).
3. SHA256-hash the normalized JSON-LD.
4. Use the hash and the payload as inputs to JWS verification algorithm.

## Problems Encountered

### Lack of JWS detached payload library support

As described above, the only library we found that supports detached payloads was the [PHP JOSE](https://github.com/Spomky-Labs/jose) library. 

### Inconsistent ordering of JWS headers

To our knowledge the JOSE specs do not specify how JSON headers should be ordered. In our implementations, we ensured consistent lexicographical sorting of JWS headers. This is not critical since the encoded header is included in the signature, but our goal was to produce consistent signatures (similar to what's done in `_getDataToHash`.

Specifying the sorting of the keys, the separators and the encoding should be enough for any implementation to be able to produce the same signature.

Example in python:

```python
import json

header = {'alg': 'RS256', 'b64': False, 'crit': ['b64']}

# stringify json
# there are no guarantees about the ordering of the keys and the separators use
# a whitespace between the keys
json.dumps(header)
'{"crit": ["b64"], "alg": "RS256", "b64": false}'

# we can specify the separators. In this case we say we don't want whitespaces
json.dumps(header, separators=(',', ':'))
'{"crit":["b64"],"alg":"RS256","b64":false}'

# and we can specify the ordering of the keys
json.dumps(header, separators=(',', ':'), sort_keys=True)
'{"alg":"RS256","b64":false,"crit":["b64"]}'

# ultimately we can specify the encoding to use and return a bytestring that
can then be used to base64 encode / sign / hash
json.dumps(header, separators=(',', ':'), sort_keys=True).encode('utf-8')
b'{"alg":"RS256","b64":false,"crit":["b64"]}'
```

## Reference: Modifications to javascript JSON-LD signature library to support `RsaSignature2017`

The only modifications are:
- Add new algorithm type `RsaSignature2017`
- Add new path to `_createSignature` to support `RsaSignature2017`
- TBD additional JSON-LD headers (nonce, created, creator, ...)

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

**Reminder** Most of these steps should not be implemented directly in the JSON-LD signatures library as shown here; instead they should be refactored into a JWS detached payload library.


https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/SignatureFormatAlignment.md
