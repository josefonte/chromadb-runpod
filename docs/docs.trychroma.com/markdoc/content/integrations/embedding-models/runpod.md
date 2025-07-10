---
name: RunPod
id: runpod
---

# RunPod

RunPod is a cloud computing platform built for AI, machine learning, and general compute needs. It provides scalable, high-performance GPU and CPU resources through both Serverless endpoints and dedicated Pods. RunPod's Serverless offering features pay-per-second billing with built-in autoscaling, making it ideal for production embedding model workloads.

Chroma provides a convenient integration with embedding models deployed on RunPod Serverless endpoints. You can deploy popular embedding models or custom fine-tuned models on RunPod and use them seamlessly with ChromaDB.

{% Banner type="tip" %}
Get started quickly by deploying an embedding model like `BAAI/bge-large-en-v1.5` or `sentence-transformers/all-MiniLM-L6-v2` on RunPod Serverless for high-performance, scalable embedding generation.
{% /Banner %}

## Using RunPod models with Chroma

### Python

This embedding function relies on the `runpod` python package, which you can install with `pip install runpod`.

You must set your RunPod API key and provide the endpoint ID of your deployed embedding model.

```python
import os
import chromadb.utils.embedding_functions as embedding_functions

runpod_ef = embedding_functions.RunPodEmbeddingFunction(
    api_key=os.environ["RUNPOD_API_KEY"],  # Optional if RUNPOD_API_KEY env var is set
    endpoint_id="your-endpoint-id-here",
    model_name="BAAI/bge-large-en-v1.5",
    timeout=300  # Optional, defaults to 300 seconds
)

embeddings = runpod_ef(input=["This is my first text to embed", "This is my second document"])
```

### JavaScript

This embedding function relies on the `runpod-sdk` package, which you can install with `npm install runpod-sdk`.

```javascript
import { RunPodEmbeddingFunction } from 'chromadb';

const runpodEf = new RunPodEmbeddingFunction({
  runpod_api_key: process.env.RUNPOD_API_KEY, // Optional if RUNPOD_API_KEY env var is set
  runpod_endpoint_id: "your-endpoint-id-here",
  runpod_model_name: "BAAI/bge-large-en-v1.5",
  runpod_timeout: 300 // Optional, defaults to 300 seconds
});

const embeddings = await runpodEf.generate(["This is my first text to embed", "This is my second document"]);
```

## Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| `api_key` / `runpod_api_key` | Your RunPod API key | `RUNPOD_API_KEY` environment variable |
| `endpoint_id` / `runpod_endpoint_id` | The endpoint ID of your deployed embedding model | Required |
| `model_name` / `runpod_model_name` | The name of the embedding model | Required |
| `timeout` / `runpod_timeout` | Request timeout in seconds | 300 |

## Getting Started with RunPod

1. **Create a RunPod account** at [runpod.io](https://runpod.io)
2. **Deploy an embedding model** using RunPod Serverless
3. **Get your API key** from the RunPod dashboard
4. **Note your endpoint ID** from the deployed endpoint
5. **Use the embedding function** in your ChromaDB application

For more information about deploying models on RunPod, visit the [RunPod documentation](https://docs.runpod.io/overview).
