<img width="1620" height="1802" alt="El Pais_art EP 19-10-21 26" src="https://github.com/user-attachments/assets/38655e71-de57-40e0-b6c9-5b675fd7b5e0" />
# Informatica7522 
# Nome del Tuo Nuovo Progetto
## Un breve sottotitolo accattivante che descriva l'obiettivo della ricerca

Benvenuti nella pagina ufficiale del progetto. Questo spazio illustra l'integrazione tra le tecnologie del Web Semantico e la potenza dei Large Language Models (LLM).

---

## 📌 Indice delle Sezioni
1. [Home](#-home)
2. [Topic](#-topic)
3. [Methodology](#-methodology)
4. [SPARQL Queries](#-sparql-queries)
5. [LLM Prompts](#-llm-prompts)
6. [RDF Triples](#-rdf-triples)
7. [Conclusion](#-conclusion)

---

## 🏠 Home
BARBAPAPA 

---

## 📂 Topic
Descrivi dettagliatamente l'argomento (il dominio di conoscenza) che il tuo progetto prende in esame. Specifica quali sono le fonti dei dati o i testi analizzati.

---

## ⚙️ Methodology
Spiega passo dopo passo il flusso di lavoro (workflow) adottato. Ad esempio:
1. Raccolta dei dati grezzi dal Topic.
2. Ingegnerizzazione dei Prompt per l'estrazione delle entità.
3. Elaborazione tramite LLM.
4. Generazione automatica del Knowledge Graph e delle triple.

---

## 🔍 SPARQL Queries
In questa sezione puoi mostrare come interrogare il grafo di conoscenza generato. Il blocco di codice sottostante evidenzierà automaticamente la sintassi SPARQL:

```sparql
PREFIX ex: [http://example.org/project/](http://example.org/project/)
PREFIX rdf: [http://www.w3.org/1999/02/22-rdf-syntax-ns#](http://www.w3.org/1999/02/22-rdf-syntax-ns#)

SELECT ?entita ?relazione ?concetto
WHERE {
  ?entita rdf:type ex:SemanticConcept ;
          ex:relatedTo ?concetto .
}
LIMIT 5
