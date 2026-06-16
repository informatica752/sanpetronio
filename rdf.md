---
layout: default
title: 💎 RDF Triples
---

# 💎 RDF Triples

```turtle
@prefix ex: [http://example.org/](http://example.org/) .
```

The content that follows presents the **RDF triples** produced to complete the missing elements identified earlier.

## 3. RDF Triples for Geographical Coordinates

📍 We prompted ChatGPT to generate an RDF triple for the latitude using a **few-shot prompting approach**, providing a reference example to define the expected structure and format.

<img width="365" height="310" alt="image" src="https://github.com/user-attachments/assets/2f36bb30-12be-4e3a-bbcc-446a6c13ca18" />

### ➡️ ChatGPT output:

```turtle
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    geo:lat "44.29346" .
```

#### Longitude generation

Next, we applied the same approach to generate the longitude value (11.343126° E), changing only the predicate to geo:long.

➡️ **Resulting RDF triple**:

```turtle
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    geo:long "11.343126" .
```

#### Merging latitude and longitude

We then requested the integration of both values into a single RDF description. This was achieved by combining multiple predicates under the same subject using Turtle shorthand syntax.

➡️ **Merged RDF representation**:

```turtle
@prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .

<http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
    geo:lat "44.29346" ;
    geo:long "11.343126" .
```
### Final ArCo classification step

Finally, we introduced the ArCo namespace prefix and added an explicit type declaration (a arco:CulturalInstituteOrSite) to semantically classify the resource within the ArCo ontology.

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

