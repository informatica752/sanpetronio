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
| **02** | `SELECT` | **Specifies** ➔ the projection, i.e., the number and the order of the data to retrieve |
| **03** | `WHERE` | **Constraints** ➔ imposes restrictions on the solution by means of graph patterns and/or boolean operations |
| **04** | `FILTER`    | **Restricts** ➔ Enforces explicit logical constraints, keeping only the resources that satisfy our search conditions. |
| **05** | `REGEX`     | **Matches** ➔ Evaluates text strings using advanced pattern-matching, allowing for case-insensitive and flexible keyword searches. |
| **06** | `OPTIONAL` | **Adapts** ➔ Fetches extra details safely, ignoring missing values. |
| **07** | `UNION`    | **Combines** ➔ Merges multiple alternative search paths together. |
| **08** | `ORDER BY` | **Organizes** ➔ Sorts the final results into a clean alphanumeric order. |
| **09** | `LIMIT`    | **Limits** ➔ Caps the output entries to keep the web page fast. |


## 🔎 Step 1: Mapping the Baseline – Graph Discovery

Before mapping any data extensions, it was essential to verify whether the **Basilica of San Petronio** was already recognized as an active semantic entity within national cultural open data.

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
* **What it shows:** This tells the database to display only two columns in our final results: the link of the monument (`?site`) and its name (`?label`). The word `DISTINCT` makes sure we do not get duplicates.

**2. `?site` `a` `cis:CulturalInstituteOrSite`**
* **Where it looks:** The letter "`a`" means "is a type of". This line forces the query to look only inside the category of real physical monuments and cultural sites, skipping unrelated artworks.

**3. `rdfs:label` `?label`**
* **What it matches:** This pulls the official text name or title of the monument from the database.

**4. `FILTER`(`REGEX`(`LCASE(STR(?label`)), "san petronio", "i"))**
* **How it searches:** This is our search engine. It does three quick steps:
  * It turns the data into normal text.
  * It converts all letters to lowercase.
  * It looks for the words "san petronio".
  * `STR` Function: Converts a resource value into a plain text string.
     Why it's used: It removes language tags (like @it or @en) so that the text can be correctly read by the `REGEX` filter.
* **Why we do this:** The `i` flag stands for "case-Insensitive". When passed as a parameter inside the `REGEX` function, it instructs the query engine to search for this specific word in any case variation.

By doing this research we found the correct [IRI of Basilica di San Petronio](http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio) as the first result.

* **Results:** Only a limited amount of information about the Basilica is available on ArCo:
  * Name
  * Type
  * Location

## 🔎 Step 2: Looking at All Basilicas in ArCo

Our initial query revealed a surprising gap: despite its immense historical significance, San Petronio's digital record in ArCo was incredibly bare. This raised a crucial question: was this data scarce across the entire knowledge graph?

To answer this, we decided to investigate the general term "basilica" across the entire knowledge graph, extracting all connected properties to understand how this type of architecture is standardly categorized.

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

By applying the `FILTER` directly to the label `l`, and by limiting the results to 100, we managed to restrict the range of results, which otherwise would have been enormous.

### Query Breakdown: How It Works

**1. `SELECT` `DISTINCT` `?entity` `?property` `?value`**

**What it shows:** This tells the database to display three clean columns in our final results:

* **`?entity`:** The specific basilica resource (its link/IRI).
* **`?property`:** The relationship or attribute type (like "hasArchitect" or "hasDesign").
* **`?value`:** The actual information connected to that property.

**Why we use `DISTINCT`:** It automatically removes duplicate rows, keeping our list clean and unique.

**2. `?entity` `?property` `?value`**

**How it extracts:** This is our data-grabber. It tells the query to retrieve every single property and every single value connected directly to those cultural sites.

**3. `FILTER`(`REGEX`(`?l`, "basilica", "`i`"))**

**How it filters:** This searches for any monument where the name (`?l`) contains the word "basilica".

**The "`i`" flag:** It ignores uppercase and lowercase letters completely, finding "Basilica", "basilica", or "BASILICA" automatically.

