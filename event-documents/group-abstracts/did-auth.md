# DID Auth Overview

* James Monaghan, Evernym
* Manu Sporny, Digital Bazaar

# Introduction

Quick summary of the points from the [topic paper](../../topics-and-advance-readings/did-auth.md):
* Everyone's doing "blockchain auth" already. We want to standardise on DIDs, and we need interoperability on authentication before we can hope to have interoperability on exchanging verifiable claims and other more sophisticated transactions. We should therefore be doing DID Auth.
* Here's how you authenticate between a client and server by proving control over a DID.

![did-auth](../../supporting-files/did-auth.jpg)

# Terminology

* Authentication Client - the means by which a user responds to an authentication challenge
* Content Server - the protected resource the user is seeking to access
* Challenge Endpoint - the means by which an authentication challenge is delivered to the user (typically a URI stored in DDO)

![actors](../../supporting-files/did-auth-actors.jpg)

# Use Cases

## Two-Step

### Registration

TODO: includes making a connection?

### Authentication

## One-Step

## Device Configurations

<table>
<tr>
<td> Scenario </td><td> Logging in with </td><td> Authentication Client </td><td> Challenge Channel </td><td> Notes </td>
</tr><tr>
<td> 1 </td><td> web browser </td><td> same browser </td><td> same browser </td><td> The user is accessing some content with a web browser, and authenticating themselves using the same browser </td>
</tr><tr>
<td> 2 </td><td> web browser </td><td> mobile browser </td><td> mobile browser </td><td> The user is accessing some content with a web browser (most likely a laptop or tablet), and authenticating themselves using a browser on a separate device (most likely their mobile phone) - orchestrating that is the user's responsibility </td>
</tr><tr>
<td> 3 </td><td> web browser </td><td> mobile app </td><td> mobile app </td><td> The user is accessing some content with a web browser, and is authenticating themselves using an app on their mobile device - orchestrating that is the user's responsibility </td>
</tr><tr>
<td> 4 </td><td> mobile app </td><td> mobile app </td><td> mobile app </td><td> The user is accessing some content with an app, and is authenticating themselves using a different app - orchestrated via inter-app messaging </td>
</tr><tr>
<td> 5 </td><td> web browser </td><td> same browser </td><td> Challenge Endpoint (in DDO) </td><td> Not sure what this one is? </td>
</tr><tr>
<td> 6 </td><td> mobile app </td><td> Challenge Endpoint </td><td> Challenge Endpoint (in DDO) </td><td> The user is accessing some content with a web browser, and is authenticating themselves using a client (probably a mobile app) which is connected to the Challenge Endpoint </td>
</tr>
</table>

## Flow 1

![flow-1](../../supporting-files/did-auth-flow-1.jpg)

## Flow 2

## Flow 3

![flow-3](../../supporting-files/did-auth-flow-3.jpg)

Orchestration (steps 6 & 8) may involve scanning a QR code, communication via Bluetooth, etc.

## Flow 4

## Flow 5

## Flow 6

![flow-6](../../supporting-files/did-auth-flow-6.jpg)

This assumes the Content Server is already aware of the DID (or it is communicated in step 1).

# Requirements

* MUST be able to cryptographically prove control over a DID
   * Need to support multiple DID methods (the method specs should contain enough detail to determine which key proves control, and which signature scheme is appropriate)
* MUST be able to use a web browser with no extensions to authenticate
* MUST be able to use an app to authenticate
* MUST be able to use a secondary device to authenticate a session on your primary device

# Payload Example

These are protocol feature requirements, to be augmented with examples:

## Challenge

* Will be a lightweight "verifiable claim request" payload
* Should be able to specify the DID (for returning users), although this is not required since the DID will be included in the response
* Should be able to specify the nonce to be signed, although this is not required since it is possible to deterministically generate nonces using a pre-agree scheme
  * Do we want to include explicit support for using timestamps?
* Should be able to request additional attributes to be included in the response claim (or do we want to avoid the drama of designing how that works?)
  * You might want a key to have been endorsed by a trusted party who certifies the user really has control (e.g. Yubikey)
* Should be able to include credentials (in the form of verifiable claims?) demonstrating the credibility of the Content Server which is requesting authentication
* May specify a particular public key?
   * the user may have several keys associated with a DID, and they are proving control of a DID not a specific key, so we will _not_ set the expectation that the user must use the same key each time
   * if the user responds using a different key than the one the content server requests (they may choose to, or they may have to because they have rotated keys), the content server may perform further authentication (for example, requesting another factor)
* Must be able to deliver the challenge in-band (direct to the user's browser) and out-of-band (to the service endpoint specified by the DDO)
* Must include the endpoint where the response should be sent

## Response

* Will be a verifiable claim
  * Must contain the DID
  * May contain other attributes requested (although clients can elect not to provide these)
* Signature uses a scheme appropriate to the DID?
  * Signature includes the nonce

# Protocol Diagrams

# Multi-Device Orchestration

TODO: at least a way to use QR codes to link a browser session to a mobile device

# Standards Alignment

TODO explain alignment with (and improvements over) other standards (and non-standard implementations):
* Web auth / FIDO / JWT/JWS
* DID spec / DID service discovery
* (SQRL, BitID, etc)

# Notes & Further Issues

* Need to show the enrolment/registration flow as well as the login/authentication flow
* How to detect the context (is this an in-band or out-of-band authentication)?
* Need to account for delays in the protocol (poor connectivity, need for MFA, etc)
* Need to call out the privacy implications of using timestamps for nonces
* Heard lots of good ideas on Thursday for making sure this is useful for more than just websites - need to capture that

## Driving Adoption

* "DID Auth" is a terrible name for marketing purposes - consumers will never go for it
  * "Super Sign-On" is nice
  * Do we need a logo, trust mark, UX guidelines to drive adoption?
  * Use a trademark to drive conformance (avoid OpenID "issues")
* Want to avoid "NASCAR syndrome" with login buttons
  * Can the Content Server be aware of the authentication methods available to the user so it can display appropriate options? This has privacy implications.
* Should collect a list of apps from the RWOT community which have implemented flows _similar_ to this, and ask them to pledge compliance:
  * Digital Bazaar / Authorization.io
  * uPort
  * Evernym
  * Dappre
  * Aevatar
  * Consent?
