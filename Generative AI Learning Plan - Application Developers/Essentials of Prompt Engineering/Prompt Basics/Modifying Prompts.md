# **Modifying Prompts**  

## **Why Modify Prompts?**  
Even highly capable **foundation models (FMs)** can produce better outputs with **refined prompts** and **optimized inference parameters.**  

---

## **Inference Parameters**  
Customizing inference parameters influences **creativity, coherence, and length** of AI responses.  

### **1️⃣ Randomness & Diversity**  
- **Temperature:** Controls creativity and makes the output more diverse and unpredictable (0 = deterministic, 1 = highly creative).  
- **Top-P:** Top p is a setting that controls the diversity of the text by limiting the number of words that the model can choose from based on their probabilities. 
- **Top-K:** Top k limits the number of words to the top k most probable words, regardless of their percent probabilities.

### **2️⃣ Length**  
- **Maximum Length:** Limits token count that the model can generate during the inference process to prevent excessive or infinite outputs.  
- **Stop Sequences:** Stop sequences are special tokens or sequences of tokens that signal the model to stop generating further output. 

---

## **Best Practices for Prompting**  

✅ **Be Clear & Concise**  
Prompts should be straightforward and avoid ambiguity.
Bad: *Compute the sum total of the subsequent sequence of numerals: 4, 8, 12, 16.*  
Good: *What is the sum of these numbers: 4, 8, 12, 16?*  

✅ **Include Context**  
Provide any additional context that would help the model respond accurately.
Bad: *Summarize this article: [insert article]*  
Good: *Provide a summary of this article for a blog post: [insert article]*  

✅ **Use Directives for Response Type**  
If you want a particular output form, such as a summary, question, or poem, specify the response type directly.
Bad: *What is the capital?*  
Good: *What is the capital of New York? Provide the answer in a full sentence.*  

✅ **Consider the Output in the Prompt**  
Mention the requested output at the end of the prompt to keep the model focused on appropriate content.
Bad: *Calculate the area of a circle.*  
Good: *Calculate the area of a circle with a radius of 3 inches. Round your answer to the nearest integer.*  

✅ **Start Prompts with a Question**  
Phrase your input as a question, beginning with words, such as who, what, where, when, why, and how.
Bad: *Summarize this event.*  
Good: *Why did this event happen? Explain in three sentences.*  

✅ **Provide Example Responses**  
Use the expected output format as an example response in the prompt. Surround it in brackets to make it clear that it is an example.
Bad: *Determine the sentiment of this post: [insert post]*  
Good: *Determine the sentiment using these examples:  
  - "Great pen!" → Positive  
  - "I hate when my phone battery dies" → Negative  
  - [insert post] → ?*  

✅ **Break Up Complex Tasks**  
- Divide into **subtasks** for better accuracy.  
- Ask the model to **think step-by-step** when handling intricate instructions.  

✅ **Experiment & Be Creative**  
- Try different prompts to optimize the model's responses.

✅ **Use prompt Templates** 
- Prompt templates are predefined structures or formats that can be used to provide consistent inputs to FMs.
- Use **prompt templates** to ensure consistency in interactions.  

---

## **Scenario**  

🚫 **Original Prompt:**  
*"Generate a market analysis report for a new product category."*  

✅ **Updated Prompt (with Best Practices & Parameters):**  
Parameters
Temperature: 0.9
Top p: 0.999
Maximum length: 5,000

Prompt
Generate a comprehensive market analysis report for a new product category in the finance industry for an audience of small and medium-sized businesses (SMBs). Structure the report with the following sections:

1. Executive Summary
2. Industry Overview
3. Target Audience Analysis
4. Competitive Landscape
5. Product Opportunity and Recommendations
6. Financial Projections

The tone should be professional and tailored to the target audience of SMBs.


📌 **Why This Works:**  
- **Optimized Parameters** encourage **creative yet relevant** responses.  
- **Contextual Guidance** (finance industry, SMBs) refines output.  
- **Structured Directives** ensure a well-organized response.  

By applying these best practices, **prompt engineering unlocks the full potential of generative AI.** 🚀  