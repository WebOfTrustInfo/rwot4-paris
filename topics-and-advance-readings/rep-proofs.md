# Reputation proofs

by Dmitry Khovratovich (Evernym, Inc.)

Reputation is a well known concept historically applied to humans, organizations, and goods. 
The Internet made possible to make a reputational statement by anyone on almost every object in the web,
 from people (Linkedin) to hotels (TripAdvisor).

Whereas it is tempting to implement reputation on top of any identity system, a number of issues arise. 
The privacy problem is a major one: I may not want to disclose my recommendations in public, nor I want to show everyone who endorsed me, unless in private.

In this article we explore possible ways to create and present proofs of reputation, 
which provide limited and owner-controlled information about reputation. We restrict to human beings 
only as we are primarily concerned with linkage between reputation and identity. First we identify 
some properties of reputation that are relevant to our study.

 * Source and destination. A reputation grade is given by one identity (reputer) to another one (reputee).
 * Value. Grades can be positive or negative, though some systems prohibit negative grades (e.g. Facebook). It can also be 0-1 (vouched or not) or more precise, with a range of possible grades issued by the reputer. 
 * Aggregation. The grades are either aggregated into a single reputation value or considered separately.
 * Transitivity. The reputation may be a mere combination of grades given by reputers, or having this sum weighted accordingly to the current reputation of reputers.
 * Context. Grade is given to a certain skill or property of the identity.
 * Timing. Grades are accompanied with timestamps or not.
 * Fading. Timestamps are taken into account when counting the aggregate value or not.


## Reputation privacy requirements

Given the reputation properties, the following privacy requirements may arise:

* Confidentiality of sources. Alice does not reveal who endorsed her.
* Confidentiality of reputees. Alice does not reveal whom she recommended.
* Grade secrecy. Bob reveals who endorsed him but does not disclose the grades.
* Timing secrecy. Bob hides when exactly he was endorsed by Alice.
* Context secrecy. Carol hides what she was endorsed for by Bob.

## Reputation proofs

Given these requirements we envision the following proofs to be valuable to the users.

### Examples

1. Bob proves that he has been recommended as a cooker by at least 10 people.
2. Alice proves that she has been recommended as a software developer in the last 6 months.
3. Carol proves that the weighted aggregated reputation over the last 6 months is at least 100.

All the examples are zero-knowledge proofs in the sense that nothing more than truthness of a statement
 is revealed during the proof presentation to the verifier (and thus to an external observer).

### Proof format

We suggest the following approach to create proof schemas. A proof schema should include the 
following details to encompass the examples above:

* Proof subject, i.e. the identity whose reputation is in the statement. Can be a DID or another identificator.
* Proof predicate, i.e. a logical statement about the reputation of the user, his connections, and their grades, that can be evaluated.

Certain mathematical techniques admit quite powerful predicate proofs, but they are usually limited 
to a conjunction of simple arithmetic statements. To support more advanced predicates, we propose a two-layer tree format, where

* The first layer is the root;
* The second layer consists of leaves;
* Every leaf is a function of (grade, timestamp, context, source, destination);
* The root contains a boolean function of the leaf functions.

A pair (subject, predicate, signature_of_A) certifies that A knows an injective mapping from the set of 
all grades given to or by the proof subject  -- to the leaves of the tree such that the root function returns TRUE.



### Proof construction

Various techniques have been proposed over the last 20 years to create a reputation accumulation system with some privacy support. 
These include:

* Trusted servers of the organization that collects reputation data and publishes some proofs. Example: Linkedin.
* Trusted third-party organization that collects the reputation grades and publishes proofs at  user consent.
* Multiple-issuer system where each issuer is able to produce reputation proofs of himself or other users, and these proofs can be 
made unlinkable.
* Decentralized system where reputation is similar to coin supply, and privacy is provided by 
mechanisms similar to that in cryptocurrencies.

## Future work

We are looking for feedback from RWoT attendees on the following topics:

* New and more sophisticated examples of reputation proofs;
* Comments on schema format;
* Competing proposals from other organizations.

