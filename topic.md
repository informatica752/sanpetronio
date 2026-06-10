---
layout: default
title: 📂 Topic
---

# 📂 Topic & Research Domain

## 🏛️ General Characteristics of the Basilica di San Petronio
Located in the heart of [Piazza Maggiore](https://it.wikipedia.org/wiki/Piazza_Maggiore), the **[Basilica di San Petronio](https://it.wikipedia.org/wiki/Basilica_di_San_Petronio)** is the most iconic and dominant religious monument in [Bologna](https://it.wikipedia.org/wiki/Bologna). It is the world's largest brick [Gothic church](https://it.wikipedia.org/wiki/Gotico_italiano) and stands as a unique monument to civic pride, having been commissioned by the municipality rather than the bishops. 

Begun in [1390](https://it.wikipedia.org/wiki/1390) under the direction of [Antonio di Vincenzo](https://it.wikipedia.org/wiki/Antonio_di_Vincenzo), the basilica is globally renowned for its imposing, uniquely unfinished facade—split horizontally between beautiful marble carvings at the bottom and raw brickwork at the top. Inside, it houses invaluable cultural treasures, including the world's longest indoor meridian line (designed by [Gian Domenico Cassini in 1655](https://magazine.unibo.it/it/articoli/giovanni-domenico-cassini-e-la-nascita-della-meridiana-piu-lunga-del-mondo-a-bologna)) and magnificent masterpieces of Italian Gothic and [Renaissance art](https://it.wikipedia.org/wiki/Rinascimento).

---

## 🎯 Why We Chose This Project

Our research topic is born out of a shared academic journey and a surprising discovery. As students in Bologna, the Basilica di San Petronio is a daily presence in our academic and personal lives. However, our group brings a dual regional perspective: while studying in [Emilia-Romagna](https://it.wikipedia.org/wiki/Emilia-Romagna), **three of our team members come from [Tuscany](https://it.wikipedia.org/wiki/Toscana)**.

This specific cross-regional background naturally led us to compare the monuments of our respective regions. In Tuscany, prominent medieval monuments—most notably the **[Basilica di San Francesco](https://it.wikipedia.org/wiki/Basilica_di_San_Francesco_(Arezzo))**—benefit from incredibly rich digital documentation. We initially assumed that a monument of San Petronio's caliber would have a similarly robust representation in national cultural frameworks.

### The Element of Surprise on ArCo
Our project truly began when we queried **[ArCo](https://dati.beniculturali.it/arco/index.php)**, the official knowledge graph of the Italian Ministry of Culture. To our genuine astonishment, we found a staggering data asymmetry:
* **The San Francesco Benchmark:** The Basilica di San Francesco features a deeply nested, dense network of Linked Open Data, meticulously mapping its architectural history, internal chapels, artistic commissions, and structural evolutions over the centuries.
* **The San Petronio Blank Slate:** Despite its massive physical and historical weight, San Petronio exists on ArCo almost entirely as an "empty shell." It contains basic registry stubs but completely lacks detailed metadata, semantic properties, and granular historical connections.

This deep semantic gap motivated us to take action. This project is our attempt to use modern Semantic Web technologies and AI to give the Basilica di San Petronio the digital depth it deserves.

---

## 📊 Semantic Gap Analysis

To visually contextualize the scale of this data disparity, the table below highlights the conceptual density of the current national linked data structure before our intervention:

| Basilica Entity | Geographic Context | Presence in ArCo | Graph Density & Detail Level | Target Ontologies Connected |
| :--- | :--- | :---: | :---: | :---: |
| **San Francesco** | Tuscany | ✅ Yes | 🔴 High (Rich metadata, interconnected sub-entities) | ArCo, FOAF, CIDOC-CRM |
| **San Petronio** | Emilia-Romagna | ✅ Yes | ⚪ Extremely Low (Basic stub/registry data only) | Minimal / Basic ArCo |

By leveraging the deep relational structure of the Basilica di San Francesco as our structural blueprint, our methodology aims to extract, model, and inject the missing historical and architectural knowledge into a newly engineered, independent Knowledge Graph dedicated to San Petronio.
---

### 🏠 [Torna alla Homepage](index.html)
