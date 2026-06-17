---
layout: default
title: 💎 RDF Triples
---

# 💎 RDF Triples


### What are RDF Triples used for?
In the traditional web, pages are linked together, but computers don't understand what the text inside them actually means. **RDF Triples solve this problem by giving meaning to data.** They allow search engines, AI models, and applications to automatically connect different pieces of information, cross-reference data from different websites (like linking Wikipedia with museum archives), and run complex smart searches instead of just looking for simple keywords.

### How they work
To do this, RDF Triples connect information using a basic three-word statement: **Subject - Predicate - Object**. 

### Our Goal
The goal of this section is to produce structured semantic data designed to fill specific information gaps identified on the official **ArCo (Architecture of Knowledge)** portal regarding the Basilica of San Petronio. Instead of processing a pre-written description, we took the data provided by **ChatGPT** to resolve these gaps and asked the model to **generate** corresponding formal RDF triples.

To find the most accurate and compliant data layout for ArCo's standards, we tested the model using three different prompting strategies: **Zero-Shot**, **Few-Shot**, and **Chain-of-Thought (CoT)**. 

The content that follows presents the **RDF triples** produced to complete the missing elements identified during the previous LLMs investigation.

## 1. RDF Triple for description 📝

Using a **zero-shot** prompting technique, we asked ChatGPT to create a RDF Triple:
 <img width="802" height="1248" alt="image" src="https://github.com/user-attachments/assets/ef8c6e62-43a8-43a9-8ede-0b0e9cd6097b" />

We gave ChatGPT the following information to generate the RDF triple:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `l0:description` | The Gothic basilica of San Petronio in Bologna (…) in pre-modern Europe. |

➡️ **Result:**
```turtle
@prefix l0: <https://w3id.org/italia/onto/l0/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    l0:description """The Gothic basilica of San Petronio in Bologna, dominating the southern side of Piazza Maggiore, represents one of the most ambitious expressions of late medieval civic architecture in Italy and an emblematic monument of the city's communal identity. Conceived in 1390 as a grandiose project to rival the major cathedrals of Christendom, its unfinished façade partly clad in pink and white marble and partly left in exposed brick visibly reflects the interrupted evolution of its construction and the historical tensions between civic and ecclesiastical power that shaped its long development.

The vast interior, articulated by a solemn succession of towering piers and pointed arches, preserves the austere spatial clarity typical of Italian Gothic architecture, while also hosting an extraordinary stratification of artistic interventions spanning from the Middle Ages to the Baroque period. Among its most significant decorative cycles, the Chapel of the Magi (Bolognini Chapel) stands out for the vivid frescoes attributed to Giovanni da Modena, which include one of the most striking medieval visualizations of the Inferno from Dante Alighieri's Divine Comedy, where monumental and densely populated scenes unfold with expressive intensity and narrative richness.

Particularly notable within the basilica is the monumental meridian line traced on the floor of the nave by Giovanni Domenico Cassini in 1655, an extraordinary scientific instrument embedded in sacred space. This precise astronomical device, aligned with the sun's movement, allowed for refined measurements of the solar year and constitutes a rare synthesis of scientific inquiry and religious architecture, emblematic of Bologna's historic role as a center of learning. The basilica also preserves important sculptural and pictorial testimonies, including chapels enriched with Renaissance and late medieval frescoes, devotional altarpieces, and architectural elements that reflect the continuous adaptation of the building across centuries. Its complex stratigraphy, combining unfinished monumental ambition with layered artistic contributions, makes San Petronio not only a place of worship but also a fundamental reference point for the study of Gothic architecture, urban identity, and the dialogue between art, science, and civic power in pre-modern Europe."""@en .
```

## 2. RDF Triple for wikidata link 🔗
Through a **zero-shot** prompt, ChatGPT generated the RDF triples to connect the Basilica with its relative wikidata link:
<img width="1160" height="384" alt="image" src="https://github.com/user-attachments/assets/a9022cd1-620e-42ad-93ae-7ad3be2141e0" />

We gave ChatGPT the following information to generate the RDF triple:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `owl:sameAs` | <http://www.wikidata.org/entity/Q810103> |

➡️ **Result:**
```turtle
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix arco: <https://w3id.org/arco/ontology/core/> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    rdfs:label "Basilica di San Petronio, Bologna"@it ;
    owl:sameAs <http://www.wikidata.org/entity/Q810103> 
```
## 3. RDF Triples for Geographical Coordinates 📍

We prompted ChatGPT to generate an RDF triple for the latitude using a **few-shot prompting approach**, providing a reference example to define the expected structure and format.

