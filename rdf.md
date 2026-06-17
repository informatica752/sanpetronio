---
layout: default
title: 💎 RDF Triples
---

# 💎 RDF Triples

### What are RDF Triples used for?
In the traditional web, pages are linked together, but computers don't understand what the text inside them actually means. **RDF Triples solve this problem by giving meaning to data.** They allow search engines, AI models, and applications to automatically connect different pieces of information, cross-reference data from different websites (like linking Wikipedia with museum archives), and run complex smart searches instead of just looking for simple keywords.

### How they work
To do this, RDF Triples connect information using a basic three-word formula: **Subject --> Predicate --> Object** 

### Our Test
To see how well the models could transform regular text into this machine-readable format, we tested them using three different strategies: **Zero-Shot**, **Few-Shot**, and **Chain-of-Thought (CoT)** prompts. This approach allowed us to analyze the performance gap between the models, showing how they improve when moving from a direct request to a guided example, and finally to a step-by-step reasoning process.



```turtle
@prefix ex: [http://example.org/](http://example.org/) .
```

The content that follows presents the **RDF triples** produced to complete the missing elements identified earlier.

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

