# Introduction

# Terminology

* Authentication Client - the means by which a user responds to an authentication challenge
* Content Server - the protected resource the user is seeking to access
* Challenge Endpoint - the means by which an authentication challenge is delivered to the user (typically a URI stored in DDO)

# Use Cases

Logging in with | Authentication Client | Challenge Channel | Notes
web browser | same browser | same browser | The user is accessing some content with a web browser, and authenticating themselves using the same browser
web browser | mobile browser | mobile browser | The user is accessing some content with a web browser (most likely a laptop or tablet), and authenticating themselves using a browser on a separate device (most likely their mobile phone) - orchestrating that is the user's responsibility
web browser | mobile app | mobile app | The user is accessing some content with a web browser, and is authenticating themselves using an app on their mobile device - orchestrating that is the user's responsibility
mobile app | mobile app | mobile app | The user is accessing some content with an app, and is authenticating themselves using a different app - orchestrated via inter-app messaging
web browser | same browser | Challenge Endpoint (in DDO) | Not sure what this one is?
mobile app | Challenge Endpoint | Challenge Endpoint (in DDO) | The user is accessing some content with a web browser, and is authenticating themselves using a client (probably a mobile app) which is connected to the Challenge Endpoint



# Requirements

* MUST be able to cryptographically prove control over a DID
   * Need to support multiple DID methods (the method specs should contain enough detail to determine which key proves control, and which signature scheme is appropriate)
* MUST be able to use a web browser with no extensions to authenticate
* MUST be able to use an app to authenticate
* MUST be able to use a secondary device to authenticate a session on your primary device

# Payload Example

These are payload requirements, to be augmented with examples:

## Challenge

* Will be a lightweight "verifiable claim request" payload
* Should be able to specify the DID (for returning users), although this is not required since the DID will be included in the response
* Should be able to specify the nonce to be signed, although this is not required since it is possible to deterministically generate nonces using a pre-agree scheme
  * Do we want to include explicit support for using timestamps?
* Should be able to request additional attributes to be included in the response claim (or do we want to avoid the drama of designing how that works?)
* Should be able to include credentials (in the form of verifiable claims?) demonstrating the credibility of the Content Server which is requesting authentication
* May specify a particular public key?
   * the user may have several keys associated with a DID, and they are proving control of a DID not a specific key, so we will _not_ set the expectation that the user must use the same key each time
   * if the user responds using a different key than the one the content server requests (they may choose to, or they may have to because they have rotated keys), the content server may perform further authentication (for example, requesting another factor)
* Must be able to deliver the challenge in-band (direct to the user's browser) and out-of-band (to the service endpoint specified by the DDO)
* Must include the endpoint where the response should be sent

## Response

* Will be a verifiable claim
  * Must contain the DID
  * Should contain other attributes requested
* Signature uses a scheme appropriate to the DID?
  * Signature includes the nonce

# Protocol Diagrams



# Notes & Further Issues

* How to support enrolment/registration?
* How to detect the context (is this an in-band or out-of-band authentication)?
* How to support multi-device orchestration (specify a QR code scheme as a minimum)?
* What level of alignment is needed with DID Service Discovery (for now can we agree on a well-known URI scheme to use for sending challenges)?
