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
| **02** | `SELECT` | **Specifies** ➔ the projection, i.e., the number and the order of the data to retrieve 
| **03** | `WHERE` | **Constraints** ➔ imposes restrictions on the solution by means of graph patterns and/or boolean operations 
| **04** | `FILTER`    | **Restricts** ➔ Enforces explicit logical constraints, keeping only the resources that satisfy our search conditions. |
| **05** | `REGEX`     | **Matches** ➔ Evaluates text strings using advanced pattern-matching, allowing for case-insensitive and flexible keyword searches. |
| **06** | `OPTIONAL` | **Adapts** ➔ Fetches extra details safely, ignoring missing values. |
| **07** | `UNION`    | **Combines** ➔ Merges multiple alternative search paths together. |
| **08** | `ORDER BY` | **Organizes** ➔ Sorts the final results into a clean alphanumeric order. |
| **09** | `LIMIT`    | **Limits** ➔ Caps the output entries to keep the web page fast. |


## 🔎 Step 1: Mapping the Baseline – Graph Discovery

Before mapping any data extensions, it was essential to verify whether the **Basilica of San Petronio** was already recognized as an active semantic entity within national cultural open data, and to pinpoint its official taxonomic indexing.

To achieve this, we executed a discovery script filtering the graph for our target monument:

```sparql
PREFIX cis: <http://dati.beniculturali.it/cis/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?site ?label
WHERE {
  ?site a cis:CulturalInstituteOrSite ;
        rdfs:label ?label .

  FILTER(REGEX(LCASE(STR(?label)), "san petronio", "i"))
}
```

### Query Breakdown: How It Works

Let's break this query down into simple pieces:

**1. `SELECT` `DISTINCT` `?site` `?label`**
* **What it shows:** This tells the database to display only two columns in our final results: the link of the monument (`?site`) and its name (`?label`). The word `DISTINCT` makes sure we do not get the same result repeated.

**2. `?site` `a` `cis:CulturalInstituteOrSite`**
* **Where it looks:** The letter "`a`" means "is a type of". This line forces the query to look only inside the category of real physical monuments and cultural sites, skipping unrelated artworks.

**3. `rdfs:label` `?label`**
* **What it matches:** This pulls the official text name or title of the monument from the database.

**4. `FILTER`(`REGEX`(`LCASE(STR(?label`)), "san petronio" "i"))**
* **How it searches:** This is our search engine. It does three quick steps:
  * It turns the data into normal text.
  * It converts all letters to lowercase.
  * It looks for the words "san petronio".
  * `STR` Function: Converts a resource value into a plain text string.
     Why it's used: It removes language tags (like @it or @en) so that the text can be correctly read by the `REGEX` filter.
* **Why we do this:** The `i` flag stands for "case-Insensitive". When passed as a parameter inside the `REGEX` function, it instructs the query engine as following: "Search for this specific word inside the text, and completely ignore whether it is written in uppercase, lowercase, or a mix of both." It finds the basilica even if it was written with different capital letters (like "San Petronio", "san petronio", or "SAN PETRONIO").

<img width="1915" height="562" alt="sparql basilica petronio " src="https://github.com/user-attachments/assets/2b27ea6e-a4e4-4571-bb16-266e23e16190" />
By doing this research we found the correct [IRI of Basilica di San Petronio](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) as the first link on the list. 

* **Results:** Only a limited amount of information about the Basilica is available on ArCo:
* Name
* Type
* Location
<img width="1878" height="518" alt="image" src="https://github.com/user-attachments/assets/7bf02789-ba95-435c-858e-a5802a7e995c" />
 

## 🔎 Step 2:Looking at All Basilicas in ArCo
Our initial query revealed a surprising gap: despite its immense historical significance, San Petronio's digital record in ArCo was incredibly bare. This raised a crucial question: was this data scarcity a database-wide issue for all basilicas, or was it an omission unique to our monument?
To answer this, we decided to investigate the general term "basilica" across the entire knowledge graph, extracting all connected properties to understand how this type of architecture is standardly cataloged.

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/>
PREFIX cis: <http://dati.beniculturali.it/cis/>

