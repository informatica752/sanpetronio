---
layout: default
title: "Basilica di San Petronio"
---

### Explore the Project

<div style="display: flex; flex-wrap: wrap; gap: 10px; margin-top: 15px; margin-bottom: 20px;">
  <a href="index.html" style="background-color: #f8f9fa; color: #0056b3; padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; display: inline-block; border: 1px solid #e1e4e8; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">🏠 Home</a>
  <a href="topic.html" style="background-color: #f8f9fa; color: #0056b3; padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; display: inline-block; border: 1px solid #e1e4e8; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">📂 Topic</a>
  <a href="methodology.html" style="background-color: #f8f9fa; color: #0056b3; padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; display: inline-block; border: 1px solid #e1e4e8; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">⚙️ Methodology</a>
  <a href="sparql.html" style="background-color: #f8f9fa; color: #0056b3; padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; display: inline-block; border: 1px solid #e1e4e8; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">🔍 SPARQL Queries</a>
  <a href="prompt.html" style="background-color: #f8f9fa; color: #0056b3; padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; display: inline-block; border: 1px solid #e1e4e8; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">💻 LLM Prompts</a>
  <a href="rdf.html" style="background-color: #f8f9fa; color: #0056b3; padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; display: inline-block; border: 1px solid #e1e4e8; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">🔗 RDF Triples</a>
  <a href="conclusion.html" style="background-color: #f8f9fa; color: #0056b3; padding: 10px 18px; border-radius: 6px; text-decoration: none; font-weight: bold; display: inline-block; border: 1px solid #e1e4e8; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">🏁 Conclusion</a>
</div>

# Home

<img width="1200" height="675" alt="Basilica-di-San-Petronio-1" src="https://github.com/user-attachments/assets/b3bea0e0-26aa-4bac-b197-509f297a8de7" />


### Explore the Project
* **[🏠 Home](index.html)**
* **[📂 Topic](topic.html)**
* **[⚙️ Methodology](methodology.html)**
* **[🔍 SPARQL Queries](sparql.html)**
* **[💻 LLM Prompts](prompts.html)**
* **[🔗 RDF Triples](rdf.html)**
* **[🏁 Conclusion](conclusion.html)**


# About the Project

This project was carried out as part of the **KE4H (Knowledge Engineering for the Humanities)** course at the [University of Bologna](https://www.unibo.it/it). 

Our research centers on the **[Basilica di San Petronio di Bologna](https://it.wikipedia.org/wiki/Basilica_di_San_Petronio)**, one of the city's most deeply significant landmarks and one of the largest churches in the world. Despite its immense historical, architectural, and cultural value, we discovered that this monumental basilica is only partially documented within **[ArCo](https://dati.beniculturali.it/arco/index.php)**, the official [knowledge graph](https://en.wikipedia.org/wiki/Knowledge_graph) of Italian Cultural Heritage.

The goal of our study was to analyze how the Basilica di San Petronio is modeled in ArCo, pinpoint any missing data or structural gaps, and propose semantic enhancements. To accomplish this, we integrated advanced **[SPARQL querying](https://en.wikipedia.org/wiki/SPARQL)** with **[Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model)** to generate new RDF triples aligned with [ArCo's official ontology](http://wit.istc.cnr.it/arco/lode/extract?lang=en&url=https://raw.githubusercontent.com/ICCD-MiBACT/ArCo/master/ArCo-release/ontologie/arco/arco.owl).

Ultimately, this work investigates how AI-driven assistants can optimize the representation of cultural heritage within structured datasets, overcoming existing data gaps and making cultural knowledge more accessible.

## Key Objectives

* 🔍 **Analyze** the current representation of the Basilica di San Petronio within the ArCo dataset.
* 📍 **Identify Gaps** in the existing data, such as missing geographical coordinates, architectural details, images, and metadata.
* 🧠 **Experiment** with various LLM prompting techniques (including Zero-Shot, Few-Shot, and Chain-of-Thought) for accurate RDF generation.
* 🛠️ **Enrich the Dataset** by producing valid RDF triples using AI-based assistants compliant with ArCo's schema.
* 📊 **Evaluate** the effectiveness and impact of incorporating LLMs into knowledge engineering workflows for cultural heritage.

## Tools Used

* **[ArCo Ontology](http://wit.istc.cnr.it/arco/lode/extract?lang=en&url=https://raw.githubusercontent.com/ICCD-MiBACT/ArCo/master/ArCo-release/ontologie/arco/arco.owl)& [SPARQL Endpoint](https://en.wikipedia.org/wiki/SPARQL)** with **[Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model)** (Data retrieval & modeling)
* **[ChatGPT](https://chat.openai.com/), [Gemini](https://gemini.google.com/?hl=it)** (LLM testing & triple generation) & **[Claude](https://claude.com/)**
* **[GitHub](https://github.com/)** (Project hosting & version control)

## Our Team

This project was collaboratively developed by:

* 👱🏼‍♀️ **Sofia Giorgetti**
* 👩🏻 **Francesca Cianciosi**
* 👩🏻 **Giulia Nestola**
* 👩🏻 **Martina Fierli**

Students of the Master’s Degree in [Language, Society and Communication](https://corsi.unibo.it/2cycle/LanguageSocietyCommunication) at the University of Bologna.

