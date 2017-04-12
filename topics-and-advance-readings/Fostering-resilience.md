Fostering the resilience of an ecosystem of workers through regulated decentralized reputation
========================================================================
*Philippe Honigman, Klara Sok*

Our questions proposed for consideration to RwoT-Europe working groups relate to mechanisms of attribution and regulation of reputation within a peer-to-peer network. We suggest to anchor the discussion around the real-life use case described below.

### Cepa, a public organization for managerial workers
Cepa is a public organization whose purpose is to support and assist 3.5 millions managerial workers throughout their career. Cepa also helps companies to access the skills that they need, through hiring and competency development.

On average, Cepa's 500 field consultants engage with 120,000 workers every year, in personal, face-to-face meetings or on workshops. More than 1 million are in touch with Cepa every year via their website and their online job board. There is no (direct) cost involved ; consultants are paid out of a national budget, funded by taxes on managers' salaries.

### New challenges, new opportunities for managers
Managers have faced dramatic changes over the last 20 years. Firms have gradually moved from centralized, hierarchical organizations towards flatter structures and agile processes. The labor market has also evolved, in many ways less favorable with regard to the traditional position of manager: remote working, freelancing, fragmentation of employment at multiple companies, outsourcing using software-powered coordination, etc.

Digital platforms and public social networks are increasingly being used by workers to find job opportunities, acquire new skills and expand their contacts. However platforms' purpose and governance are hardly compatible with the values and the mission of a public service.

### Sparking off a professional network for peer support
While Cepa consultants' assistance is consistently praised by the workers they interact with, their reach and their knowledge are limited. With the consultants' help, managers could engage with each other in order to develop their network, access new opportunities, learn about other jobs and sectors they might head to. The intended result would be to make professional careers more resilient and more fulfilling.

Hence the project of a public platform, designed and operated as a common, whose main goal would be to enable workers - and all the stakeholders of the working world - to help each other as a network of peers.

### Peer Interactions and Acknowledgement

Figure (a) describes the main agents and operations taking place in the network the platform:
![enter image description here](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/supporting-files/Fostering-1.png?raw=true)
*Figure (a) - agents and operations in the network*

At the heart of the system lies the interaction between managerial workers, shown here as a `connecting event`. Interactions can occur according to wide diversity of formats: online or offline, remotely or in person, between 2 people or in larger groups, etc. However, each format needs to be defined and activated by the `regulator` in order to be actionable in the economy of the network.

Once activated by the regulator, `catalysts` can instantiate a connecting event locally. Catalysts are independent agents that are authorized to organize an event, according to the rules defined by the regulator.
An event will connect at least one `giving worker` and one `receiving worker`. `Giving` or `receiving` are roles, thus the same person may be in turn giving or receiving on the same event.

During or after the event, receiving workers may provide a feedback about their experience and acknowledge the value received from the giving worker. This value is accumulated as `reputation` by the giving worker.

### Central regulation, decentralized reputation flow

The initial project is carried out as an Cepa's initiative. In this first phase :
-	catalysts are Cepa consultants ;
-	the format of the connecting events is defined by Cepa ;
-	the rules governing how reputation is issued and handled are stated by Cepa ;
-	the evaluation process leading to the issuance of reputation is decentralized.

Each worker is free to acknowledge the value received from any of her peers through a connecting event. Resulting reputation may be made available to third-parties, without depending on Cepa's policy nor availability of their information system. Managers' reputation is considered as an attribute of their self-sovereign identities. While acquiring reputation requires to play by the rules defined by Cepa as the regulator of the network, workers are to be empowered to use it as they see fit.

### From central authority to decentralized governance

In the initial phase, the network could display similarities with hybrid system such as SingularDTV, which defines itself as a "centrally organized, distributed entity".

As the sole regulator of the network, Cepa controls its operations by naming and revoking catalysts, defining the rules of engagement associated to connecting events, and establishing how reputation can be acquired and depreciated over time.

Cepa's public mandate confers legitimacy on the project among workers. As its main sponsor, Cepa also brings to the table the financial and human resources needed to kick off the service. However, once the model proven through successful experiments, governance may be opened to other stakeholders. The professional, reputational network will functions then as a common, that no single organization can single-handedly control.

![enter image description here](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/supporting-files/Fostering-2.png?raw=true)
*Figure (b) - two layers of decentralization*

### Incentivization through tokenized reputation

The purpose of the proposed system is not to create a market of services between workers, but to encourage peer support. Hence incentives cannot rely on direct monetization of peer services ; they should be symbolic rather than monetary. Tokenized reputation can be used to that effect.

In addition to materialize peers' gratitude and acknowledgement, quantified representation of workers' reputation may be used by individuals and organizations to access - otherwise hidden - pools of expertise.

