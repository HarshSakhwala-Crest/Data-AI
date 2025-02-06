# **Using Amazon Bedrock FMs for Inference**  

Amazon Bedrock allows developers to **work with a variety of foundation models (FMs)**, each optimized for different generative AI tasks like **text generation, summarization, embeddings, and image generation**.  

---

## **📌 Amazon Titan Models**  

Amazon Titan models support **text generation, text embeddings, and multimodal embeddings**.  

### **🔹 Amazon Titan Text**  
- Tasks: **Summarization, text generation, classification, Q&A, info extraction**  
- Supports **structured outputs** like **tables, JSON, CSV**  
- **Unique Parameters:**  
  - **Stop sequences:** Define custom **stop points** for output  
  - **MaxTokenCount:** Limit response length  

**🖥 Example API Call**  

{
  "inputText": "<prompt>",
  "textGenerationConfig": {
    "maxTokenCount": 512,
    "stopSequences": [],
    "temperature": 0.1,
    "topP": 0.9
  }
}

### **🔹 Amazon Titan Text Embeddings**
Converts text into numerical embeddings for search & personalization
Supports different vector dimensions (256, 512, 1024)

**🖥 Example API Call**  

{
    body = json.dumps({"inputText": <prompt>,
"dimensions": <256   512   1024>,
"normalize": True   False,
})
    model_id = 'amazon.titan-embed-text-v2:0'
    accept = 'application/json'
    content_type = 'application/json'

    response = bedrock_runtime.invoke_model(
         body=body,
         modelId=model_id,
         accept=accept,
         contentType=content_type )

    response_body = json.loads(response['body'].read())
    embedding = response_body.get('embedding')
}

### **🔹 Amazon Titan Multimodal Embeddings**
Supports image-text embeddings
Enables image search by text or similar images

**🖥 Example API Call**  

{
   body = json.dumps({"inputText": <prompt>,
       "inputImage": <image>,
       "embeddingConfig":  { "outputEmbeddingLength":  <output_embedding_length> }
})
   model_id = 'amazon.titan-embed-image-v1'
   accept = 'application/json'
   content_type = 'application/json'

   response = bedrock_runtime.invoke_model(
        body=body,
        modelId=model_id,
        accept=accept,
        contentType=content_type )

   response_body = json.loads(response.get('body').read())
   embedding = response_body.get('message')
}

### **🔹 Amazon Titan Image Generator (v1 & v2)**
v1: Text-to-image, inpainting (fill missing areas), outpainting (extend image boundaries).
v2: Adds reference images for layout and background removal.


## **📌 AI21 Labs Jurassic-2 Models(Mid and Ultra)**
Supports text generation & summarization with unique repetition penalties.

Parameter |	Function
**Max completion length(maxTokens)** |	Limits response size
**Stop sequences (stopSequences)** | Configure stop sequences that the model recognizes and after which it stops generating further tokens.
**Presence penalty(presencePenalty)** |	Reduces repetition of previously used words
**Count penalty(countPenalty)** |	Reduces token repetition based on count
**Frequency penalty(frequencyPenalty)** |	Reduces token repetition proportional to frequency
**Penalize special tokens** |   
**Whitespaces (applyToWhitespaces)**: A true value applies the penalty to white spaces and new lines.
**Punctuations (applyToPunctuation)**: A true value applies the penalty to punctuation.
**Numbers (applyToNumbers)**: A true value applies the penalty to numbers.
**Stop words (applyToStopwords)**: A true value applies the penalty to stop words.
**Emojis (applyToEmojis)**: A true value excludes emojis from the penalty.

**🖥 Example API Call**  

{
  "prompt": "<prompt>",
  "maxTokens": 200,
  "temperature": 0.5,
  "topP": 0.5,
  "stopSequences": [],
  "countPenalty": {"scale": 0.0},
  "presencePenalty": {"scale": 0.0},
  "frequencyPenalty": {"scale": 0.0}
}

### **Jamba-Instruct**
Jamba-Instruct offers a 256K context window for text generation, summarization, and question answering tasks for the enterprise.

To call the AI21 Labs Jamba-Instruct model, you can use either invoke_model or converse API.

Input with invoke_model:

response = bedrock.invoke_model(
modelId='ai21.jamba-instruct-v1:0',
body=json.dumps({
'messages': [
{ 'role': 'user',
'content': <prompt>
}
],
})
)

Input with converse

response = bedrock.converse(
modelId='ai21.jamba-instruct-v1:0',
'messages': [
{ 'role': 'user',
'content': [{'text':<prompt>}]
}
],
)

## **📌 Anthropic Claude Models**
Claude models are optimized for conversational AI, summarization, and creative content generation.

### **🔹 Claude Messages API**
Designed for chat-based interactions
Supports multi-turn conversations
In Anthropic Claude Messages API, each input message must be an object with a role and content.

**🖥 Example API Call**  

[
  {"role": "user", "content": "Hello there."},
  {"role": "assistant", "content": "Hi, I'm Claude. How can I help you?"},
  {"role": "user", "content": "Can you explain LLMs in plain English?"}
]

### **🔹 Claude Converse API**
The Converse API provides a unified set of parameters that work across all models that support messages.

## **📌 Stability AI (Stable Diffusion XL - SDXL)**
Text-to-image model
Supports inpainting (fix missing parts) & outpainting (extend image boundaries)
Parameter |	Function
**Prompt strength (cfg_scale)** |	Determines how closely image follows prompt
**Generation steps (steps)** |	More steps = better image quality
**Seed(seed)** |	Ensures repeatable outputs

**🖥 Example API Call** 

{
  "text_prompts": [{"text": "A futuristic city at sunset", "weight": 1.0}],
  "height": 512,
  "width": 512,
  "cfg_scale": float,
  "clip_guidance_preset": string,
  "sampler": string,
  "samples",
  "seed": int,
  "steps": int,
  "style_preset": string,
  "extras" : JSON object
}

## **📌 Cohere Command Model**
Optimized for business tasks like summarization, copywriting, extraction.
Emphasizes security & compliance (SOC 2 certified).
Parameter |	Function
**Return likelihoods(return_likelihoods)** |    Returns token probabilities (
**GENERATION**: This option only returns likelihoods for generated tokens.
**ALL**: This option returns likelihoods for all tokens.
**NONE**: This option doesn’t return any likelihoods. This is the default option.
)
**Stream(stream)** |	Specify true to return the response piece by piece in real time and false to return the complete response after the process finishes.

**🖥 Example API Call**

{
  "prompt": "Summarize this article.",
  "temperature": 0.7,
  "p": float,
  "k": float,
  "max_tokens": 300,
  "stop_sequences": ["###"],
  "return_likelihoods": "GENERATION|ALL|NONE",
  "stream": boolean,
  "num_generations": int
}

## **📌 Summary**
Amazon Bedrock provides a diverse set of foundation models for text, embeddings, and image generation. By adjusting inference parameters, users can fine-tune responses to balance creativity, relevance, and efficiency. 🚀