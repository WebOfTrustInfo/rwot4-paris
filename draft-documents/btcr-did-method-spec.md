# BTCR DID Method Specification

There is a [Collaborative working URL](https://docs.google.com/document/d/15HWtXTDXcvyUjgAqnewPoZKbgSWhl-XiIDas1ip94Hs/edit), at Google Docs.

## abstract

## introduction

### background

### motivation

### purpose

## Method syntax

### name: "btcr"

### specific-idstring component

  Bitcoin public address

### btcr paths

None.  (unless use instead of fragment)

### btcr fragments

### when output index is required

### length considerations

#### P2PKH
#### P2WSH

### example BTCR Method-Specific DIDs

    DID did:btcr:123…
    key to check did:btcr:123…#1

## DDOs

### inferred - background on

for details, see section on reading DDO, below

### stored

### linking to external stored

#### ipfs

#### sia

### example stored DDO

## DID Operations for btcr
 
### create: btcr DID creation

#### meaning of first conforming transaction

#### tracing the chain for valid outputs

#### example generation from bitcoind

### read: btcr DDO implicit read

#### valid context

#### proof of ownership

##### example

#### proof of control

##### orcontrol with timelocked last output, and override n-1 

###### recognition of compliant use of n-1 pattern

#### service endpoints

  see also endpoint authentication

##### bitcoind

##### discussion of SPV clients

##### discussion of block explorers

##### discussion of blockchain median time past

###### created

###### updated

##### interpretation of signature

#### code to generate

### update: btcr DDO update via new transaction

### revoke: btcr DID invalidation by spending the coin

## DID resolving for btcr

bitcoind CLI 

## Security Considerations

### attacks and their residual risks

*At least the following forms of attack MUST be considered: eavesdropping, replay, message insertion, deletion, modification, and man-in-the-middle.  Potential denial of service attacks MUST be identified as well.  If the protocol incorporates cryptographic protection mechanisms, it should be clearly indicated which portions of the data are protected and what the protections are (i.e., integrity only, confidentiality, and/or endpoint authentication, etc.).  Some indication should also be given to what sorts of attacks the cryptographic protection is susceptible.  Data which should be held secret (keying material, random seeds, etc.) should be clearly labeled. If the technology involves authentication, particularly user-host authentication, the security of the authentication method MUST be clearly specified.*

residual risks (such as the risks from compromise in a related protocol, incorrect implementation, or cipher) after threat mitigation has been deployed.

This section MUST provide integrity protection and update authentication for all operations required by Section 7 of this specification (DID Operations).

### Bitcoin infrastructure burden and DoS considerations

### endpoint authentication

#### bitcoind

#### SPV

#### block explorers

### unique assignment

2^167, etc.

## proving ownership of the DDO example

  ???

### resolving DDO 

### verification of ownership

## proving ownership of the control key

  ???

### background: signing with the address in Bitcoin

  and quantum-crypto considerations

### external DDOs may be signed

### C/R using nonce

#### creating the challenge

#### notes on channels

#### example verification using bitcoind CLI

### 9.2.3 Identity Owner Authentication and Verifiable Claims

# other sections from DID spec to incorporate into the outline

## 9.3 Authentication Service Endpoints
## 9.4 Non-Repudiation
## 9.5 Notification of DDO Changes
## 9.6 Key and Signature Expiration
## 9.7 Key Revocation and Recovery

# another other section from DID spec: 10. Privacy Considerations

## 10.1 Requirements of DID Method Specifications
## 10.2 Keep Personally-Identifiable Information (PII) Off-Ledger
## 10.3 DID Correlation Risks and Pseudonymous DIDs
## 10.4 DDO Correlation Risks
## 10.5 Herd Privacy

# Future Considerations

## Equivalence

## from DID spec: 11.4 Time Locks and DDO Recovery

Section 9.7 mentions one possible clever use of time locks to recover
control of a DID after a key compromise. The technique relies on an
ability to override the most recent update to a DDO with Proof of
Control applied by an earlier version of the DDO in order to defeat
the attacker.

This protection depends on adding a [time lock (see Bitcoin BIP
65)](https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki#Abstract)
to protect part of the transaction chain, enabling a Proof of Control
block to be used to recover control.

We plan to add support for time locks in a future version of this
specification.

## 11.5 Smart Signatures
