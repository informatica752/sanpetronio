---
layout: default
title: 🤖 LLM Prompts
---

# 🤖 LLM Querying & Prompt Engineering

To retrieve the missing data for the points of interest in **Arco**, we queried Large Language Models (LLMs) using different Prompt Engineering strategies. 

## 🛠️ Models Utilized
* **ChatGPT (OpenAI):** Utilized for its high precision in structured formatting and complex reasoning tasks.
* **Gemini (Google):** Employed for its strong contextual understanding and fluid textual generation.

The choice of the prompting technique was carefully selected and adapted for both models based on the nature of the data to be extracted (e.g., free-form text, strict formats, or data requiring logical reasoning).

Below is the methodological overview of the three techniques applied across ChatGPT and Gemini: **Zero-Shot**, **Few-Shot**, and **Chain-of-Thought**.

## 🔬 The Three Prompting Techniques Used

### 1. 🎯 Zero-Shot Prompting
This technique involves making a direct request to the models **without providing any examples**. The models rely exclusively on the knowledge pre-trained within their parameters.
* **Best for:** Simple linguistic tasks, summarization, or straightforward factual data retrieval.

### 2. 📋 Few-Shot Prompting
This consists of providing the models with **one or more concrete examples** (input/output pairs) before asking the final question. This conditions the LLMs to strictly follow a specific style, length, or syntactic structure.
* **Best for:** Output standardization, style matching and extracting structured media links.

### 3. 🧠 Chain-of-Thought (CoT)
This technique forces the models to **break down a complex problem and "think aloud"**, displaying intermediate logical steps before delivering the final answer.
* **Best for:** Complex reasoning or analyzing multi-variable rules and pricing sheets.
* 
---

## 📊 Prompt Strategy Overview

The table below summarizes the exact prompting strategy used for each missing data point across our LLM workflows:

| Missing Data | Chosen Technique | Rationale & Objective |
| :--- | :--- | :--- |
| **1. 📝 Description** | `Few-Shot` | Guides the models to generate descriptions matching a specific length, tone, and editorial style. |
| **2. 🔗 Wikidata link** | `Zero-Shot` | Direct extraction of the unique knowledge-graph URL from the models' database. |
| **3. 📍 Coordinates** | `Zero-Shot` | Straightforward retrieval of numerical values (Lat, Lon) for the locations. |
| **4. 📷 Official image** | `Few-Shot` | Ensures the model follows the exact syntax and domain pattern required for media assets. |
| **5. 🎟️ Entrance ticket**| `Chain-of-Thought` | Step-by-step analysis of standard rates, concessions, and free entry criteria. |
| **7. 📞 Contact** | `Zero-Shot` | Quick and direct extraction of available telephone numbers and email addresses. |

> ⚠️ **Methodological Note:** Although ChatGPT and Gemini proved highly capable of retrieving information, all data extracted through these techniques underwent a manual validation process to eliminate hallucinations, especially regarding URLs and coordinates.










## 🎟️ 5. Entrance Ticket

Finding out the price of admission tickets can be tricky because prices often change based on age groups, student discounts, or free entry rules. To make sure ChatGPT and Gemini didn't make mistakes, we used a **Chain-of-Thought (CoT)** prompt. This forced the models to reason step-by-step and look at all the different ticket options before giving us the final price.

### Prompt Used 
|`Please find the entrance ticket information for the Basilica of San Petronio in Bologna, Italy.

To ensure the answer is correct, think step-by-step and show your reasoning out loud before giving the final summary:

1. Look at the general entry: Determine if entering the main area of the Basilica is free or if it requires a paid ticket.
2. Check for internal attractions: Check if specific areas inside (such as the Magi Chapel/Cappella dei Magi, the panoramic terrace, or the museum) have separate ticket fees.
3. Identify the prices: For any paid area, list the standard full price and check if there are any concessions (for students, seniors, or kids) or free entry criteria.
4. Verify extra rules: Check if there are mandatory fees for things like taking photos or group tours.

Finally, summarize the results using this format:
- General Entry Status: [Free / Paid]
- Special Areas & Prices: [List the areas and their specific costs]
- Concessions/Free Entry: [Who gets a discount or enters for free]`|


### LLM Outputs 

Below are the visual results obtained from the models showing their logical breakdown before compiling the required data layout:

#### ChatGPT Response
<img width="528" height="862" alt="entrance 2 " src="https://github.com/user-attachments/assets/a5c6cf31-101d-4bf8-96c1-51c3f6a00780" />
<img width="540" height="757" alt="entrance 1 " src="https://github.com/user-attachments/assets/55c2a32d-83b8-4ea5-97c0-a1510e471c2b" />


#### Gemini Response
<img width="503" height="458" alt="entrance 4 " src="https://github.com/user-attachments/assets/f3464a9b-b8a0-470f-8671-8fbdadb46455" />
<img width="573" height="792" alt="entrance 3 " src="https://github.com/user-attachments/assets/754b85a5-d9f8-4be2-ad2e-133bf1e10d94" />

✅ **LLMs comparison:**

➡️ Both models provided accurate baseline pricing for the chapel route, but they diverge significantly on operational updates and specific group regulations:

* **ChatGPT:** Focuses on a generalized, slightly outdated tourist overview. It leaves the panoramic terrace as a tentative option ("when available/seasonal") and claims no photo fee applies inside. It follows a standard sequence and concludes with an offer to map out a traveler's itinerary.
* **Gemini:** Adopts a highly precise, administrative approach based on official, updated institutional rules. It correctly tracks recent operational changes, noting the definitive closure of the terrace, and captures the specific €2.00 internal photography permit rule.
* **ChatGPT:** Simplifies the general entry guidelines by stating that accessing the main body of the basilica is entirely free for everyone without exception.
* **Gemini:** Deepens data integrity by uncovering specific logistical rules for institutional groups. It highlights that while individual adults enter for free, formal school and youth groups are subject to a mandatory €2.00 entry fee just to access the basilica.

**Overall** ⬇️:

**ChatGPT**: its approach is conversational, relies on historic travel-guide data, and misses precise micro-rules.

**Gemini** : its approach is factual and rigorous, capturing policy updates and exact administrative group rules for data accuracy.


## 📞 7. Contacts

To retrieve official contact information such as telephone numbers, email addresses, and official websites, we implemented a **Zero-Shot** approach. Since we needed a strict structural separation between phone contacts and email lists to facilitate seamless database integration, the prompt embedded formatting constraints directly into the natural language instructions.


### LLM Outputs & Validation

Both models successfully processed the request, cleanly partitioning the operational telephone channels from the digital mailing endpoints as shown below:

#### ChatGPT Response
![ChatGPT Contacts Screen](path-to-your-image/chatgpt-contacts.png)

#### Gemini Response
![Gemini Contacts Screen](path-to-your-image/gemini-contacts.png)









