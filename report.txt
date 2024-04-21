# System Design and Technologies Report: Building an Article Retrieval System

## Introduction
The Article Retrieval System (ARS) is designed to provide users with a sophisticated tool for retrieving relevant articles based on user queries. This report delves into the design of the ARS, the technologies chosen for its implementation, challenges encountered during development, and potential areas for future development.

## System Design
The ARS architecture follows a retrieval-augmented generation approach, combining retrieval-based and generation-based techniques. The system is split into two main components. The first one takes care of all the logic, retrieving and generating, and the second one of loading context from files.

After the context is loaded, it's embedded and stored in a vector database. When the user asks the query, it's embedded by the same model and using similarity search the most similar k articles are retrieved. After that Llama-3 takes care of generating quality output and answering the question based on the retrieved context.

## Technologies Selected
- **Llama-3:** I selected this model due to its exceptional performance and superiority over other models of similar size and because it's free to use.
- **Pinecone Vector Store:** One huge advantage using Pinecone was possibility to upgrade similarity search to hybrid search. Despite that Pinecone has very good performance and is free on basic plan.
- **Langchain:** It was a tough choice between Langchain and Llama-index. I chose Langchain because it's more universal in the context of future development than Llama-index.
- **Semantic Splitter:** The basic approaches of splitting texts are very archaic. Splitting text based on the meaning is more human-like, it's more logical to do. It gives less chance to cut the sentences or separate ones that make a context with each other.

## Challenges Encountered
The main challenge was to choose the proper technologies and parameters to find the balance between performance and quality.
For example, should I choose a semantic splitter which needs way more computations than a basic splitter? Is a more advanced embedding model worth slowing down the system on multiple levels?

## Potential Areas for Future Development
- **More supported extensions:** Currently, the system supports only CSV files as it was the dataset. Despite that system is designed to easily add any file extension as supported.

- **Hybrid search:** Hybrid search can be a huge step into retrieving higher quality documents based on the user query. It means leaving serverless architecture, but it's worth testing if it is worth the results.

- **Preprocessing:** Currently, documents are not preprocessed, but it may be a good development area.