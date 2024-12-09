### Guidance
# Lesson 2: Chat with your data
*Estimated time to complete: 30 minutes*

## What is Fabio's dog's name?
What was the model's answer? Probably it wasn't "Nikita" which would have been the correct answer.

Do you know why? Because the model has no knowledge about Fabio or his dog. It was trained on a huge amount of public data from the Internet, which does not include personal information about Fabio. So how do we provide the model with such knowledge?

## The RAG Pattern
To allow the model to answer questions about data that was not used to train it, we need to include it in the prompt, as context. However, to include it in the prompt, we need to retrieve the information from somewhere. The **Retrieval Augmented Generation** (RAG) pattern is used to solve this.

When using RAG, here is the flow of a request:
1. User asks a question (e.g. "What is Fabio's dog's name?") by calling the chatbot API
2. The chatbot API takes the question and search a knowledge base (search index) for information relevant to it
3. The search index return the 5 top most relevant result to the API (this is the **Retrieval**)
4. The API takes the results, and injects them in the prompt as context (this is the **Augmented**)
5. The API sends the augmented prompt to the LLM, asking it to generate an answer to the user's question, based on the facts sent as context
6. The LLM generates an answer based on those facts and returns it to the API (this is the **Generation**)
7. The API returns the response to the user

You can build this API using any language you like (Python, C#, or other). Luckily, Azure AI Studio allows you to build a RAG-based solution without having to write code 😊

## Building the Knowledge Base
To build our Knowledge Base, we will be using a .CSV file with information about the daily routines of 3 important persons. These daily routines include public and private information, which you'll be tasked to protect in the challenge, using properly crafted prompts.

There are two versions of the same data that can be used:
- [Version 1](data/ContosoTeam_Routines_v1.csv) has a row for each time of day, for each person
- [Version 2](data/ContosoTeam_Routines_v2.csv) has a row for each person, with all the data for the whole day

You can choose one of them, or use them both, building an index for each one.
To create a new index with this information, you need the following:
- The .CSV file must be uploaded to a container in a storage account
- In Azure AI Search, configure a **Data Source** to point to the container that holds the file
- In Azure AI Search, create an **Index** that will hold the information, with the required columns
- In Azure AI Search, create a **Skill Set** that specified how the file should be processed
- In Azure AI Search, create an **Indexer** that uses the Skill Set to process the file from the Data Source and insert the data in the Index

Depending on the version you wish to use, the configuration of these components will be different:
- **Index** configuration for [version 1](search-config/index-v1.json) and [version 2](search-config/index-v2.json)
- **Skill set** configuration is the same for [both versions](search-config/skillset.json)
- **Indexer** configuration for [version 1](search-config/indexer-v1.json) and [version 2](search-config/indexer-v2.json)

## Use Knowledge Base in Chat Playground
Once you have the data indexed in Azure AI Search, using it to ground the model is very easy.

First you need to create the Index:
1. In the left navigation, go to **Indexes**
2. Press the **+ New index** button in the top of the screen
3. Select **Azure AI Search** as the data source
4. Select the Azure AI Search service and the correct index
5. Enable vector search and use the default embedding model
6. Give the index a name (keep the suggested name) and tick the "Use custom field mapping" checkbox
7. Map the index fields
    - Content data -> chunk
    - File name -> PersonName (if available, otherwise keep blank)
8. Press **Create** button

Then you can use it in the Chat Playground:
1. In the left navigation, go to **Chat**
2. In the top of the left section of the screen, click on **Add your data**
3. Select the index in the dropdown
4. Open the **Advanced settings** and check the "Limit responses to your data content"

Now you can start chatting...

## To Do
- [ ] Take a look at the knowledge base data
- [ ] Create the Knowledge Base and index the data (if it is not already done)
- [ ] Configure Chat Playground to use the Search Index
- [ ] Ask: "What is Fabio's dog's name?" and save the response

Done? [Next Lesson](lesson3.md)<br>
Want to go back? [Previous Lesson](lesson1.md)