#### Latitude generation
<img width="365" height="310" alt="image" src="https://github.com/user-attachments/assets/2f36bb30-12be-4e3a-bbcc-446a6c13ca18" />

We leveraged ChatGPT to transform the following details into an RDF triple:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `geo:lat` | 44.29346 |
 
➡️ **Result:**

```turtle
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    geo:lat "44.29346" .
```

#### Longitude generation

Next, we asked Chat GPT to apply the same approach to generate the longitude value (11.343126° E), changing only the predicate to `geo:long`.

<img width="372" height="83" alt="image" src="https://github.com/user-attachments/assets/48755750-30a9-4f27-97e5-56a83e80ddde" />

The RDF triple was generated via ChatGPT using the following input data:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `geo:long` | 11.343126 |

➡️ **Result:**

```turtle
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    geo:long "11.343126" .
```

#### Merging latitude and longitude

We then requested the integration of both values into a single RDF description. This was achieved by combining multiple predicates under the same subject using Turtle shorthand syntax.

<img width="403" height="58" alt="image" src="https://github.com/user-attachments/assets/921bc009-77c0-4db5-bab8-79db7324d2d1" />

➡️ **Merged RDF representation**:

```turtle
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    geo:lat "44.29346" ;
    geo:long "11.343126" .
```
### Final ArCo classification step

Finally, we introduced the ArCo namespace prefix and manually added an explicit type declaration (`a arco:CulturalInstituteOrSite`) to semantically classify the resource within the ArCo ontology.

This step enriches the RDF description by defining not only the coordinates but also the ontological nature of the entity.

➡️ **Final RDF triple**:

```turtle
@prefix arco: <https://w3id.org/arco/ontology/arco/> .
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    a arco:CulturalInstituteOrSite ;
    geo:lat "44.29346" ;
    geo:long "11.343126" .
```
## 4. RDF for official image 📷

The ArCo ontology employs different properties to reference images depending on their status. For official images, it uses `arco:hasRepresentativeImage`, whereas for non-official images, it relies on `foaf:depiction`.

Based on our previous research, there is currently no designated official image for the Basilica di San Petronio. Furthermore, when tasked with finding one, Gemini and ChatGPT provided completely different images, each identifying their respective choice as the most representative. 

➡️ Given this lack of official standardization, we have chosen to use the `foaf:depiction` predicate to attach our image.

<img width="481" height="109" alt="image" src="https://github.com/user-attachments/assets/87b2d1f6-83f0-4d40-87e0-c46b6b3b6f9a" />

Below the specifications used to ask Chat GPT to provide us the RDF triple:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `foaf:depiction` | URL of the image found on [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Basilica_di_San_Petronio_-_Bologna.jpg)|

In order to interrogate Chat GPT we used the *zero shot prompting technique*

<img width="420" height="211" alt="image" src="https://github.com/user-attachments/assets/6b8fd63a-2f09-4cbb-9bd5-287b7b64c5cc" />

➡️ **Result:** 

```turtle
@prefix arco: <https://w3id.org/arco/ontology/arco/> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    a arco:CulturalInstituteOrSite ;
    foaf:depiction <https://commons.wikimedia.org/wiki/Special:FilePath/Basilica_di_San_Petronio_-_Bologna.jpg> .
```
## 5. RDF for entrance ticket 🎟️
Using a **zero-shot** prompting technique, we asked ChatGPT to create a RDF Triple to link all information about the entrance ticket to the Basilica of San Petronio:

<img width="631" height="337" alt="image" src="https://github.com/user-attachments/assets/b547c625-be0f-4ccf-96d1-53ae4bae5f3b" />

The RDF triple was generated via ChatGPT using the following input data:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `potapit:hasTicket` | all ticket information |