**4. `ORDER BY` `?entity` `?property`**

**How it organizes:** This sorts the final results table first by the monument name (`?entity`) and then by the type of relationship (`?property`).

**Why this is useful:** It neatly groups all the properties of each single basilica together, making it incredibly easy for us to read and compare them!

This query shows all the details and categories used for every basilica in the database.

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
* **Why we do this:** If we only searched for "San Francesco", the database would return hundreds of unrelated churches across Italy. By adding the second condition for "arezzo", we instantly filter out unrelated results.

By comparison, the documentation was significantly more detailed than the data available for the Basilica of San Petronio. 

You can find the [IRI of Basilica di San Francesco (Arezzo)](http://dati.beniculturali.it/mibact/luoghi/resource/CulturalInstituteOrSite/20560).

## Step 4: Comparing results – gaps identified

By comparing the results of the queries above with the first query, we outlined six main gaps that should be added to enrich Basilica di San Petronio's record:

1. 📝 Description
2. 🔗 Wikidata link
3. 📍 Geographical coordinates 
4. 📷 Official image
5. 🎟️ Entrance ticket
6. 📞 Contact information

## Step 5: Queries to verify these gaps in ArCo

In order to ensure the absence of such information on ArCo, we ran several queries using the IRI of Basilica di San Petronio: `http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio`

### Query 1: Verifying the absence of a description 📝

We executed a query to verify whether a formal textual description or historical overview of the Basilica di San Petronio exists within the knowledge graph:

```sparql
PREFIX l0: <https://w3id.org/italia/onto/l0/>
PREFIX arco: <https://w3id.org/arco/ontology/core/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?property ?descriptionText ?descriptionLabel
WHERE {
  {
    <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
      l0:description ?descriptionText .
    BIND("l0:description" AS ?property)
    BIND("" AS ?descriptionLabel)
  }
  UNION
  {
    <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio>
      arco:hasDescription ?descResource .
    BIND("arco:hasDescription" AS ?property)
    ?descResource l0:description ?descriptionText .
    OPTIONAL { ?descResource rdfs:label ?descriptionLabel }
  }
}
ORDER BY ?property ?descriptionText
LIMIT 10
```

**Analyzing the query:**

* **Subject Target:** The query isolates the unique URI assigned by ArCo to the Basilica as the main subject of our search.
* **Multiple Vocabulary Scanning:** To prevent false negatives, the query scans different vocabularies simultaneously:
  * **Direct Attachment** (`l0:description`): checks if a text block is directly attached to the main monument resource using the national OntoPiA base vocabulary.
  * **Indirect Modeling** (`arco:hasDescription`): analyzes the graph to see if the text is encapsulated within a complex, intermediate description resource.

**Results:** ❌ Empty Table

It confirms the absence of any description.

### Query 2: Verifying the absence of the Wikidata link 🔗

We executed a targeted SPARQL query to investigate whether ArCo's graph contains an explicit Linked Data connection to the corresponding Wikidata profile for the Basilica di San Petronio:

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

SELECT DISTINCT ?p ?o
WHERE {
  <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio> ?p ?o .
  FILTER (STRSTARTS(STR(?o), "https://www.wikidata.org/entity/") || STRSTARTS(STR(?o), "https://www.wikidata.org/wiki/"))
}
```

**Analyzing the query:**

* **Subject Target:** The query isolates the unique URI assigned by ArCo to the Basilica as the main subject of our search.
* **String-Pattern Matching:** Instead of scanning all properties, the `FILTER` block utilizes the `STRSTARTS` function to check if any object points to a Wikidata URL.

**Results:** ❌ Empty Dataset

Despite being one of Italy's major heritage sites, the Basilica di San Petronio exists as an isolated node within ArCo, lacking semantic alignment with the global Wikidata knowledge base.

### Query 3: Verifying the absence of geographical coordinates 📍

We executed a query to verify whether ArCo explicitly integrates geospatial positioning data within the semantic profile of the Basilica di San Petronio:

```sparql
PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?lat ?long
WHERE {
  <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio> 
      geo:lat ?lat ;
      geo:long ?long .
}
LIMIT 5
```

**Analyzing the query:**

* **Coordinate Search:** In structured cultural heritage graphs, coordinates are rarely attached directly to the monument. Instead, intermediate spatial nodes are often used.
* **Direct Properties:** This query looks for the standard `geo:lat` and `geo:long` properties.

**Results:** ❌ Empty Table

This confirms that ArCo lacks both direct coordinate triples and formal geometry instances for the Basilica di San Petronio.

### Query 4: Verifying the absence of an official depiction 📷

We designed an exploratory SPARQL query to detect whether ArCo encompasses any official visual assets or digital media linked to the Basilica di San Petronio in Bologna:

```sparql
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>

SELECT DISTINCT ?image
WHERE {
  {
    <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio> 
        foaf:depiction ?image .
  }
  UNION
  {
    <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio> 
        arco:hasRepresentative ?image .
  }
  UNION
  {
    <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio> 
        arco:hasDigitalRepresentation ?image .
  }
}
LIMIT 10
```

**Analyzing the query:**

To maximize the efficiency of this check, the query implements a `UNION` pattern, cross-referencing three distinct semantic pathways where an image asset might be nested:

* **`foaf:depiction`:** the cross-domain standard predicate used to link a conceptual resource to its visual representation.
* **`arco:hasRepresentative`:** from the ArCo ontology; usually points to a representative image of the cultural entity.
* **`arco:hasDigitalRepresentation`:** a broader ontological property designed to connect physical monuments with their web-accessible digital twins or files.

**Results:** ❌ Empty Table

The official national graph lacks any direct link to an official image of the Basilica.

### Query 5: Verifying the absence of entrance ticket information 🎟️

We verified the presence of admission ticket information connected to the Basilica:

```sparql
PREFIX potapit: <https://w3id.org/italia/onto/POT/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?ticket ?label ?price
WHERE {
  <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio> 
      potapit:hasTicket ?ticket .
  
  OPTIONAL { ?ticket rdfs:label ?label . }
  OPTIONAL { ?ticket potapit:hasPriceSpecification ?price . }
}
LIMIT 10
```

**Analyzing the query:**

* **Property Selection** (`potapit:hasTicket`): This property comes from the POT-AP-IT (Prices, Offers, Tickets - Italian Application Profile) vocabulary, integrated into ArCo to model entry fees and ticket information.
* **`OPTIONAL` Blocks:** Instead of a rigid lookup, the query uses `OPTIONAL` patterns to retrieve any additional human-readable labels or specific price structures.

**Results:** ❌ Empty Table

### Query 6: Verifying the absence of contact details 📞

We verified the presence of contact details:

```sparql
PREFIX smapit: <https://w3id.org/italia/onto/SM/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?contactPoint ?contactType ?contactValue
WHERE {
  <http://dati.beniculturali.it/iccd/schede/resource/CulturalInstituteOrSite/S001851_Basilica_di_San_Petronio> 
      smapit:hasOnlineContactPoint ?contactPoint .
  
  OPTIONAL { ?contactPoint rdfs:label ?contactType . }
  OPTIONAL { ?contactPoint smapit:hasEmail ?contactValue . }
  OPTIONAL { ?contactPoint smapit:hasTelephone ?contactValue . }
  OPTIONAL { ?contactPoint smapit:hasWebSite ?contactValue . }
}
LIMIT 10
```

**Analyzing the query:**

* **URI Specificity:** By using the unique, hardcoded URI of Basilica di San Petronio, we ensure that the endpoint evaluates only the explicit graph node belonging to the main church building.
* **Property Selection** (`smapit:hasOnlineContactPoint`): This relation looks for an outward link from the physical church node to an abstract digital container defined by the `SM-AP-IT` (Social Media and Services - Italian Application Profile) vocabulary.
* **`OPTIONAL` Parameters:** Runs parallel, independent checks to capture categorization labels, email addresses, phone lines, and websites.

**Results:** ❌ Empty Dataset

