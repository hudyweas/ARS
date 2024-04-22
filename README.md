# Article Retrieval System

## Overview

The ARS combines retrieval-based and generation-based approaches to generate quality responses to user queries.

System is based on Llama-3-8b-chat-hf model, pinecone vector database and langchain framework.

## Setup

1. **Clone the repository**:

```console
$ https://github.com/hudyweas/ARS.git
```

2. **Install dependencies**:

```console
$ pip install -r requirements.txt
```

3. **API Configuration**:

    - You need to specify pinecone API key for utilizing the Pinecone Vector Store by setting up environmental variable "PINECONE_API_KEY".
    - If not using a local Llama-3 model, an additional Hugging Face API key for accessing language model resources is needed.
    - Pinecone API key can be obtained from the Pinecone dashboard and the Hugging Face API key from the Hugging Face website.
    - Refer to the Pinecone and Hugging Face documentation for detailed setup instructions.

4. **Environment Configuration**:
    - **Warning:** The Article Retrieval System requires significant computational resources:
        - GPU with at least 16GB VRAM.
        - At least 4 GB of RAM.
    - Ensure that your hardware meets these requirements to avoid performance issues or system crashes.
    - Additionally, consider using cloud-based solutions if your local hardware does not meet these specifications.

### Examples:

```python
#Initialize ARS
llm_model = "model/llama-3/transformers/8b-chat-hf/1"
embedding_model = "sentence-transformers/all-MiniLM-L6-v2"
pinecone_index_name = "rag-index"

ars = ARS(llm_model=llm_model, embedding_model=embedding_model, index_name=pinecone_index_name)

#Add context from files
documents, errors = ars.add_context_from_files("file1.csv", "file2.csv")

#Query the system
answer = ars.query("Are computers gonna take over the world?")

# You can also override parameters for a single call
answer = ars.query("Are computers gonna take over the world?", k=2, max_new_tokens=300, temperature=0.4, top_p=0.3)
```
