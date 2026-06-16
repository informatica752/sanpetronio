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

## 🏛️ 1. Basilica Description 

Providing a description that fits highly specialized academic standards can be difficult for an AI. To test if the models could replicate a sophisticated, institutional tone, we used a **Few-Shot prompt**. We provided them with an official, high-level example from the ArCo (Architecture of Knowledge) portal and asked them to write a description of the Basilica matching that exact academic style, vocabulary, and flow.

### Prompt Used 

```Please provide a description of the Basilica of San Petronio in Bologna, Italy, matching the style of the following example found on ArCo: 
"The Gothic basilica of San Francesco, rich in frescoed testimonies of fourteenth-century Aretine painting, welcomes one of the greatest masterpieces of the Renaissance, the 'Legend of the True Cross' by Piero della Francesca, the extraordinary cycle painted by the artist between around 1452 and 1455 in the Bacci Chapel. The luminous stories of Piero della Francesca, restored to their splendor in 2000 after a long restoration process, represent an essential destination for anyone who considers Renaissance civilization one of the greatest achievements of the human spirit. The new lighting, created thanks to the Light is Back project by iGuzzini, enhances Piero della Francesca's 'painting of light', all its crystalline legibility, forms, space, and color. The cycle illustrates some of the stories from the 13th-century 'Golden Legend' by Jacopo da Varagine, an iconographic source on which many depictions by Tuscan and Italian artists from the fourteenth century onwards are based. Scene after scene, it narrates the history of the wood of Christ's Cross, from the seed of the tree placed in the mouth of the dying Adam to the recapture of the Cross from the hands of Chosroes by Emperor Heraclius and his final entry into Jerusalem. Set against landscapes dear to the artist and painted architecture—Arezzo itself perched on the hill and Sansepolcro with its buildings in perspective—elegant and geometrically perfect figures accompany the observer through the narrative and history. In the basilica, particular emphasis is given not only to the stained glass windows by Guglielmo de Marcillat, but also to the Tarlati Chapel with the Annunciation attributed to Matteo Lappoli, the large wooden Crucifix on the high altar attributed to the Master of San Francesco, the frescoes by Spinello Aretino, other valuable works, and the recently restored funeral monument of Francesco Roselli."```

Write the new description making sure it perfectly fits the institutional standards and style of the ArCo portal.

### LLM Outputs 

Below are the visual results obtained from the models, showing how they adapted to the academic example and structured the historical and artistic information under institutional standards:

#### ChatGPT Response
<img width="705" height="847" alt="description 5 " src="https://github.com/user-attachments/assets/04ee6cd2-7a4d-4ade-9756-f042d7f4eea2" />


#### Gemini Response
<img width="688" height="807" alt="description 6 " src="https://github.com/user-attachments/assets/4ed6deb2-8071-4272-aa1c-bb0a6098365d" />


✅ **LLMs comparison:**

Both models successfully abandoned their standard formatting to mimic the dense, institutional style of the ArCo example, but they approached the academic structure differently:

* **ChatGPT:** Focuses heavily on the thematic narrative. It uses highly sophisticated, flowing vocabulary to explain the historical tensions between civic and church power, diving deep into the cultural meaning behind the architecture.
* **Gemini:** Strictly replicates the literal structure of the ArCo portal example. It uses a dense, compact layout enclosed in quotation marks, heavily featuring specific dates (1390, 1400, 1475, 1492, 1547, 1655) and exact historical names to maximize its academic value.

**Overall** ⬇️:

**ChatGPT**:captures the *spirit* of the academic prompt, focusing on high-level artistic concepts and historical themes across split paragraphs.

**Gemini**:captures the *exact template* of the institutional prompt, packing a massive amount of technical architectural facts, names, and precise dates into a direct imitation.


## 🌐 2. Wikidata Page 

Verifying if a monument has an official Wikidata page is important for linking its data globally, but AIs can sometimes hallucinate or generate unnecessary links. To test if the models could correctly confirm its existence using only what they already knew, we used a **Zero-Shot prompt**. We simply asked them a direct "Yes" or "No" question without giving any examples or extra links, allowing us to see how accurate they are on their own.

### Prompt Used 

Does an official Wikidata page exist for the Basilica of San Petronio in Bologna, Italy?

### LLM Outputs 

The visual evidence below displays whether the models confirmed or denied the presence of the Wikidata record:

#### ChatGPT Response

<img width="683" height="662" alt="WIKIDATA  1" src="https://github.com/user-attachments/assets/0cf6977d-beec-4c0b-9ca1-bcdec1d1fd77" />


