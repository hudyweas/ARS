# System Design and Technologies Report: Building an Article Retrieval System

## Introduction

The Article Retrieval System (ARS) is designed to provide users with a sophisticated tool for retrieving relevant articles based on user queries.

## System Design

The ARS architecture follows a retrieval-augmented generation approach, combining retrieval-based and generation-based techniques.

After the context is extracted from file, it's embedded and stored in a vector database. When the user asks the query, it's embedded by the same model and using similarity search the most similar k articles are retrieved. After that Llama-3 takes care of generating quality output and answering the question based on the retrieved context.

## Technologies Selected

-   **Llama-3:** I selected this model due to its exceptional performance and superiority over other models of similar size and because it's free to use.
-   **Langchain:** I've decided to choose an LLM framework to provide an additional level of abstraction to improve performance and code development. It was a tough choice between Langchain and Llama-index. I chose Langchain because it's more universal in the context of future development than Llama-index. The other reason for using this framework is that it has an implemented Semantic Chunker.
-   **Pinecone Vector Store:** One huge advantage of using Pinecone was the possibility of upgrading the similarity search to a hybrid search. Next to that Pinecone has very good performance and is free on a basic plan which allows scalability without changing the technology.

## Challenges Encountered

The main challenge was to choose the proper technologies and parameters to find the balance between performance and quality.
For example, should I choose a semantic splitter which needs way more computations than a basic splitter? Is a more advanced embedding model worth slowing down the system on multiple levels?

Using a regular splitter gave unsatisfactory results. The text has been split in random places. That's why I decided to use Semantic Chunker. At this point, I encountered another problem. The previous embedding model I were using was taking too much time to split the text, so I decided to change it to a smaller one.

The other big challenge was using Llama. As it is a new model, there are not many sources to learn how to configure the model. In my case, I was struggling with weird Llama behaviour. It turned out it was because of an invalid prompt.

## Potential Areas for Future Development

-   **More supported extensions:** Currently, the system supports only CSV files as it was the dataset. Despite that system is designed to easily add any file extension as supported.

-   **Advanced extracting techniques:** Files are a limited source of data. Adding techniques like WEB Scrapping will add other sources of informations to improve the output.

-   **Hybrid search:** Hybrid search can be a huge step into retrieving higher quality documents based on the user query. Within this development, it is mandatory to choose the target Pinecone architecture as using hybrid search and moving from serverless architecture to pod-based, may end with regression in accuracy.

-   **Preprocessing:** Currently, documents are not preprocessed, but it may be a good development area.