SELECT DISTINCT ?entity ?property ?value
WHERE {
  ?entity a cis:CulturalInstituteOrSite ;
          rdfs:label ?l ;
          ?property ?value .

  FILTER (regex(str(?l), "basilica", "i"))
}
ORDER BY ?entity ?property
LIMIT 100
```
By applying the `FILTER` directly to the label `l`, and by limiting the results to 100, we managed to restrict the range of results, which otherwise would have been gigantic.

<img width="1915" height="856" alt="sparql basilica" src="https://github.com/user-attachments/assets/077a9451-581a-4ea3-b30d-5511798d0e77" />

### Query Breakdown: How It Works

**1. `SELECT` `DISTINCT` `?entity` `?property` `?value`**

**What it shows:** This tells the database to display three clean columns in our final results:

**`?entity`:** The specific basilica resource (its link/IRI).

**`?property`:** The relationship or attribute type (like "hasArchitect" or "hasDesign").

**`?value`:** The actual information connected to that property.

**Why we use `DISTINCT`:** It automatically removes duplicate rows, keeping our list clean and unique.

**2. `?entity` `?property` `?value`**

**How it extracts:** This is our data-grabber. It tells the query to retrieve every single property and every single value connected directly to those cultural sites.

**3. `FILTER`(`REGEX`(`?l`, "basilica", "`i`"))**

**How it filters:** This searches for any monument where the name (`?l`) contains the word "basilica".

**The "`i`" flag:** It ignores uppercase and lowercase letters completely, finding "Basilica", "basilica", or "BASILICA" automatically.

**3. `ORDER BY` `?entity` `?property`**

**How it organizes:** This sorts the final results table first by the monument name (`?entity`) and then by the type of relationship (`?property`).

**Why this is useful:** It neatly groups all the properties of each single basilica together, making it incredibly easy for us to read and compare them!

This query shows all the details and categories used for every basilica in the database. We use it as a checklist to see exactly what information (like architects, dates, or locations) is missing from San Petronio's page, so we know exactly what we need to add.

## ⚖️ Step 3: Comparing with Basilica di San Francesco (Arezzo)
To prove that San Petronio's record was abnormally sparse, we decided to run a comparative check against other major Italian landmarks. 
Specifically, we selected the **Basilica of San Francesco in Arezzo** as our quality benchmark, which is famous for its rich historical and artistic heritage.

To retrieve the official data record for the Basilica of San Francesco, we executed the following SPARQL query:

```sparql
PREFIX cis: <http://dati.beniculturali.it/cis/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?site ?label
WHERE {
  ?site a cis:CulturalInstituteOrSite ;
        rdfs:label ?label .
  
  FILTER (
    regex(str(?label), "san francesco", "i") &&
    regex(str(?label), "arezzo", "i")
  )
}
LIMIT 100
```
### Query Breakdown: How It Works
**`FILTER` (`REGEX`(...) `&&` `REGEX`(...))**
* **How it searches:** This is the core update of our query. It uses a double filter connected by the **`&&`** operator:
  * **The `&&` Operator:** This acts as a logical **AND**. It means that a result will only be shown if it matches **both** conditions at the same time.
  * **First Condition:** It searches for the words "san francesco".
  * **Second Condition:** It searches for the word "arezzo".
* **Why we do this:** If we only searched for "San Francesco", the database would return hundreds of unrelated churches across Italy. By adding the second condition for "arezzo", we instantly filter out all other results and find the exact monument we need.

  <img width="1896" height="227" alt="sparql san francesco " src="https://github.com/user-attachments/assets/e6f12147-6ef2-4d7e-96ca-62c0e95e5cf5" />
By comparison, the documentation was significantly more detailed than the data available for the Basilica of San Petronio. 
 [IRI of Basilica di San Francesco (Arezzo)](http://dati.beniculturali.it/mibact/luoghi/resource/CulturalInstituteOrSite/20560) 

## Step 4: Comparing results: gaps identified
By comparing the results of Query 2 and Query 3 with the first Query, we outlined (numero) gaps that should be added to enrich Basilica di San Petronio:

📝 Description
🔗 Wikidata link
📍 Geographical coordinates 
📷 Official image
🎟️ Entrance ticket
⛔ Access Conditions
📞 Contact 

## Step 5: Queries to double-check these gaps ArCo
In order to ensure the absence of such information on ArCo, we run some queries. 

### Query 1:


### Query 2: Verifying the absence of the wikidata link
We executed a targeted SPARQL query to investigate whether ArCo's graph contains an explicit Linked Data connection to the corresponding Wikidata profile for the Basilica di San Petronio.
🔍 Query:

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

SELECT DISTINCT ?p ?o
WHERE {
  <http://dati.beniculturali.it/cis/CulturalInstituteOrSite/basilica-di-san-petronio> ?p ?o .
  FILTER (STRSTARTS(STR(?o), "https://www.wikidata.org/entity/") || STRSTARTS(STR(?o), "https://www.wikidata.org/wiki/"))
}
```
📝 Analysing the query:

* Subject Target: The query isolates the unique URI assigned by ArCo to the Basilica (...`/basilica-di-san-petronio`) as the main subject of our search.
* String-Pattern Matching: Instead of scanning all properties, the `FILTER` block utilizes the `STRSTARTS` function. This evaluates the string format of every object (`?o`) to check if it points to either a Wikidata structured entity (`/entity/`) or a standard Wikipedia/Wikidata web page (`/wiki/`).

📊 Results:
❌ Empty Dataset

Despite being one of Italy's major heritage sites, the Basilica di San Petronio exists as an isolated node within ArCo, lacking semantic alignment with the global Wikidata knowledge base.