#### Gemini Response

<img width="507" height="231" alt="WIKIDATA 2 " src="https://github.com/user-attachments/assets/38b15161-14b3-401f-80bb-fe7a4093deec" />

✅ **LLMs comparison:**

➡️ Both models correctly answered "Yes" and identified the exact Wikidata ID (**Q810103**), but they organized the data quite differently:

* **ChatGPT:** Provides a highly structured and detailed report. It extracts specific data points from Wikidata (like Name, Location, Religion, and Architectural identity) into a bulleted list, provides the direct URL link, and adds a final conclusion box.
* **Gemini:** Gives a short, direct paragraph response. Instead of listing individual data points, it summarizes what kind of information can be found on the page (like history, coordinates, and dimensions) and relies on automated citation chips for links.

**Overall** ⬇️:

**ChatGPT**: acts like a data analyst, creating an organized, itemized report with a direct web link.

**Gemini**: acts like a fast search assistant, giving a quick text summary with automatic background source links.


## 🌍 3. Geographical Coordinates

Both Gemini and ChatGPT were evaluated using a zero-shot prompting technique, where they were tasked with providing the exact latitude and longitude of the Basilica of San Petronio in Bologna, Italy.

The objective was to assess how precisely each model can retrieve and present geospatial data for a well-known landmark.

### Prompt Used 
Could you please give me the exact latitide and longitude of the Basilica of San Petrionio (Bologna)?

🤖 **ChatGPT Response**

<img width="657" height="250" alt="image" src="https://github.com/user-attachments/assets/c99375f6-f02f-431d-9616-dd859a164dc8" />


🤖 **Gemini Response**

<img width="599" height="137" alt="image" src="https://github.com/user-attachments/assets/1a646310-252c-46e0-9c90-e06871b10ac8" />


✅ **LLM Comparison**

➡️ Both models successfully identified the correct geographical location of the Basilica of San Petronio in Bologna and provided highly similar coordinate values. However, minor differences were observed in numerical precision and formatting:

**Gemini**: Presents coordinates in a slightly rounded format, prioritizing simplicity and readability over decimal granularity.
**ChatGPT**: Provides coordinates with a higher level of decimal precision, reflecting a more exact numeric representation.

**Overall** ⬇️:  

**ChatGPT:** emphasizes numerical precision and fine-grained coordinate representation, which may be useful for mapping or computational use cases requiring higher accuracy.

**Gemini:** prioritizes clarity and compactness, offering coordinates in a more simplified format that remains fully usable for general navigation purposes.

## 🖼️ 4. Official Image

We requested both ChatGPT and Gemini to provide a URL of an image of the Basilica of San Petronio in Bologna using a few-shot prompting approach, where an example was included to guide the expected format and type of response.

### Prompt Used: 
Please find the primary image associated with the Basilica of San Petronio (Bologna). Provide the direct image URL (JPG, PNG, or equivalent), specify whether it is an official image, a historical photograph, a contemporary photograph, or an artistic depiction. Include the exact source of the image, the page where it is hosted, the image file URL, and any available attribution or licensing information.

Example: 
An officially recognized image of the Duomo di Firenze is available on Wikimedia Commons.

- URL: https://commons.wikimedia.org/wiki/File:Florence_Cathedral_(Duomo).jpg
- Title: Florence Cathedral (Duomo).jpg:
- Author: Kevin Poh;
- Source:https://commons.wikimedia.org/wiki/File:Florence_Cathedral_(Duomo).jpg
- License: https://creativecommons.org/licenses/by/2.0

#### ChatGPT Response
<img width="913" height="570" alt="image" src="https://github.com/user-attachments/assets/33872be1-398f-4b96-b0bc-56bd19bccccf" />
<img width="902" height="466" alt="image" src="https://github.com/user-attachments/assets/6c549123-8474-4e0f-840b-dab64ca9f912" />

#### Gemini Response
<img width="753" height="727" alt="image" src="https://github.com/user-attachments/assets/1fbd0b72-aad7-432b-b381-ae8141c02307" />
<img width="766" height="520" alt="image" src="https://github.com/user-attachments/assets/fc50ec31-2e1d-4b99-ab52-cef3aa457d3a" />


✅ **LLM Comparison**

➡️ The results highlight a key difference in how the models interpret the concept of an “official image”:

**ChatGPT**: Clearly states that no official image exists and provides multiple curated Wikimedia Commons alternatives with detailed metadata and licensing information.
**Gemini**: Selects a single “primary” image without explicitly addressing the absence of an official designation, focusing instead on visual representativeness. Gemini's response contains a further inconsistency: the image it identifies as the primary representation of the basilica does not match the image displayed at the URL it provides.

