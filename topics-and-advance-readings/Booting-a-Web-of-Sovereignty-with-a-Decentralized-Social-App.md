# Booting a Web of Sovereignty with a Decentralized Social App
_By: Adam Lake_

Building and growing a decentralized peer-to-peer (P2P) and self sovereign Web application capable of becoming a prominent social media app might be the moonshot project most suited to kickstarting a Web of trust and “redecentralize” the Web. It would not only be an extreme success for a more user-centric social network to scale, but would be a shining example of how we could organize to create alternatives to other tech monopolies as well. Success may be improbable but the upsides are so great that it’s worth the risk. 

The fullness of “sovereign identity” is not likely to be realized with a single approach to all domains for identity on the Web. A P2P social media platform is a good focused use case to discuss self sovereign identity. Perhaps we can arrive at a sovereign identity solution for this single app. 

The dominant networking platform is a paper tiger. There is no real value they provide besides the network effect and some software that can be replaced. Replacing the software and growing a network are not at all trivial, but tech monopolies may be far more vulnerable to a mission-driven challenger than one might initially think. There is already an appetite for alternatives and growing wariness around data concentration and mining. 

While we can market this project it will only succeed if there are enough people who sufficiency care about the issues this alternative addresses. It is difficult to determine if that critical mass exists. That being said, we have a responsibility to build the technology that embodies these values so we’re ready if and when the required cultural shift takes place. The public may already have the desire but lack the technology and awareness. A user centric P2P platform may grow quickly or very slowly like the Web did at first and then hit a tipping point. One thing we know for sure, it’s not as possible without the proper technology. 

A web of trust also needs organizational models other than the predominant profit-centric model that governs all large tech companies. Whether it be a non-profit foundation, a social benefit corporation, a cooperative, or something else, we need to couple these technologies with organizational models that have symbiotic governing principles.  

I am including business plan elements to hopefully inspire the reader to believe that supplanting social media monopolies with a P2P models is more than remotely possible. However, I would like to focus RWoT time on nailing down the core technical framework for a decentralized self sovereign social network. 
### Problems with Social Media Monopolies 

* They engage in comprehensive and growing data collection on billions of users and as they grow, so will central ownership of the social graph and our digital selves.
* This data allows for exponentially greater manipulation of human beings and their realities than ever seen before. The social media monopolies may or may not be malicious, but power concentration is always a threat to a free society and centralized systems can more easily be taken over by nefarious actors.
* Systemic risk is highest in centralized systems.
* A prominent tech CEO recently stated in his “Manifesto” that he wants his social network  to essentially create and control the social infrastructure for the entire planet
* Projecting trends, social media monopolies will become a systemic risk center for a free society.

