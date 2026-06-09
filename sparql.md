---
layout: default
title: 🔍 SPARQL Queries
---

### 🌐 Navigazione: [🏠 Home](index.html) | [📂 Topic](topic.html) | [⚙️ Metodologia](methodology.html) | **🔍 SPARQL** | [🤖 Prompts](prompts.html) | [💎 RDF](rdf.html) | [🏁 Conclusioni](conclusion.html)

# 🔍 SPARQL Queries

# 🏛️ SPARQL Queries

---

This section hosts the queries used to evaluate the digital footprint of the **Basilica of San Petronio** (Bologna) within the **ArCo knowledge graph**, mapping out the data gaps identified during our research.

## 🛠️ Query Keywords at a Glance

The diagram below maps out how our SPARQL keywords handle and clean data from the graph to the final output:

graph LR
    A[ArCo Graph Data] --> B(DISTINCT)
    B -->|Remove duplicates| C(FILTER & REGEX)
    C -->|Match specific text| D(OPTIONAL)
    D -->|Include missing data| E(UNION)
    E -->|Combine patterns| F(ORDER BY)
    F -->|Sort results| G(LIMIT)
    G -->|Restrict rows| H[Final Output Table]

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style H fill:#bbf,stroke:#333,stroke-width:2px