**Overall** ⬇️:

**ChatGPT:** adopts a more cautious and documentation-driven approach, explicitly clarifying the absence of an official image and offering multiple verified alternatives.

**Gemini:** takes a more direct approach by selecting one image it considers most representative, without discussing official status or alternative options.

## 🎟️ 5. Entrance Ticket

Finding out the price of admission tickets can be tricky because prices often change based on age groups, student discounts, or free entry rules. To make sure ChatGPT and Gemini didn't make mistakes, we used a **Chain-of-Thought (CoT)** prompt. This forced the models to reason step-by-step and look at all the different ticket options before giving us the final price.

### Prompt Used 

Please find the entrance ticket information for the Basilica of San Petronio in Bologna, Italy.

To ensure the answer is correct, think step-by-step and show your reasoning out loud before giving the final summary:

1. Look at the general entry: Determine if entering the main area of the Basilica is free or if it requires a paid ticket.
2. Check for internal attractions: Check if specific areas inside (such as the Magi Chapel/Cappella dei Magi, the panoramic terrace, or the museum) have separate ticket fees.
3. Identify the prices: For any paid area, list the standard full price and check if there are any concessions (for students, seniors, or kids) or free entry criteria.
4. Verify extra rules: Check if there are mandatory fees for things like taking photos or group tours.

Finally, summarize the results using this format:
- General Entry Status: [Free / Paid]
- Special Areas & Prices: [List the areas and their specific costs]
- Concessions/Free Entry: [Who gets a discount or enters for free] 


### LLM Outputs 

Below are the visual results obtained from the models showing their logical breakdown before compiling the required data layout:

#### ChatGPT Response
<img width="540" height="757" alt="entrance 1 " src="https://github.com/user-attachments/assets/55c2a32d-83b8-4ea5-97c0-a1510e471c2b" />
<img width="528" height="862" alt="entrance 2 " src="https://github.com/user-attachments/assets/a5c6cf31-101d-4bf8-96c1-51c3f6a00780" />



#### Gemini Response
<img width="573" height="792" alt="entrance 3 " src="https://github.com/user-attachments/assets/754b85a5-d9f8-4be2-ad2e-133bf1e10d94" />
<img width="503" height="458" alt="entrance 4 " src="https://github.com/user-attachments/assets/f3464a9b-b8a0-470f-8671-8fbdadb46455" />


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

To find the official contact details, we used a **Zero-Shot** approach. We specifically designed the prompt to separate phone numbers from email addresses into distinct, clean sections. This layout was essential for us to easily read, copy, and organize the contact channels without mixing them up.

### Prompt Used 
Please find the official contact information for the Basilica of San Petronio in Bologna, Italy.

Search for phone numbers, email addresses, and the official website. You must separate the phone numbers section from the email section so they are distinct and easy to copy. If there are multiple phone numbers or emails (for example, for both the tourist desk, the parish office, or bookings), please list them all.

If a specific piece of information is missing, just write N/D. 


### LLM Outputs 

Below are the visual results obtained from the models showing the direct information extraction and clean formatting required by our prompt.


#### ChatGPT Response
<img width="585" height="723" alt="CONTACTS 1 " src="https://github.com/user-attachments/assets/7ef54657-305f-40fa-b2bd-65e5a03a2969" />
<img width="526" height="268" alt="CONTACT 2 " src="https://github.com/user-attachments/assets/02b7f368-5a8e-4cbb-afe3-5ecac7269459" />



#### Gemini Response
<img width="598" height="690" alt="CONTACT 3 " src="https://github.com/user-attachments/assets/43c931f5-9b0a-4e14-90e0-94125a89a095" />

✅ **LLMs comparison:**

➡️ Both models found the main contact information and separated phone numbers from emails, but they chose a different level of detail:

* **ChatGPT :** Digs deeper into internal offices. It finds specific contacts for researchers and historians, like the phone number and email for the Historical Archive, the Musical Archive email, and the Sacristy. It also adds a nice "quick copy" summary section.
* **Gemini :** Focuses only on the main contacts used by standard tourists and group planners (general info and booking). It includes an official email address listed by the Archdiocese of Bologna (`BasilicaSanPetronio@alice.it`) but leaves out the specific archive departments.

**Overall** ⬇️:

**ChatGPT**: goes much deeper into internal details, finding specific contacts for advanced or niche requests (like archives).

**Gemini**: keeps it simple for the general public, showing only the most important tourist lines and the official church registry email.






