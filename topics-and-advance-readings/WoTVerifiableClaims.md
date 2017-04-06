# Verifiable Claims and Web of Trust

by Manu Sporny, Christopher Allen, Joe Andrieu, Matthew Collier, Dave Longley, and Adam Lake

The Rebooting Web of Trust community has been exploring the intersection of
Distributed Ledger Technology, Verifiable Claims, Web of Trust, and the Refugee
Crisis. The discussions surrounding these topics have led to a variety of
technologies being developed that are mature enough to be organized into
experimental solutions.

During this meeting, we would like to focus on building experimental solutions
for two primary use cases. These use cases are:

1. Asserting a Verifiable Claim against a government-issued photo ID
   where the person asserting the claim can do so via a smartphone
   web browser.
2. Onboarding a refugee into a Verifiable Claims account where a
   guardian oversees the refugee's account until the refugee
   acquires a device capable of enabling them to take control of their
   account.

## Implementation of Verifiable Claims for Web of Trust

The purpose of the Web of Trust Claims use case is to demonstrate how
Verifiable Claims may be created via peer attestation. Verifiable Claims that
are peer attested can be used to establish a Web of Trust similar to, but more
powerful than, what PGP achieved in the 1990s.

The core of the use case revolves around two individuals attesting to several
important metrics that relate to personhood. Each individual asserts the
other's name and that they checked the name against a government issued photo
ID while both parties were physically present. This establishes that 1) the
person is real, 2) the person is recognized by a government (by holding a
government issued ID), 3) the person is visually similar to the image on the
government  issued ID, and 4) the person's name is present on the government
issued ID.

The Web of Trust Claims use case is expected to result in the following flow:

1. The Issuer provides a QRCode so that the Subject can submit their data to
   the Issuer.
2. The Subject scans the QRCode and packages the Claim into a new QRCode that
   they want the Issuer to digitally sign.
3. The Issuer scans the Subject's Claim QRCode.
4. The Issuer verifies the contents of the Claim by checking the values
   against a government issued photo ID.
5. The Issuer issues the Verifiable Claim and creates a new QRCode for
   the Subject.
6. The Subject scans the digitally signed Verifiable Claim and stores it in
   their digital wallet.

The Web of Trust use case is expected to use Verifiable Claims in the
following format:

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
      issuer: 'https://dmv.va.gov/'
    }]
  },
  signature: {...}
}
```

## Implementation of Verifiable Claims for the Refugee Crisis

The Purpose of the Refugee Crisis use case is to demonstrate how Verifiable
Claims may be created where the Subject of the claims is not able to
immediately store the Verifiable Claims. Achieving this capability would enable
a UNHCR Agent to onboard a refugee when they are discovered and provide
guardianship over their account until the refugee receives a device that
enables them to directly interact with the Verifiable Claims associated with
their account.

The core of this use cases resolves around a UNHCR Agent and a refugee where
the UNHCR Agent onboards the refugee into the UNHCR system. The UNHCR Agent
creates an account for the refugee and associates multiple Verifiable Claims
with the refugee, including: 1) a picture of the refugee, 2) the name of the
refugee, and 3) the place where the refugee was discovered.

The UNHCR Refugee Verifiable Claims use case is expected to result in the
following flow:

1. A Subject (refugee) provides their name to an agent acting on behalf of
   UNHCR.
2. The Issuer creates a digital wallet in "Guardianship" mode for the Subject.
3. The Issuer starts the issuing process into the digital wallet.
4. An image is taken of the subject and uploaded to UNHCR's database.
5. A Verifiable claim for the Subject's name and image is issued by the Issuer
   with the appropriate "claim basis" fields filled out.
6. A barcode band is printed out for the refugee to wear that contains their
   access code to their digital wallet.

The UNHCR Refugee Verifiable Claims use case is expected to use Verifiable
Claims in the following format:


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

We would like to collaborate with the participants of the Fourth Rebooting Web
of Trust Workshop to refine the flows and Verifiable Claims in these use cases.
Our goal is to produce a demo that shows at least one if not both use cases
working by the end of the workshop.