### From acknowledgement to reputation

Previous initiatives such as the Portable Reputation Toolkit apprehend reputation as the result of a verification process of one's claims. In the proposed system, reputation isn't about checking the truthfulness of a given assertion ; it is defined as a function of aggregated acknowledgements resulting from a regulated interaction between 2 agents.

There is no claim to be verified, nor truth to be established about them. Peers are offered the possibility to express their subjective perception of the value delivered through the interaction. Those evaluations are aggregated and processed according to the rules defined by the regulator, in order to be eventually accounted as one's reputation. Here are a few examples of possible rules:

-    evaluations are only null (i.e. neutral) or positive
-    evaluations are weighed according to the evaluator's reputation
-    evaluations are weighed according to the nature of the connecting event, for instance, physical meetings may yield more reputation than online interactions
-    reputation depreciates by 20% per year
### Desirable properties for reputation
Noah Thorpe and Harlan T Wood have suggested which properties a reputation currency should offer: 

-    Verifiable - Reputation is issued by an identity to another identity. Public and private keys are well suited to this.
-    Portable - Reputation can be moved from system to system with minimal friction. Portability increases the value of reputation.
-    Non-forgeable - Like currency, the account of the reputation issuer and receiver must be securely controlled.
-    Uniform - A uniform format is necessary for consistent assessment, discovery and aggregation.
-    Timestamped - Reputation claims may be correlated with other events. The order of multiple reputation claims from entity A to B matters.
-    Summable - To make decisions one must be able to aggregate and assess multiple claims about the same identity.
-    Unique - This summing should not double count copies of the same reputation claim. Reputation increases in usefulness with copying, but copies of the same reputation should not be mistaken for multiple endorsements.
-    Durable - Reputation should outlast individual enterprises and technological changes.

It's worth noting that the reputation network introduced here does require the same set of properties - especially when decentralized governance will be introduced.

In addition, we would like to suggest some properties that may be deemed as necessary with respect to our use case:

-    Obfuscable - (or selectively disclosable) Reputation is a sensitive personal information that should only be exposed with the full consent of its owner.
-    Semantic - Professional reputation is highly contextual. Reputational data needs to be linkable to some classification, ontology or tagging system. 

### Open questions for RWoT-Europe 2017 working group
The Cepa use case leads to the following challenges proposed for consideration by Rebooting-the-Web-of-Trust Working Group: 

1.    Enabling agents to **obfuscate their reputational attributes**, while ensuring that both the identity of each worker and her reputation history are verifiable.
    The core purpose of the system is not to generate reputation ; it is to make it easier for professionals to seek, find and offer valuable help to their peers.
	Reputation is a by-product, that may prove extremely useful, and extremely sensitive as well. Hence its disclosure shouldn't be imposed by the system. A member should be able to hide or disclose her reputation as she sees fits.	
	On the other hand, when disclosed to 3rd parties, one's reputation should be (cryptographically) verifiable.

2.    Modelling a web of trust scheme that allows for **verifiable**, **dynamic** and **upgradable** computation of reputation (smart contract architecture).
     Verifiability refers to the ability to independently trace the history of signed evaluations that serves as the raw material for computing reputation.
     Dynamic concerns the application of rules for computing reputation, out of past evaluations and according to consensus-based decisions among regulators. For instance, such rules may determine the rate of depreciation of reputation over time, or weight higher evaluations that take place in the same physical location.
     Upgradability relates to the ability to change the rules of the system, including the way rules can be changed. When smart contract are to be used for dynamic processing of reputation, keeping the community of regulators in control of the system requires an instrument for "meta-governance".

3.    Discussing the **social acceptability** of different forms of evaluation in a professional environment.
	Decentralized evaluations are not necessarily desirable in every circumstance. While some form of social rating (reddit, Stack Overflow, github, etc) do not seem to raise many objections, some others are highly controversial or induce complex strategies to cheat the system.
	We would like to discuss how different factors might influence the way evaluation is perceived in the context of a web of trust: formats of evaluation and reputation data, transparence vs. obfuscation of evaluation data, etc.

### Some related work
-  [On Privacy-Preserving Identity within Future Blockchain Systems](https://www.w3.org/2016/04/blockchain-workshop/interest/hardjono-pentland.html)
-  [Privacy-ABC Technologies, Personal Data Ecosystem, and Business Models](https://abc4trust.eu/download/R2.1%20-%20PDE%20and%20ABC%20Review%20V1.0.pdf)
-  [Portable Reputation Toolkit](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/topics-and-advance-readings/portable-reputation-toolkit.md)
- [Social Credit System](https://en.wikipedia.org/wiki/Social_Credit_System)
