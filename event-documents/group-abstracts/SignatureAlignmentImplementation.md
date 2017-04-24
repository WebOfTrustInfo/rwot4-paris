# Implementing the JSON-LD RSA Signature Suite 2017

By Kim Hamilton Duffy, Rodolphe Marques, Markus Sabadello

This describes specific steps and issues with implementing the RSA Signature Suite 2017.

This document assumes familiarity with JSON-LD signatures, and focuses on the specific changes to the algorithm to generate RSA Signature Suite 2017 signatures. Note that many of these steps should be performed by a detached payload aware JWS library.

## Source of Truth 

RFC 7797 does not include an RS256 testcase, so we created a source of trust using the one JOSE [implementation](https://github.com/Spomky-Labs/jose) (PHP) that implemented the RFC 7797 spec. We created a detached payload / RS256 unit test to obtain a source of truth.

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


## Creating JSON-LD signatures with JSON-LD RSA 2017 Signature Suite

### Overview

Starting with a JSON-LD document, we want to produce a JSON Web Signature:

1. Normalize the JSON-LD with the URDNA2015 algorithm (now called GCA2015)
2. SHA256 hash the normalized JSON-LD
3. Use the hash as the input for JWS signature with the header `{"alg":"RS256","b64":false,"crit":["b64"]}`
4. Create a new key `signatureValue` in the JSON-LD document and use the
   generated signature as its value.
   
### Detailed steps 

This describes the detailed signing steps, including processing due to lack of JWS library support for detached payloads.

The signing flow is identical to other signature suites in the [JSON-LD signature library](https://github.com/digitalbazaar/jsonld-signatures); the only modifications required are in the `createSignature` function. A new algorithm, `RsaSignature2017`, was added to implement this signature suite.

**Note** A proper implementation would recraft these steps as a JWS detached signature library, as opposed to including these steps in a JSON-LD signature library.

Inputs:

- JSON-LD headers (nonce, created, creator, ...) same as before. Algorithm should be `RsaSignature2017` 
- JSON-LD document

JSON-LD Signing Algorithm:

- ensure algorithm is in accepted set
- add 'created' date of now, if not supplied
- canonicalize using the `GCA2015` algorithm (formerly`URDNA2015`)
- **Perform RSA Signature Suite 2017 signing**
- compact the signature
- return the JSON-LD document with the signature block added

### RSA Signature Suite 2017 signatures

**Note/TODO** Our prototypes omit the call to `_getDataToHash`, which prefixes the JSON-LD normalized document with the sorted header key/values `created`, `domain`, and `nonce` (all that are supplied). We need to decide whether to use that approach, or to rely on JWS headers (if protected headers, they are part of the signed payload)

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


## Steps to verify

We have not implemented the verification algorithm so this is just a tentative
description of what should happen:

1. Remove the `signature` from the JSON-LD document
2. Normalize the resulting JSON-LD document (without the `signatureValue` key)
3. SHA256 hash the normalized JSON-LD
4. Use the hash and the payload as inputs to JWS verification algorithm


## Problems encountered

### Lack of JWS detached payload library support

As described above, the only library we found that supports detached payloads was the [PHP JOSE](https://github.com/Spomky-Labs/jose) library. 

### Consistent ordering of JWS headers

To our knowledge the JOSE specs do not specify how json headers should be ordered. In our implementations, we ensured consistent lexicographical sorting of JWS headers. This is not critical since the encoded header is included in the signature, but our goal was to produce consistent signatures (similar to what's done in `_getDataToHash`.

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


## Modifications to javascript JSON-LD signature library to support `RsaSignature2017`

The only modifications are:
- Add new algorithm `RsaSignature2017`
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

**Reminder** These steps should not be implemented directly in the JSON-LD signatures library; instead they should be refactored into a JWS detached payload library.
