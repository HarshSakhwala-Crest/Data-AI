# **Amazon Bedrock Methods**

Amazon Bedrock provides a suite of APIs that allow users to interact with foundation models, configure settings, and execute inference tasks within AWS environments. These APIs are categorized into **setup and configuration APIs** and **runtime APIs**.

---

## **📌 Amazon Bedrock Setup & Configuration APIs**

### **🔹 ListFoundationModels**
This API returns a list of foundation models available in Amazon Bedrock.

#### **🖥 Example: Listing Foundation Models**
```python
%pip install --upgrade boto3
import boto3
import json

bedrock = boto3.client(service_name='bedrock')
model_list = bedrock.list_foundation_models()
for x in range(len(model_list.get('modelSummaries'))):
     print(model_list.get('modelSummaries')[x]['modelId'])
```

#### **📝 Sample Output**
```text
amazon.titan-tg1-large
amazon.titan-image-generator-v1:0
amazon.titan-text-express-v1
anthropic.claude-3-sonnet-20240229-v1:0
mistral.mixtral-8x7b-instruct-v0:1
meta.llama3-70b-instruct-v1:0
```

---

## **📌 Amazon Bedrock Runtime APIs**

### **🔹 InvokeModel**
This API invokes a specific foundation model for inference tasks.

#### **🖥 Example: Running Inference on a Text Model**
```python
import boto3
import json

bedrock_rt = boto3.client(service_name='bedrock-runtime')
prompt = "What is Amazon Bedrock?"
configs = {
    "inputText": prompt,
    "textGenerationConfig": {
        "maxTokenCount": 4096,
        "stopSequences": [],
        "temperature": 0,
        "topP": 1
    }
}

body = json.dumps(configs)
modelId = 'amazon.titan-tg1-large'
accept = 'application/json'
contentType = 'application/json'

response = bedrock_rt.invoke_model(
    body=body,
    modelId=modelId,
    accept=accept,
    contentType=contentType
)
response_body = json.loads(response.get('body').read())
print(response_body.get('results')[0].get('outputText'))
```

#### **📝 Sample Output**
```text
Amazon Bedrock is a managed service that makes foundation models from leading AI startups and Amazon's own Titan models available through APIs.
```

---

### **🔹 InvokeModelWithResponseStream**
This API invokes a model to run inference using the input provided. It returns the response in a stream.

#### **🖥 Example: Streaming Text Generation**
```python
prompt = "Write an essay for living on Mars using 10 sentences."
configs = {
    "inputText": prompt,
    "textGenerationConfig": {
        "temperature": 0
    }
}

body = json.dumps(configs)
accept = 'application/json'
contentType = 'application/json'
modelId = 'amazon.titan-tg1-large'

response = bedrock_rt.invoke_model_with_response_stream(
    modelId=modelId,
    body=body,
    accept=accept,
    contentType=contentType
)

stream = response.get('body')
if stream:
    for event in stream:
        chunk = event.get('chunk')
        if chunk:
            print((json.loads(chunk.get('bytes').decode())))
```

#### **📝 Sample Output**
```json
{"outputText": "Living on Mars would be an incredible adventure. The planet is known for its red deserts, vast canyons, and unique geological features."}
```

---

### **🔹 Converse API**
This API provides a consistent interface for interacting with conversational AI models.

#### **🖥 Example: Using Converse API for Q&A**
```python
import boto3

client = boto3.client("bedrock-runtime")
model_id = "amazon.titan-tg1-large"

# Inference parameters
inference_config = {"temperature": 0.5, "topP": 0.9}

# System prompt & conversation setup
system_prompts = [{"text": "You are a helpful assistant. Please answer the query politely."}]
conversation = [
    {"role": "user", "content": [{"text": "Hello, what is the capital of France?"}]}
]

# Invoke Converse API
response = client.converse(
    modelId=model_id,
    messages=conversation,
    inferenceConfig=inference_config
)

print(response['output']['message']["content"][0]["text"])
```

#### **📝 Sample Output**
```text
Hello, the capital of France is Paris. It is also the country's biggest city.
```