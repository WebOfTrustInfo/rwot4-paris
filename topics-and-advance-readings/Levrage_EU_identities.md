# Distributed identities as a EU cross-border identity infrastructure
## by L. Boldrin  - InfoCert s.p.a.

Many EU countries have in place a national, government supported e-Identity infrastructure (see, e.g. https://www.government.nl/binaries/government/documents/reports/2015/05/13/international-comparison-eid-means/international-comparison-eid-means.pdf for a survey) with some regional differences (see, e.g, http://norden.diva-portal.org/smash/get/diva2:902133/FULLTEXT01.pdf for eID in nordic countries).

eIDAS Regulation (Regulation EU 910/2014) set up a framework upon which national “identity schemes” should be recognized all around Europe – at least for public services. This poses a set of issues related to the technical and operational implications of this requirement. The current approach, promoted by EU projects like STORK, STORK 2 and by the EU initiative “Connecting Europe Facilities” (CEF - https://ec.europa.eu/cefdigital/wiki/display/CEFDIGITAL/eID) goes through a set of “proxy nodes” disseminated in EU countries, which provide a eID sharing infrastructure. The schema is illustrated by the picture below, for the access to an UK bank from a user from Norway (from:  http://oixuk.org/wp-content/uploads/2017/01/Alpha-Digital-Identity-Across-Borders-FINAL-December-2016.pdf)

The complete picture is presented in  https://ec.europa.eu/cefdigital/wiki/download/attachments/23003182/JS4%20Building%20Block%20DSI_IntroDocument%20%28eID%29-v1.05.pdf?version=1&modificationDate=1490615634087&api=v2, which provides some more detail on the eIDAS nodes and the flows they implement.
 
While the concept proved to work, there are many concerns as to the practical scalability of this approach as well as its possible adoption by the commercial sector.  One of the major issues is the absence of useful identifiers – an identifier is included among the core set of attributes transported by the eIDAS infrastructure (see https://ec.europa.eu/futurium/en/system/files/ged/celex_32015r1501_en_txt.pdf) but it is is specific to the country of origin: 
The unique identifier consists of: 

   1. The first part is the Nationality Code of the identifier. 
This is one of the ISO 3166-1 alpha-2 codes, followed by a slash (“/“)) 

   2. The second part is the Nationality Code of the destination country or international organization.
This is one of the ISO 3166-1 alpha-2 codes, followed by a slash (“/“) 

   3. The third part a combination of readable characters.
This uniquely identifies the identity asserted in the country of origin but does not necessarily reveal any discernible correspondence with the subject's actual identifier (for example, username, fiscal number etc) 

Example: ES/AT/02635542Y (Spanish eIDNumber for an Austrian SP)
(from: [https://ec.europa.eu/cefdigital/wiki/display/CEFDIGITAL/eID+eIDAS+profile?preview=/23003348/35218928/eIDAS%20SAML%20Attribute%20Profile%20v1.1_2.pdf](https://ec.europa.eu/cefdigital/wiki/display/CEFDIGITAL/eID+eIDAS+profile?preview=/23003348/35218928/eIDAS%20SAML%20Attribute%20Profile%20v1.1_2.pdf))

We believe there is room for alternative eID exchange frameworks, which complement (and may eventually replace) the proxy approach, especially for the commercial sector. The distributed identity paradigm may well fit this role, in two ways: 

   *	At minimum, a self-sovereign identifier could be included on request of the identity owner as an  information in the cross-border exchanges. Proxies may have  a role here in enriching the basic information from the national eID infrastructure with the supplementary identifier, with no impact on the existing national infrastructure (which are normally strongly regulated). The counterpart proxy could then propagate this identifier (if the calling service  has the capability to deal with it) or discard it.

   *	On a larger perspective, eIDAS attributes provided by national identity schemas (directly, or through eIDAS nodes) could be derived into identity claims, through an intermediary which acts as a “claim broker”:
 
In this scenario the production of identity information and its usage would be neatly separated by  the derivation process.

Leveraging on existing national infrastructures may provide the initial boot for reaching a critical mass.
As a migration path, private actors running eIDAS nodes could parallel the “standard” node with a claim provider, and  offer the user the choice.


