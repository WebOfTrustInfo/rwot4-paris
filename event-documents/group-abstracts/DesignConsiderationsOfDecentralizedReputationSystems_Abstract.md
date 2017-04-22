# Design considerations of decentralized reputation systems #

_By_

_Angus Champion de Crespigny (anguschampion@gmail.com), Dmitry Khovratovich (khovratovich@gmail.com), Florent Blondeau (florent.blondeau@nameshield.net), Klara Sok (klarasok@gmail.com), Philippe Honigman (philh@ftopia.com), Nikolaos Alexopoulos (alexopoulos@tk.tu-darmstadt.de), Fabien Petitcolas (fabienpe@outlook.com), Shaun Conway (shaun@consent.global)_

Reputation is a common topic and key component of the future web of trust. While there have been numerous analyses of how reputation may be used, there has to date been no systematic definition of the various aspects of a reputation system that should be considered when they are being designed. By defining these design considerations, we can come to a consensus on what is and isn’t important in a system, what are the different ways in which they can be built, and conduct further research and analysis into specific factors in a structured way.

We identified 10 design considerations all decentralized reputations should address. These are:

1.	Context: what is the reputation value applicable to? What can be understood about an entity by seeing their reputation value(s)?
2.	Participation: how is it defined who can and can’t participate, and who can and can’t have a reputation value assigned?
3.	Consent: Is consent required by a user to issue claims or a reputation value against the user? Is consent required to reveal claims or a reputation value of a user?
4.	Obfuscation: To meet consent requirements, how is data that calculates a reputation value obfuscated? Can it be derived or is it perfectly information concealing?
5.	Value: How is the reputation value calculated? How are claims contributing to the reputation value normalized?
6.	Performance: How does the system manage the performance and behavior of the users? How does it manage the performance of the network for speed, reliability, and data integrity? How do users have confidence in this?
7.	Sustainability: How does the system stay relevant over time?
8.	Claim lifecycle: How are claims valued over time? Can they be revoked, and under what conditions?
9.	Resilience: How does the system protect against attacks that reduce the integrity of the reputation value?
10.	Legal: What is the legal environment in which the system sits? Are there potential violations of ‘natural’ law?

We have defined each, and populated each with examples and considerations for their design. We will continue to develop and refine to establish language standards for discussing reputation systems. 
We have not defined what is and isn’t required in each, as particular implementations may have differing reasons for each. However, best practices for these considerations we anticipate being topics for future analysis.
