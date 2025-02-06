# **Introduction to Amazon Bedrock Foundation Models**  

Amazon Bedrock provides **a wide selection of high-performing foundation models (FMs)** from leading AI startups and Amazon. These models cater to **various generative AI use cases**, including **text summarization, language translation, coding, and image generation.**  

---

## **📌 Foundation Models Available in Amazon Bedrock**  

| **Company**       | **Foundation Model**       | **Description**  |
|------------------|-------------------------|-----------------|
| **Amazon**       | Amazon Titan            | General-purpose models pretrained on large datasets.  |
| **AI21 Labs**    | Jurassic-2, Jumba       | Multilingual LLMs for **text generation** (Spanish, French, German, etc.).  |
| **Anthropic**    | Claude 3                | Powerful **Claude models** with options for **intelligence, speed, and cost balance.**  |
| **Cohere**       | Command & Embed         | **Text generation for business** + embeddings for search, clustering, classification.  |
| **Meta**         | Llama                    | Ideal for **chat interfaces, virtual assistants, language translation.**  |
| **Mistral AI**   | Mistral / Mixtral       | Supports **Synthetic Text Generation, Code Generation, RAG, and Agents.**  |
| **Stability AI** | Stable Diffusion (SDXL) | **Text-to-image model** for generating **realistic, high-quality images, art, and logos.**  |

---

## **📌 Inference Parameters**  

When interacting with FMs, **adjust inference parameters** to **customize responses.** Modify **one parameter at a time** for better control over outputs.  

### **🔹 Randomness & Diversity Controls**  
| **Parameter** | **Function** | **Min** | **Max** | **Default** |
|--------------|------------|--------|--------|---------|
| **Temperature** | Adjusts randomness in word choice. Lower = **predictable**, higher = **creative.** | 0 | 1 | 0 |
| **Top K** | Limits choices to the **K most probable words.** Lower = **more conservative responses.** | — | — | — |
| **Top P** | Cuts off low-probability words based on **cumulative probability.** Tightens response distribution. | 0 | 1 | 1 |

---

### **🔹 Length Controls**  
| **Parameter**       | **Function** | **Min** | **Max** | **Default** |
|--------------------|------------|--------|--------|---------|
| **Response Length** | Sets **min & max token limits** on response size. | 0 | 8,000 | 512 |
| **Length Penalty** | Encourages **concise responses** by penalizing overly long outputs. It sets a soft limit on size. | — | — | — |
| **Stop Sequences** | Defines **specific tokens** that signal **early termination** of response generation  when encountered. | — | — | — |