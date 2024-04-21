# Article Retrieval System

## Overview

The ARS combines retrieval-based and generation-based approaches to generate quality responses to user queries.

System is based on Llama-3 model, pinecone vector database and langchain framework.

## Dependencies

- **pandas (pd)**
- **torch**
- **transformers**
- **bitsandbytes**
- **accelerate**
- **langchain_experimental**
- **langchain**
- **langchain_community**
- **langchain_pinecone**

## Setup

1. Clone the repository:
```console
$ https://github.com/hudyweas/RAG.git
```

2. Install dependencies:
```console
$ pip install -r requirements.txt
```
3. Follow the instructions in the USAGE section below to use the RAG.

## Configuration

1. **Query Configuration**:
   - Parameters to configure query:
     - max_new_tokens: Limiting the length of generated responses.
     - temperature: Controlling the randomness of generated responses.
     - top_p: Determining the diversity of generated responses.
     - k: The number of documents to retrieve for context.
   - Feel free to tweak these settings to suit your needs.


2. **API Configuration**:
   - For API integration, you need to specify pinecone API key for utilizing the Pinecone Vector Store.
   - If not using a local Llama-3 model, an additional Hugging Face API key for accessing language model resources is needed.
   - Pinecone API key can be obtained from the Pinecone dashboard and the Hugging Face API key from the Hugging Face website.
   - Refer to the Pinecone and Hugging Face documentation for detailed setup instructions.


3. **Environment Configuration**:
   - **Warning:** The Article Retrieval System requires significant computational resources:
     - GPU with at least 16GB VRAM.
     - At least 4 GB of RAM.
   - Ensure that your hardware meets these requirements to avoid performance issues or system crashes.
   - Additionally, consider using cloud-based solutions if your local hardware does not meet these specifications.

## Usage 

1. **Initialization**:
To use the ARS, initialize an instance of the ARS class with the desired parameters, including the path to the language model, the name of the embedding model, the index name and optional parameters.

2. **Adding Context**:
Add context to the system by providing paths to files containing relevant documents. Use the `add_context_from_files()` method to load documents from files and add them to the model's context.

3. **Querying**:
Query the system by providing a query using the `query()` method. The system will generate a response based on the provided context and the query. You can specify additional parameters such as maximum token length, sampling temperature, etc., for customized responses.

### Examples:
Below are examples demonstrating how to initialize the ARS, add context from files, and query the system:

```python
#Initialize ARS
ars = ARS(llm_model="model_path", embedding_model="embedding_model", index_name="index_name")

#Add context from files
documents, errors = ars.add_context_from_files("file1.csv", "file2.csv")

#Query the system
answer = ars.query("query")
```