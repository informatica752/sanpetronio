---
layout: default
title: 💎 RDF Triples
---

# 💎 RDF Triples


### What are RDF Triples used for?
In the traditional web, pages are linked together, but computers don't understand what the text inside them actually means. **RDF Triples solve this problem by giving meaning to data.** They allow search engines, AI models, and applications to automatically connect different pieces of information, cross-reference data from different websites (like linking Wikipedia with museum archives), and run complex smart searches instead of just looking for simple keywords.

### How they work
To do this, RDF Triples connect information using a basic three-word formula: **Subject - Predicate - Object**. 

### Our Goal
The ultimate goal of this section is to produce structured semantic data designed to fill specific information gaps identified on the official **ArCo (Architecture of Knowledge)** portal regarding the Basilica. Instead of processing a pre-written description, we took the data provided by **ChatGPT** to resolve these gaps and asked the model to **generate** corresponding formal RDF triples.

To find the most accurate and compliant data layout for ArCo's standards, we tested the model using three different prompting strategies: **Zero-Shot**, **Few-Shot**, and **Chain-of-Thought (CoT)**. 

---
```turtle
@prefix ex: [http://example.org/](http://example.org/) .
```

The content that follows presents the **RDF triples** produced to complete the missing elements identified earlier.

## 1. RDF Triple for description
Using a zero-shot prompting technique, we asked ChatGPT to create a RDF Triple:

```turtle
@prefix l0: <https://w3id.org/italia/onto/l0/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    l0:description """The Gothic basilica of San Petronio in Bologna, dominating the southern side of Piazza Maggiore, represents one of the most ambitious expressions of late medieval civic architecture in Italy and an emblematic monument of the city's communal identity. Conceived in 1390 as a grandiose project to rival the major cathedrals of Christendom, its unfinished façade partly clad in pink and white marble and partly left in exposed brick visibly reflects the interrupted evolution of its construction and the historical tensions between civic and ecclesiastical power that shaped its long development.

The vast interior, articulated by a solemn succession of towering piers and pointed arches, preserves the austere spatial clarity typical of Italian Gothic architecture, while also hosting an extraordinary stratification of artistic interventions spanning from the Middle Ages to the Baroque period. Among its most significant decorative cycles, the Chapel of the Magi (Bolognini Chapel) stands out for the vivid frescoes attributed to Giovanni da Modena, which include one of the most striking medieval visualizations of the Inferno from Dante Alighieri's Divine Comedy, where monumental and densely populated scenes unfold with expressive intensity and narrative richness.

Particularly notable within the basilica is the monumental meridian line traced on the floor of the nave by Giovanni Domenico Cassini in 1655, an extraordinary scientific instrument embedded in sacred space. This precise astronomical device, aligned with the sun's movement, allowed for refined measurements of the solar year and constitutes a rare synthesis of scientific inquiry and religious architecture, emblematic of Bologna's historic role as a center of learning. The basilica also preserves important sculptural and pictorial testimonies, including chapels enriched with Renaissance and late medieval frescoes, devotional altarpieces, and architectural elements that reflect the continuous adaptation of the building across centuries. Its complex stratigraphy, combining unfinished monumental ambition with layered artistic contributions, makes San Petronio not only a place of worship but also a fundamental reference point for the study of Gothic architecture, urban identity, and the dialogue between art, science, and civic power in pre-modern Europe."""@en .
```
We gave ChatGPT the following information to generate the RDF triple:

Subject: Basilica di San Petronio, URI <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
Predicate: l0:description
Object: The Gothic basilica of San Petronio in Bologna (…) in pre-modern Europe.


## 3. RDF Triples for Geographical Coordinates

📍 We prompted ChatGPT to generate an RDF triple for the latitude using a **few-shot prompting approach**, providing a reference example to define the expected structure and format.

<img width="365" height="310" alt="image" src="https://github.com/user-attachments/assets/2f36bb30-12be-4e3a-bbcc-446a6c13ca18" />

### ➡️ ChatGPT output:

We leveraged ChatGPT to transform the following details into an RDF triple:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `geo:lat` | 44.29346 |

----
```turtle
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    geo:lat "44.29346" .
```
---

#### Longitude generation

Next, we asked Chat GPT to apply the same approach to generate the longitude value (11.343126° E), changing only the predicate to `geo:long`.

<img width="372" height="83" alt="image" src="https://github.com/user-attachments/assets/48755750-30a9-4f27-97e5-56a83e80ddde" />

➡️ **Resulting RDF triple**:

The RDF triple was generated via ChatGPT using the following input data:

| Subject | Predicate | Object |
| :--- | :--- | :--- |
| [Basilica di San Petronio in Bologna](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) | `geo:long` | 11.343126 |



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

