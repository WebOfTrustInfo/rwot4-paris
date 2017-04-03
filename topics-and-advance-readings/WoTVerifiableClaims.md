# Verifiable Claims and Web of Trust

by Manu Sporny, Christopher Allen, Joe Andrieu, Matthew Collier, Dave Longley, and Adam Lake

Over the last several meetings, the Rebooting Web of Trust community has been exploring the intersection of Distributed Ledger Technology, Verifiable Claims, Web of Trust, and the Refugee Crisis. The discussions surrounding these topics have led to a variety of technologies being developed that are mature enough to be organized into an experimental solution.

During this meeting, we would like to focus on building experimental solutions for two primary use cases. These use cases are:

1. Asserting a Verifiable Claim against a government-issued photo ID
   where the person asserting the claim is an ordinary person.
2. Onboarding a refugee into a Verifiable Claims ecosystem where a
   guardian oversees the refugee's Verifiable Claims until the refugee
   acquires a device capable of enabling them to take control of their
   digital wallet.

## Implementation of Web of Trust Claims

The Web of Trust Verifiable Claims use case is expected to result in the following flow:

1. A Subject provides their DID to the Issuer by scanning a QRCode on the Issuer's device and submitting a signed Verifiable Claim for their DID.
2. The issuer verifies the DID on their device.
3. The issuer checks the forms of physical ID necessary for the claim that they are making.
4. A Verifiable claim for the Subject's name is issued by the Issuer with the appropriate "claim basis" fields filled out.
5. A QRCode is displayed to the Subject which they can scan to pick up their Verifiable Claim.

The Web of Trust Verifiable Claims use case is expected to use Verifiable Claims in the following format:

```javascript
{
  '@context': 'https://w3id.org/wot/v1',
  claim: {
    id: 'did:pat-does-did',
    name: 'Pat Doe'
  },
  claimBasis: [{
    type: 'VerifiedPhysicalCredential',
    credentialType: {
      type: 'GovernmentPhotoIdCard',
      issuer: 'https://us.gov#foo'
    }]
  },
  signature: {...}
}
```

## Implementation of UNHCR Refugee Verifiable Claims


The UNHCR Refugee Verifiable Claims use case is expected to result in the following flow:

1. A Subject (refugee) provides their name to an agent acting on behalf of UNHCR.
2. The Issuer creates a digital wallet in "Guardianship" mode for the Subject.
3. The Issuer starts the issuing process into the digital wallet.
4. An image is taken of the subject and uploaded to UNHCR's database.
5. A Verifiable claim for the Subject's name and image is issued by the Issuer with the appropriate "claim basis" fields filled out.
6. A barcode band is printed out for the refugee to wear that contains their access code to their digital wallet.

The UNHCR Refugee Verifiable Claims use case is expected to use Verifiable Claims in the following format:


```javascript
{
  '@context': 'https://w3id.org/unhcr/v1',
  claim: {
    id: 'did:jorams-did',
    name: 'Joram',
    image: 'https://unhcr.org/images/2879823749.jpg'
  },
  claimBasis: [{
    type: 'PhysicalPresence',
    credentialType: {
      type: 'Photo',
      issuer: 'https://unhcr.org/agents/49834'
    }]
  },
  signature: {...}
}
```

# Next Steps

We would like to collaborate with the participants of the Fourth Rebooting Web of Trust Workshop to refine the flows and Verifiable Claims in these use cases. Our goal is to produce a demo that shows at least one if not both use cases working by the end of the workshop.