➡️ **Result:**
```turtle
@prefix potapit: <http://dati.beniculturali.it/lod/potapit/> .
@prefix l0: <http://dati.beniculturali.it/lod/l0/> .
@prefix sm: <http://www.ontologydesignpatterns.org/cp/owl/simplemetadata.owl#> .
@prefix arco: <http://dati.beniculturali.it/lod/arco/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<https://dati.beniculturali.it/lodview/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio.html>
    rdf:type arco:CulturalInstituteOrSite ;

    potapit:hasTicket <https://example.org/ticket/BasilicaSanPetronio_FreeEntry> ,
                      <https://example.org/ticket/BasilicaSanPetronio_ChapelRoute_FullTicket> ,
                      <https://example.org/ticket/BasilicaSanPetronio_ChapelRoute_ReducedTicket> ,
                      <https://example.org/ticket/BasilicaSanPetronio_ChapelRoute_SchoolTicket> ,
                      <https://example.org/ticket/BasilicaSanPetronio_IndividualChapelVisit> .

<https://example.org/ticket/BasilicaSanPetronio_FreeEntry>
    rdf:type potapit:Ticket ;
    l0:name "Free Entry - Main Basilica and Museum Access" ;
    sm:price "0 EUR" .

<https://example.org/ticket/BasilicaSanPetronio_ChapelRoute_FullTicket>
    rdf:type potapit:Ticket ;
    l0:name "Chapel Route - Full Ticket (Re Magi, San Sebastiano, San Vincenzo Ferrer)" ;
    sm:price "5 EUR" .

<https://example.org/ticket/BasilicaSanPetronio_ChapelRoute_ReducedTicket>
    rdf:type potapit:Ticket ;
    l0:name "Chapel Route - Reduced Ticket (students 11–18, over 65, guided groups)" ;
    sm:price "3 EUR" .

<https://example.org/ticket/BasilicaSanPetronio_ChapelRoute_SchoolTicket>
    rdf:type potapit:Ticket ;
    l0:name "Chapel Route - School Groups Ticket" ;
    sm:price "2 EUR" .

<https://example.org/ticket/BasilicaSanPetronio_IndividualChapelVisit>
    rdf:type potapit:Ticket ;
    l0:name "Individual Chapel or Presbytery Visit (on reservation)" ;
    sm:price "3 EUR per chapel" .
```

## 6. RDF for contact information 📞
In order to add the missing information about contact details to the ArCo Knowledge Graph, we decided to use the **chain-of-thought** prompting technique. Forcing the model to reason step-by-step ensures it plans the graph structure first, correctly mapping every office to its own unique URI and generating flawless, hallucination-free RDF code as shown below:

<img width="661" height="507" alt="image" src="https://github.com/user-attachments/assets/d0a6420c-1831-42cd-87ef-0a3efa79bb6c" />

We gave ChatGPT the following information to generate the RDF triple:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `smapit:hasOnlineContactPoint` | all contact information |

➡️ **Result:**
<img width="667" height="401" alt="image" src="https://github.com/user-attachments/assets/e49100e4-9513-4666-b2d2-35ce7c27cfa5" />

```turtle
@prefix arco:   <https://w3id.org/arco/ontology/arco/> .
@prefix smapit: <https://w3id.org/italia/onto/SM/> .
@prefix l0:     <https://w3id.org/italia/onto/l0/> .
@prefix rdf:    <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<https://dati.beniculturali.it/lodview/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio.html>
    a arco:CulturalInstituteOrSite ; 
    smapit:hasOnlineContactPoint <http://example.org/contact/phone_general> ,
                                 <http://example.org/contact/phone_archive> ,
                                 <http://example.org/contact/email_info> ,
                                 <http://example.org/contact/email_prenotazioni> ,
                                 <http://example.org/contact/email_sacrestia> ,
                                 <http://example.org/contact/email_archivio_storico> ,
                                 <http://example.org/contact/email_archivio_musicale> ,
                                 <http://example.org/contact/website> .

<http://example.org/contact/phone_general>
    a smapit:OnlineContactPoint ;
    l0:name "General Information / Sacristy Phone" ;
    smapit:telephone "+39 051 231415" .

<http://example.org/contact/phone_archive>
    a smapit:OnlineContactPoint ;
    l0:name "Historical Archive Phone" ;
    smapit:telephone "+39 348 4414917" .

<http://example.org/contact/email_info>
    a smapit:OnlineContactPoint ;
    l0:name "General Information Email" ;
    smapit:email "info@basilicadisanpetronio.org" .

<http://example.org/contact/email_prenotazioni>
    a smapit:OnlineContactPoint ;
    l0:name "Group Visits and Bookings Email" ;
    smapit:email "prenotazioni@basilicadisanpetronio.org" .

<http://example.org/contact/email_sacrestia>
    a smapit:OnlineContactPoint ;
    l0:name "Sacristy Email (Liturgical Services)" ;
    smapit:email "sacrestia@basilicadisanpetronio.org" .

<http://example.org/contact/email_archivio_storico>
    a smapit:OnlineContactPoint ;
    l0:name "Historical Archive Email" ;
    smapit:email "archivio.storico@basilicadisanpetronio.org" .

<http://example.org/contact/email_archivio_musicale>
    a smapit:OnlineContactPoint ;
    l0:name "Musical Archive Email" ;
    smapit:email "archivio.musicale@basilicadisanpetronio.org" .

<http://example.org/contact/website>
    a smapit:OnlineContactPoint ;
    l0:name "Official Website" ;
    smapit:webSite "https://www.basilicadisanpetronio.org" .
```
