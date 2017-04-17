# DID Names

*Drummond Reed & James Monaghan, 2017-04-15, Rebooting the Web of Trust #4, Paris, France*

# Introduction

The DID (decentralized identifier) specification, partially developed at previous RWOT events and funded in part by the U.S. Department of Homeland Security, has become a defacto standard for establishing interoperable self-sovereign digital identity. See the [DID Data Model and Generic Syntax 1.0 specification](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/did-implementer-draft-10.pdf) for more information.

However, as explained in section 1.4 of the DID spec, DIDs are not human-friendly identifiers:

> **1.4 The Role of Human-Friendly Identifiers**

> DIDs achieve global uniqueness without the need for a central registration authority. This comes, however, at the cost of human memorability. The algorithms capable of generating globally unique identifiers automatically produce random strings of characters that have no human meaning. This leads to the axiom about identifiers known as [Zooko’s Triangle](https://en.wikipedia.org/wiki/Zooko%27s_triangle): "human-meaningful, decentralized, secure—pick any two".

> There are of course many use cases where it is desirable to discover a DID starting from a human-friendly identifier—a natural language name, a domain name, or a conventional address for a DID owner, such as a mobile telephone number, email address, Twitter handle, blog URL, etc. However, the problem of mapping human-friendly identifiers to DIDs (and doing so in a way that can be verified and trusted) is out-of-scope for this specification. 

Section 1.4 goes on to make specific recommendations about specifications that will tackle the problem of mapping human-friendly identifiers to DIDs:

> Solutions to this problem (and there are many) should be defined in separate specifications that reference this specification. It is strongly recommended that such specifications carefully consider: (a) the numerous security attacks based on deceiving users about the true human-friendly identifier for a target entity, and (b) the privacy consequences of using human-friendly identifiers that are inherently correlatable, especially if they are globally unique.

Given the growing demand to map human-friendly names to DIDs, this document is a proposal to create a new specification called **DID Names**.

# The DID Names Specification

The basic concept of DID Names is that the specification would directly parallel the DID specification as shown in this table:

<table>
  <tr>
    <td><strong>Specification</strong></td>
    <td><strong>Scheme Name</strong></td>
    <td><strong>Maps From</strong></td>
    <td><strong>To</strong></td>
  </tr>
  <tr>
    <td>DID Names Specification</td>
    <td>id:</td>
    <td>DID Name
(human-friendly name string)</td>
    <td>DID</td>
  </tr>
  <tr>
    <td>DID Specification</td>
    <td>did:</td>
    <td>DID
(machine-friendly "number" string)</td>
    <td>DDO</td>
  </tr>
</table>


In other words, the DID Names specification would enable any compatible distributed ledger to map a human-friendly name string that begins with id: (a "DID name") to a DID the same way the DID specification enables any compatible distributed ledger to map a DID “number” that begins with did: to a DDO (DID descriptor object). From a technical standpoint, the only real difference is that a DID name would map directly to one and only one DID.

For example, the following DID name

```id:sov:alice```

would resolve directly to a DID such as:

```did:sov:8uQhQMGzWxR8vw5P3UWH1j```

Note that this DID happens to be in the same DID method space ("sov") as the DID name. That is not a requirement—a DID name could also resolve to a DID in a different method space. For example, the DID name id:sov:alice could resolve to:

```did:eth:33ad7beb-1abc-4a26-b892-466df4379a51```

(Note that this is a theoretical example—the ```did:eth:``` method has not yet been defined).

To simplify and align the work, it is proposed that the DID Names specification be written as an extension to the DID specification, i.e., rather than define a specific DID namespace, the DID Names specification would specify **what is required in order for a DID method specification to also specify how it will support DID names**. These requirements would include:

1. Defining the DID name syntax supported by the DID method spec.

2. Defining how to perform the CRUD operations on a DID name record.

3. Defining the policies governing the DID names in this DID method space.

Using this approach, each DID method can define everything necessary to manage a human-friendly DID namespace as well as a DID "numberspace".

# DID Method Spaces

Although mapping DID names to DIDs is technically very simple compared to mapping DIDs to DDOs (where all the complexity lies), the inherent value of human-friendly names means the complexity lies instead with **the design and governance of these new namespaces**—just as it has with DNS. 

In a DID name, the string between the first and second colon is called the **DID method space**. It is tempting to compare a DID method space to a DNS top-level domain (TLD). That analogy would suggest that a DID method space could be in very high demand (ICANN currently charges US$185,000 for a generic TLD (gTLD) application).

However this analogy is flawed for two reasons:

1. **DID method names are structural, not semantic, components.** Unlike DNS TLDs, DID methods are not just strings in a table. Each method name corresponds to code that knows how to implement DID name operations (create, read, update, delete) associated with that DID method.

2. **With DID names, semantic namespaces begin at the third level.** In the DID name id:sov:alice, for example, it is really "alice" that is the equivalent of a DNS TLD.

Since the whole purpose of decentralized identity infrastructure is to prevent centralization of control (and centralization of taxation), it is strongly recommended that the DID Names specification adopt the following policies:

1. **Only DID method specifications may define DID method spaces.** This naturally limits the number of DID method spaces and simplifies architecture by telling DID resolvers what method to use to resolve a DID name.

2. **Inside DID method spaces, DID names MUST be colon delimited.** This enables lower-level DID namespaces to be delegated using colon delimiters just like DNS namespaces are delegated using dot delimiters. See the examples below.

3. **Authority for DID namespaces MUST be delegated using DIDs.** Each DID name MUST map to a DID. The public key for that DID MUST be used to authorize registration of names in the next level namespace.

4. **DID method space designers should also design the economics of their DID namespace**, i.e., costs & policies for registrations, renewals, trademark protection, dispute resolution, etc. In this way market forces, not government or industry monopolies, will drive the costs of DID names.

# Examples

Following are fictitious examples of different DID method spaces and different levels of delegated DID names within them.

<table>
  <tr>
    <td><strong>DID Name</strong></td>
    <td><strong>Notes</strong></td>
  </tr>
  <tr>
    <td>id:sov:alice</td>
    <td>Personal name in Sovrin method space</td>
  </tr>
  <tr>
    <td>id:sov:alice:home</td>
    <td>Delegated namespace</td>
  </tr>
  <tr>
    <td>id:sov:alice:home:oven</td>
    <td>Delegated namespace (to a device)</td>
  </tr>
  <tr>
    <td>id:sov:microsoft</td>
    <td>Company name in Sovrin method space</td>
  </tr>
  <tr>
    <td>id:sov:microsoft:seattle</td>
    <td>Delegated company name</td>
  </tr>
  <tr>
    <td>id:btc:ibm</td>
    <td>Company name in Bitcoin method space</td>
  </tr>
  <tr>
    <td>id:uport:frank.zappa</td>
    <td>Personal name in uPort method space</td>
  </tr>
  <tr>
    <td>id:uport:frank.zappa:moon-unit</td>
    <td>Delegated personal name</td>
  </tr>
</table>


Note that the final two examples illustrate that dots and dashes should be valid characters in DID names—only colons are reserved characters for namespace delegation. DID names should also accept Unicode characters after the method space name.

# Next Steps

If there is sufficient interest, work on drafting a DID Names specification could beging at the Rebooting the Web of Trust #4 conference April 19-21 2017 in Paris and continue the Internet Identity Workshop May 2-4 2017 in Mountain View.

