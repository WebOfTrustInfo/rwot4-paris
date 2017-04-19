# Towards a user-centered web of trust
_Fabien Petitcolas, Paul Dunphy – Vasco Data Security_

A web of trust (WoT) is considered to be one way to construct trust in the absence of a cen-tral authority. However, despite a widespread presumption that WoT would underpin trust in a future world of decentralised computing, this approach still exhibits limitations that have existed from the first deployments of Pretty Good Privacy (PGP).
#### If it isn’t usable it isn’t secure
In her “7 flaws of identity management” [1], Dhamija’s explains that for users “identity management is not a primary goal. This has been reflected in the large adoption by users of centralised single-sign on solutions, suggesting that future identity management (IdM) schemes with a novel technological underpinning but developed to the same blueprint of end-user interaction are unlikely to create widespread uptake.

A principal tenet of human-computer interaction is to find new end-user problems that a system design can solve. So far, we have not seen schemes that are accompanied by a novel vision of user interaction.

#### Authentication and trust propagation
There are at least two key aspects that need to be done right. First, the authentication of the user, as this will give access the credentials that can open the doors of numerous ser-vices. The second is the ability of users to easily manage their identities (or keys) and assign some level of trust to other identities.

Despite the hype around them, the schemes based distributed ledger technology (DLT) that we have seen so far leave those perennial challenges largely unaddressed and focus on the core DLT implementation. Even for rather well established application such as Bitcoin, recent research has suggests that cryptographic key management remains to be a principal source of concern for users [2].

#### Leveraging social connections
When users accept connections on social media networks, they de-facto assign some level of trust on the connection presented to them. Social elements (stories, photos, discussions, common contacts, etc.) quickly confirm they have connected to the right person. As shown by the widespread use of social media networks, such models are very intuitive and obvious to use for most users. One important issue, though, is that the most widely used social me-dia networks rely on central authorities to make them work, but as shown by some small-scale initiative, this does not have to be the case.

#### Decentralised convergence
A natural consequence of those observations could be to use the model of social media networks as a basis for propagating trusted connections between users. To avoid relying on a central authority, and assuming that it is unlikely that users will run nodes of a P2P net-work on their computer, such model could rely on agent software, that is network end-points that are always available and that can act on behalf of users (the same concept as used by Sovrin). How would the architecture of such platforms look like?

As for the authentication of the users, we have slowly moved from login/password to two-factor authentication. The triad of what you know, hold, and are, is likely to go undis-turbed, but could distributed ledger technology bring new or contextual elements that could make the authentication process more robust? This goes from the authentication of the user on the device with which the user interacts, to maintaining the security of the iden-tity systems, to passing user credentials among multiple services.

### References
1.	Rachna Dhamija and Lisa Dusseault, ‘The Seven Flaws of Identity Management: Usabil-ity and Security Challenges’, IEEE Security Privacy, vol. 6, no. 2, pp. 24–29, Mar. 2008.
2.	Shayan Eskandari, David Barrera, Elizabeth Stobert, and Jeremy Clark, ‘A First Look at the Usability of Bitcoin Key Management’, presented at the Workshop on Usable Securi-ty (USEC), 2015.

