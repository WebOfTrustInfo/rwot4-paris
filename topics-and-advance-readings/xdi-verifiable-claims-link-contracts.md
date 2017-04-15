XDI Verifiable Claims and Link Contracts
========================================
Markus Sabadello, Danube Tech (https://danubetech.com), Vienna, April 15th 2017

There is a high level of interest in the Rebooting-the-Web-of-Trust community and beyond in "verifiable claims", i.e. "a cryptographically non-repudiable set of statements made by an entity about another entity" (see **[1]**). This work foresees that "the next generation of web applications will authorize entities to perform actions based on rich sets of credentials issued by trusted parties" (see **[2]**).

XDI (eXtensible Data Interchange) is a technology for modeling, storing and sharing personal and organizational identity data. One key component of this technology is the "link contract", i.e. a "data sharing agreement between the publisher of the data, called the authorizing authority, and a party who wants to access the data, called the requesting authority" (see **[3]**).

XDI link contracts contain a policy tree which is used to decide if the permissions granted by the link contract can be invoked by a requesting authority. This policy evaluates conditions based on input elements such as the authorizing authority, requesting authority, and an incoming request message. Simple conditions of the policy could e.g. require the presentation of a valid password or signature. 

This topic paper explores the use of verifiable claims as part of an XDI link contract's policy. This way, an XDI link contract could grant permissions to a requesting authority only if it is able to present a certain verifiable claim.

XDI Verifiable Claims
---------------------

While the larger verifiable claims community at the moment may be unlikely to base its work on the XDI graph model, the concept of verifiable claims itself should be understood to be abstract and independent of any concrete technological realization. In other words, "the data model should be data syntax agnostic" (see **[4]**).

A claim as an assertion of the value of an attribute of a subject (see **[5]**) can be represented as a simple XDI statement (in this case, an XDI "relational" statement):

	=!:did:sov:21tD/$is#/#doctor

The fact that the subject of the claim is also the claimant, i.e. it is the subject itself making the assertion, can be represented using an XDI peer root:

	(=!:did:sov:21tD)=!:did:sov:21tD/$is#/#doctor

Expressing that the claimant is different from the subject could also be done using an XDI peer root: 

	(+!:did:sov:QQiF)=!:did:sov:21tD/$is#/#doctor

In order to express that the assertion is made specifically within the context of the relationship between claimant and subject, an XDI inner root can be used:

	(+!:did:sov:QQiF/=!:did:sov:21tD)=!:did:sov:21tD/$is#/#doctor

To make the claim "verifiable", an XDI signature and other data such as a timestamp are added:

	(+!:did:sov:QQiF/=!:did:sov:21tD)=!:did:sov:21tD/$is#/#doctor
	(+!:did:sov:QQiF/=!:did:sov:21tD)<$sig>/&/"R0wdp.....Y5w=="
	(+!:did:sov:QQiF/=!:did:sov:21tD)<$sig>/$is#/$sha$256$rsa$2048
	(+!:did:sov:QQiF/=!:did:sov:21tD)<$sig><$t>/&/"2017-04-13T05:14:38Z"

XDI Link Contracts
------------------

An XDI link contract with a policy that grants permissions if a certain verifiable claim is presented could look like this:

	(+hospital/#doctor)$contract$do/$add/+hospital[#patient]
	(+hospital/#doctor)($contract$do$if$and/$true){$msg}<$sig><$valid>/&/true
	(+hospital/#doctor)($contract$do$if$and/$true)(+!:did:sov:QQiF/{$from}){$from}/$is#/#doctor
	(+hospital/#doctor)($contract$do$if$and/$true)(+!:did:sov:QQiF/{$from})<$sig><$valid>/&/true

Note that the variable `{$from}` stands for the requesting authority that is using the link contract.

Issuing XDI Verifiable Claims
-----------------------------

Using XDI, a verifiable claim could be "issued" by requesting an assertion to be signed by a claimant (issuer), using the XDI `$do$sign` operation:

	=!:did:sov:21tD[$msg]@~0/$from/(=!:did:sov:21tD)
	=!:did:sov:21tD[$msg]@~0/$to/(+!:did:sov:QQiF)
	=!:did:sov:21tD[$msg]@~0/$contract/(+!:did:sov:QQiF/=!:did:sov:21tD)$contract
	(=!:did:sov:21tD[$msg]@~0$do/$do$sign)(+!:did:sov:QQiF/=!:did:sov:21tD)=!:did:sov:21tD/$is#/#doctor

Response:

	+!:did:sov:QQiF[$msg]@~0/$from/(+!:did:sov:QQiF)
	+!:did:sov:QQiF[$msg]@~0/$to/(=!:did:sov:21tD)
	+!:did:sov:QQiF[$msg]@~0/$is$msg/=!:did:sov:21tD[$msg]@~0
	(+!:did:sov:QQiF[$msg]@~0/$do$sign)(+!:did:sov:QQiF/=!:did:sov:21tD)=!:did:sov:21tD/$is#/#doctor
	(+!:did:sov:QQiF[$msg]@~0/$do$sign)(+!:did:sov:QQiF/=!:did:sov:21tD)<$sig>/&/"R0wdp.....Y5w=="
	(+!:did:sov:QQiF[$msg]@~0/$do$sign)(+!:did:sov:QQiF/=!:did:sov:21tD)<$sig>/$is#/$sha$256$rsa$2048
	(+!:did:sov:QQiF[$msg]@~0/$do$sign)(+!:did:sov:QQiF/=!:did:sov:21tD)<$sig><$t>/&/"2017-04-13T05:14:38Z"

The response contains the XDI verifiable claim as described earlier in this document.

Note that the issuing request also requires an XDI link contract in order to be authorized and executed. This can enable scenarios where a certain verifiable claim is required by an XDI link contract as a condition for another verifiable claim to be issued. 

Additional Notes
----------------

DIDs (see **[6]**) in this document are abbreviated and "XDIified" (see **[7]**)-

XDI examples in this document use the "XDI DISPLAY" format. Conversion to other formats such as "JXD" is possible (see **[8]**). 

XDI cryptographic signatures are currently specifically designed for XDI's unique hierarchical graph model. It will be interesting to explore if there are potential synergies with the ongoing effort to align signature formats (see **[9]**). 

Related Work
------------

Previous XDI-related contributions to RWoT include: 

 * XDI, Blockstore, and BIP32: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/cool-hack-xdi-blockstore-bip32.md
 * XDI Link Contracts: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/xdi-link-contracts.md
 * XDI Graphs in IPFS: https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/topics-and-advance-readings/XDI-Graphs-in-IPFS.md
 * JXD Examples: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/topics-and-advance-readings/JXD-Examples.md

Thank you to the wonderful RWoT community for its great and idealistic work! 

References
----------

 **[1]** http://w3c.github.io/vctf/#verifiable-claim

 **[2]** https://opencreds.github.io/vc-use-cases/

 **[3]** https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/xdi-link-contracts.md

 **[4]** https://docs.google.com/document/d/1tCKHSTFhhGgu4rVDJe4VM2QoCQcNRvx7tNku1Mg8p5Q/

 **[5]** http://wiki.idcommons.net/Claim

 **[6]** https://docs.google.com/document/d/1Z-9jX4PEWtyRFD5fEyyzEnWK_0ir0no1JJLuRu8O9Gs/

 **[7]** https://lists.oasis-open.org/archives/xdi/201611/msg00002.html

 **[8]** https://server.xdi2.org/XDIConverter

 **[9]** https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/SignatureFormatAlignment.md
