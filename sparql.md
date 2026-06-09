---
layout: default
title: 🔍 SPARQL Queries
---

### 🌐 Navigazione: [🏠 Home](index.html) | [📂 Topic](topic.html) | [⚙️ Metodologia](methodology.html) | **🔍 SPARQL** | [🤖 Prompts](prompts.html) | [💎 RDF](rdf.html) | [🏁 Conclusioni](conclusion.html)

# 🔍 SPARQL Queries

---

This section hosts the queries used to evaluate the digital footprint of the **Basilica of San Petronio** (Bologna) within the **ArCo knowledge graph**, mapping out the data gaps identified during our research.

## 🛠️ Query Keywords

| Phase | Keyword / Operator | Functional Action on Data |
| :---: | :--- | :--- |
| **01** | `DISTINCT` | **Cleans** ➔ Removes all duplicate rows from the final graph output. |
| **02** | `FILTER`    | **Restricts** ➔ Enforces explicit logical constraints, keeping only the resources that satisfy our search conditions. |
| **03** | `REGEX`     | **Matches** ➔ Evaluates text strings using advanced pattern-matching, allowing for case-insensitive and flexible keyword searches. |
| **04** | `OPTIONAL` | **Adapts** ➔ Fetches extra details safely, ignoring missing values. |
| **05** | `UNION`    | **Combines** ➔ Merges multiple alternative search paths together. |
| **06** | `ORDER BY` | **Organizes** ➔ Sorts the final results into a clean alphanumeric order. |
| **07** | `LIMIT`    | **Limits** ➔ Caps the output entries to keep the web page fast. |


## 🔎 Step 1: Mapping the Baseline – Graph Discovery

Before mapping any data extensions, it was essential to verify whether the **Basilica of San Petronio** was already recognized as an active semantic entity within national cultural open data, and to pinpoint its official taxonomic indexing.

To achieve this, we executed a discovery script filtering the graph for our target monument:

```sparql
PREFIX cis: [http://dati.beniculturali.it/cis/](http://dati.beniculturali.it/cis/)
PREFIX rdfs: [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#)

SELECT DISTINCT ?site ?label
WHERE {
  ?site a cis:CulturalInstituteOrSite ;
        rdfs:label ?label .

  FILTER(REGEX(LCASE(STR(?label)), "san petronio"))
}

### 🧩 Query Breakdown: How It Works

Let's break this query down into simple pieces:

**1. SELECT DISTINCT ?site ?label**
* **What it shows:** This tells the database to display only two columns in our final results: the link of the monument (?site) and its name (?label). The word DISTINCT makes sure we do not get the same result repeated.

**2. ?site a cis:CulturalInstituteOrSite**
* **Where it looks:** The letter "a" means "is a type of". This line forces the query to look only inside the category of real physical monuments and cultural sites, skipping unrelated artworks.

**3. rdfs:label ?label**
* **What it matches:** This pulls the official text name or title of the monument from the database.

**4. FILTER(REGEX(LCASE(STR(?label)), "san petronio"))**
* **How it searches:** This is our search engine. It does three quick steps:
  * It turns the data into normal text.
  * It converts all letters to lowercase.
  * It looks for the words "san petronio".
* **Why we do this:** It finds the basilica even if it was written with different capital letters (like "San Petronio", "san petronio", or "SAN PETRONIO").
