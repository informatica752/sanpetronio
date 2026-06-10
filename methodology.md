---
layout: default
title: ⚙️ Methodology
---

**To systematically address the lack of data for San Petronio on ArCo, our group executed the following operational phases step by step:** 

### 🌐 1. Choosing the Subject & Initial Analysis
Our project focuses on the **[Basilica of San Petronio](https://it.wikipedia.org/wiki/Basilica_di_San_Petronio)** in Bologna, an incredible historical and architectural masterpiece. Our main goal was to check how well this famous monument is preserved in digital archives, see what information was already available online, and find a way to enrich its digital records.

### 🔍 2. Checking ArCo’s Database
To see how San Petronio is represented in Italy's official cultural heritage data, we did a thorough check by querying the official **[ArCo SPARQL endpoint](https://dati.cultura.gov.it/sparql)**. This allowed us to explore exactly what information, details, and connections were already linked to the Basilica inside the national knowledge graph.

### 📊 3. Comparing Landmarks & Finding Data Gaps
To get a clear picture of what was missing, we compared San Petronio's data with other major Italian churches. Since three of our team members are from Tuscany, we used the **[Basilica of San Francesco in Arezzo](https://it.wikipedia.org/wiki/Basilica_di_San_Francesco_(Arezzo))** as our main comparison point. While San Francesco had a beautiful, super-detailed network of connected data, San Petronio turned out to be almost completely empty, showing a huge difference in data quality.

### 🕵️ 4. Confirming the Gaps with SPARQL
We didn't just stop at our first impression; we proved it technically. By writing and running targeted **SPARQL queries**, we got concrete, machine-readable proof that vital pieces of information—like historical details, timeline updates, and specific architectural connections for San Petronio—were completely missing from ArCo.

### 💡 5. Using LLMs to Find Missing Data
To fill these data gaps, we brought Generative AI into our workflow. We experimented with different prompting techniques (**Zero-Shot, Few-Shot, and Chain-of-Thought**) using **[ChatGPT](https://it.wikipedia.org/wiki/ChatGPT)and [Gemini AI](https://it.wikipedia.org/wiki/Gemini_(modello_linguistico))**. This helped us guide the AI assistants to extract accurate, high-quality historical facts about the Basilica.

### ⚖️ 6. Fact-Checking & Quality Control
Since AI models can sometimes make things up, we put the results from ChatGPT and Gemini through a strict cross-validation process. We double-checked all the historical facts against trusted academic sources, filtered out any mistakes or "hallucinations," and combined the best answers into one fully verified dataset.

### 📚 7. Writing the Code & Creating RDF Triples
Next, we translated our newly verified historical text into machine-readable data for the Semantic Web. We mapped this information onto ArCo’s official structure to generate valid **[RDF triples](https://en.wikipedia.org/wiki/Semantic_triple#See_also)** and exported them into a **[Turtle (.ttl)](https://it.wikipedia.org/wiki/Turtle_(formato))** file, creating a real, ready-to-use extension for the knowledge graph.

### 🖥️ 8. Launching the Web Platform on GitHub
To share our work with everyone, we built this **[GitHub Pages web platform](https://en.wikipedia.org/wiki/GitHub)** website. This platform hosts our entire step-by-step process, displays our comparison results, and serves as an open-science project to show how AI can help researchers enrich and update cultural heritage databases.

---
## **What Role Do These Tools Play?**


## 🏛️ Cultural Knowledge Sources: ArCo & ArCo SPARQL Endpoint
To establish a baseline for our project, we interacted extensively with national cultural heritage platforms:

* **What is ArCo?** [ArCo](https://dati.beniculturali.it/arco/index.php) (Architecture of Knowledge) is the official [Knowledge Graph](https://it.wikipedia.org/wiki/Knowledge_graph) of the [Italian Ministry of Culture](https://it.wikipedia.org/wiki/Ministero_della_cultura). It exposes millions of cultural assets as [Linked Open Data (LOD)](https://en.wikipedia.org/wiki/Linked_data), standardizing information about monuments, historical events, and artistic creators across Italy.
* **The SPARQL Endpoint:** A SPARQL Endpoint is a dedicated web interface that allows human researchers and automated software agents to query a Knowledge Graph using the SPARQL query language. By querying the ArCo endpoint, we empirically verified the massive data asymmetry: San Francesco returned a dense web of interconnected entities, while San Petronio returned only a basic registry stub.

---

## 🔀 Data Formalization: RDF Triples
As highlighted in our course materials, the fundamental building block of the [Semantic Web](https://it.wikipedia.org/wiki/Web_semantico) is the **[RDF (Resource Description Framework)](https://it.wikipedia.org/wiki/Resource_Description_Framework)** standard. 

Instead of organizing data in traditional relational tables or isolated text blocks, RDF models knowledge as a directed graph. Every piece of information is broken down into a formal **RDF Triple**:

**Subject** $\rightarrow$ **Predicate** $\rightarrow$ **Object**
* **Subject:** The resource being described (represented by a unique URI, e.g., `ex:Basilica_San_Petronio`).
* **Predicate:** The formal property or relationship (e.g., `ex:hasArchitect`).
* **Object:** The value or another interconnected resource (e.g., `ex:Antonio_di_Vincenzo`).

By adopting this structure, we shift from a "Web of Documents" (meant only for human eyes) to a "Web of Data" (where machines can logically infer connections between concepts).

---

## 🤖 Computational Processing: LLMs & AI Ingestion
To accelerate the creation of the missing triples for San Petronio without manually coding thousands of lines, we introduced **LLMs (Large Language Models)** into the data pipeline.

### Role of LLMs in Semantic Web
LLMs act as intelligent translation layers. When properly instructed, they can parse complex natural language narratives (such as historical books or architectural surveys) and isolate core semantic entities and relationships.

### Models Selected for this Research
To guarantee high syntactical accuracy and lower hallucination rates, we benchmarked and deployed the following state-of-the-art models:
* **[GPT-4o (OpenAI)](https://chat.openai.com/):** Utilized for its exceptional compliance with complex JSON-LD and Turtle structural syntax constraints.
* **[Gemini (Google)](https://gemini.google.com/?hl=it):** Deployed for its superior contextual understanding of long historical texts and nuanced architectural vocabulary.

The models were explicitly restricted through system prompts to only map relations that could be grounded in verified academic inputs.

---

## 📦 Infrastructure & Deployment: GitHub & GitHub Pages
The entire development, tracking, and publishing lifecycle of this project is hosted on **[GitHub](https://github.com/)**.

* **GitHub as a Version Control System:** It allows our team to collaborate simultaneously on the text, prompt configurations, and raw `.ttl` (Turtle) data files, ensuring a transparent history of every change made to the Knowledge Graph.
* **GitHub Pages Integration:** By using GitHub Pages combined with the native Jekyll framework, we converted our project's underlying Markdown documentation into this live, navigable, and responsive web portal under the **[Cayman Theme](https://github.com/pages-themes/cayman)** framework.

---

### 🏠 [Torna alla Homepage](index.html)
