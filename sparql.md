---
layout: default
title: 🔍 SPARQL Queries
---

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
```

### Query Breakdown: How It Works

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

<img width="1915" height="562" alt="sparql basilica petronio " src="https://github.com/user-attachments/assets/ad4e3f3d-13ad-44b5-8e52-23a14bcbb014" />

By doing this research we found the correct I[RI of Basilica di San petronio](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) as the first link on the list. 

## 🔎 Step 2:Looking at All Basilicas in ArCo
Our initial query revealed a surprising gap: despite its immense historical significance, San Petronio's digital record in ArCo was incredibly bare. This raised a crucial question: was this data scarcity a database-wide issue for all basilicas, or was it an omission unique to our monument?
To answer this, we decided to investigate the general term "basilica" across the entire knowledge graph, extracting all connected properties to understand how this type of architecture is standardly cataloged.

```sparql
PREFIX rdf: [http://www.w3.org/1999/02/22-rdf-syntax-ns#](http://www.w3.org/1999/02/22-rdf-syntax-ns#)
PREFIX rdfs: [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#)
PREFIX arco: [https://w3id.org/arco/ontology/arco/](https://w3id.org/arco/ontology/arco/)
PREFIX a-cd: [https://w3id.org/arco/ontology/context-description/](https://w3id.org/arco/ontology/context-description/)
PREFIX cis: [http://dati.beniculturali.it/cis/](http://dati.beniculturali.it/cis/)

SELECT DISTINCT ?entity ?property ?value
WHERE {
  ?entity a cis:CulturalInstituteOrSite ;
          rdfs:label ?l ;
          ?property ?value .

  FILTER(REGEX(?l, "basilica", "i"))
}
ORDER BY ?entity ?property
```

<img width="1915" height="856" alt="sparql basilica" src="https://github.com/user-attachments/assets/077a9451-581a-4ea3-b30d-5511798d0e77" />

## Query Breakdown: How It Works

**1. SELECT DISTINCT ?entity ?property ?value**

**What it shows:** This tells the database to display three clean columns in our final results:

**?entity:** The specific basilica resource (its link/IRI).

**?property:** The relationship or attribute type (like "hasArchitect" or "hasDesign").

**?value:** The actual information connected to that property.

**Why we use DISTINCT:** It automatically removes duplicate rows, keeping our list clean and unique.

**2. ?entity ?property ?value**

**How it extracts:** This is our data-grabber. It tells the query to retrieve every single property and every single value connected directly to those cultural sites.

**3. FILTER(REGEX(?l, "basilica", "i"))**

**How it filters:** This searches for any monument where the name (?l) contains the word "basilica".

**The "i" flag:** It ignores uppercase and lowercase letters completely, finding "Basilica", "basilica", or "BASILICA" automatically.

**3. ORDER BY ?entity ?property**

**How it organizes:** This sorts the final results table first by the monument name (?entity) and then by the type of relationship (?property).

**Why this is useful:** It neatly groups all the properties of each single basilica together, making it incredibly easy for us to read and compare them!

This query shows all the details and categories used for every basilica in the database. We use it as a checklist to see exactly what information (like architects, dates, or locations) is missing from San Petronio's page, so we know exactly what we need to add.

## ⚖️ Step 3: Comparing with Basilica di San Francesco (Arezzo)
To prove that San Petronio's record was abnormally sparse, we decided to run a comparative check against other major Italian landmarks. 
Specifically, we selected the **Basilica of San Francesco in Arezzo** as our quality benchmark, which is famous for its rich historical and artistic heritage.

To retrieve the official data record for the Basilica of San Francesco, we executed the following SPARQL query:

```sparql
PREFIX cis: [http://dati.beniculturali.it/cis/](http://dati.beniculturali.it/cis/)
PREFIX rdfs: [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#)

SELECT DISTINCT ?site ?label
WHERE {
  ?site a cis:CulturalInstituteOrSite ;
        rdfs:label ?label .
  FILTER(
    REGEX(LCASE(STR(?label)), "san francesco") &&
    REGEX(LCASE(STR(?label)), "arezzo")
  )
}
```
### Query Breakdown: How It Works
**FILTER (REGEX(...) && REGEX(...))**
* **How it searches:** This is the core update of our query. It uses a double filter connected by the **`&&`** operator:
  * **The `&&` Operator:** This acts as a logical **AND**. It means that a result will only be shown if it matches **both** conditions at the same time.
  * **First Condition:** It searches for the words "san francesco".
  * **Second Condition:** It searches for the word "arezzo".
* **Why we do this:** If we only searched for "San Francesco", the database would return hundreds of unrelated churches across Italy. By adding the second condition for "arezzo", we instantly filter out all other results and find the exact monument we need.

  <img width="1896" height="227" alt="sparql san francesco " src="https://github.com/user-attachments/assets/e6f12147-6ef2-4d7e-96ca-62c0e95e5cf5" />

 By comparison, the documentation was significantly more detailed than the data available for the Basilica of San Petronio. 
 [IRI of Basilica di San Francesco (Arezzo)](http://dati.beniculturali.it/mibact/luoghi/resource/CulturalInstituteOrSite/20560) 