The algorithms that social media monopolies use to populate their newsfeeds are not accessible to the users and so users have no way of knowing the ways in which the information they see is being filtered. These profit-centric corporations have the tools to measure, interpret, and manipulate the political preference of these users.  In the wrong hands this could be used as a massive propaganda machine and to tip elections. It’s inherently a threat to a democratic and free society. 
## Solutions
### Previous Attempts
Many have understood the need to create a more self sovereign P2P social media platform and a several have tried. Decent example are [Diaspora](https://en.wikipedia.org/wiki/Diaspora_(social_network)) and [Mastodon](https://mastodon.social/about). Both of these fall short of a being robust social media platform that has a good chance of longevity in that they rely on the success of the “pod” on which users register to maintain their social connections. If the pod fails a user’s profile and social connections are lost. They can build a new profile on a new pod and try to relocate all of their friends and other social connections, but it would be a painful process. And after all that they would be left in a similar position of relying on the stability of the new pod they joined. Users are also stuck with a pod host that begins to act unethically, like overcharging them for hosting. This is not user centric, it’s pod-host centric. It breaks down central control into many authorities but the power is not sufficiently in the hands of the individual user. There have been other attempts at developing a user-centric social media platform but they fall short of “self sovereign” in other ways. 

These are the primary technical requirements to produce a truly self sovereign P2P social media platform with the best chances of producing a self sovereign social media platform that can supplant one or more of the tech monopolies.
#### Personal Server/Storage 
Each user having their own personal server allows for speed and liveliness that social media users have come to expect. This server can be outsourced as a service or located in a home or office. 

While some argue that this is a burdensome requirement, that a P2P social media platform should be able to run on a user's device, the device approach means that either data is not always live and can’t be accessed at all times, or that there is data replication across the network. This seems unacceptable and won’t meet the standards of most prospective users. 

**Existing projects/solutions**: [Nextcloud](https://nextcloud.com), [Sandstorm](https://sandstorm.io/)

#### User Owned Data Decoupled from Apps

“Users should have the freedom to choose where their data resides and who is allowed to access it by decoupling content from the application itself.”

“Because applications are decoupled from the data they produce, users will be able to avoid vendor lock-in by seamlessly switching the apps and personal data storage servers, without losing any data or social connections.”

“Developers will be able to easily innovate by creating new apps or improving current apps, all while reusing existing data that was created by other apps.”

**Existing project/solution**: [Solid](https://solid.mit.edu/)

#### Portable (URI migration) Identity 
If a user's identifier is a URI then designing for URI migration will increase the chances that the social network persists over time. Because users can migrate their URI’s they are not dependant on a specific URL, a subdomain, or an identifier on a blockchain. Users will be able to migrate from one identifier to another.

**Access Control Lists:**
The only approach I currently know that might accomplish this is [access control lists](https://en.wikipedia.org/wiki/Access_control_list). It’s a simple but robust idea that each user in the network has a list/address book of URIs, one for each social contact. The contact URI is a file that can be changed by the user it points to. It would work as follows:
1.    User 1 requests to make a connection with user 2.
2.    User 2 accepts.
3.    User 1 and 2 store each others URI in their URI Contact List.
4.    During the exchange each user is asked if they want to give the other user access to the directory of their contact list where the other users URI is stored. (E.g., User 1 is asked if they want to give User 2 write access to the directory where user 2’s URI is stored on User 1’s URI contact list. And visa versa.
5.    They both accept and now have the ability to update their URI in all of the Contact Lists that they have been approved to modify. Only those that can prove ownership of the original URI can update all the connected Contact Lists. This is analog to filling out a change of address form, but it happens digitally and almost instantly. 
![enter image description here](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/supporting-files/fig1-alake.png?raw=true)

Projects and approaches to the Identity problem, none of which are portable as far as I know

* [Sovrin](https://www.sovrin.org/): an non-profit blockchain based permissioned identity ledger
* An open public proof of work identity ledger, for all identity purposes or specific to the app. 
* [Namecoin](https://namecoin.org/) without the coin
* [WebID](https://en.wikipedia.org/wiki/WebID)
* [IPFS](https://ipfs.io/), Interplanetary File System  

### Other Features

* **Custom News Feed Algorithms**: customizable algorithms for news feed such that users can swap out news feed algorithms. 
* **Fine-grained News Feed Filtering**: filtering of feed/notifications by different sorting categories such as geography, group, organization, date, person. 
* **Open source**: the social media platform will be open source

### Organizational and Business Model 

A non-profit foundation could be formed to maintain the open source software the network runs on.

An additional social enterprise and/or cooperative business could be started to host user pods at cost, as well as offer freemium accounts. A partnership with a tasteful advertising company would be required to cover the expenses of the free hosted accounts. Users can always upgrade to a no-ad option or migrate to another host if they choose. It’s an open garden. 

Any hosting company can host a person’s personal server. This means there is competition, which will drive prices down. It also means that the network can scale very quickly by taking advantage of unutilized server capacity in much the same way that AirBnB takes advantage of underutilized housing. 
### Growth Strategy, Community Sites 

Community sites are smaller networks within the larger P2P network and are for loose groups of users, affinity groups, or more formal organizations. They could be built on variety of open source software like elgg, Drupal, buddyPress and others as long as they conform to the decentralized application’s standards. Community sites are essential to scaling the network as they make the network immediately useful to those who are part of such communities rather than requiring a large threshold of friends to join the network before it becomes useful. 
### Marketing/Funding 

Initial seed funding is required to:

* Flesh out a business plan for the entire project 
* Organize a group of people, organizations, and public figures to publicize and donate to the upcoming crowdfunding campaign    
* Launch and manage the crowdfunding campaign to create the MVP. 

**Seed funding: 40K-120K**

I’ve heard varying quotes with regards to the funding required to build and launch an MVP that offers the core features and that could eventually provide equivalent functionality to popular social networks. 

**MVP funding: 200K-20M** 

All together now! There are many people and organizations that care about the issues that this project would address. If we can raise the funds and attract the required talent we have a decent chance of succeeding. Some stakeholders that come to mind are Tim Berners-Lee,  Internet Archive, Mozilla, CTA, Web Foundation, national governments (especially outside the US). There are many other stakeholder that may support this effort. 

The technology and capabilities required to pull off a decentralized social network are represented at RWoT and other affiliated meetups. There is great potential in the communities that care about decentralizing the Web, Self Sovereign Identity and the like. This community can produce a compelling decentralized social network. 
### Questions

* Will a network of servers more quickly aggregate data for a user's feed than a network of devices? 
* How to deal with hate speech and terrorism? How can you stop a bad actor from broadcasting their message to followers? Do we even want to stop it, is it worth the cost? 
* How are we going to deal with fake news?
* Who will the advertising partner be? Can Google refuse to allow us to use google ads? 
* How do we deliver on portable identity?
* Are there any insurmountable reasons a decentralized social network can not be achieved? What issues are there with this model?
* Will nation states be able to interrupt a decentralized model like this? Could they block all traffic associated with the app? 


I know it’s a longshot, but a worthy one considering the upsides of success. If this succeeds it would further open the door to new models replacing other tech monopolies. I welcome your feedback.
