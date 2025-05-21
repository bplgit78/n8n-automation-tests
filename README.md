# n8n-automation-tests
n8n projects - Json files mostly
This project houses all the n8n automation json files. The files can be loaded into your n8n instance and update/add credential keys.

n8n setup:
You will need to deploy nodejs and if you want to manage multiple versions of nodejs you will also need nvm 
1. node js: https://nodejs.org/en
2. nvm : https://github.com/coreybutler/nvm-windows
3. once both are installed:
    - use this command on your terminal: npm install n8n -g
4. once this deploy is complete
    - in a new terminal.. enter this command: n8n
    - this will start n8n and you will see a link to access it.


Projects: (Low code to no code)
1. vectorize data - RKM_to_pinecone.json
    - step 1 in creating a chat bot: Data is being loaded to pinecone
      - Prerequisites:
        -- you will need a pinecone account and an api key
        -- you will need to create an index on pinecone
        -- ensure you pick an embeddings model while creating the index on pinecone
        -- you will need open ai api key (This will give you access to the open ai embeddings model)
      - When a new file is added to the google drive, the workflow is triggered
      - initiate a "download file" operation on the google drive
      - the downloaded file will then be vectorized to pinecone vector store (You will have to create a pinecone index before this step runs in the workflow)
      - The pine cone vector store node needs an embeddings model to ensure we are creating embeddings that match the index on pinecone
      - A default data loader is needed here to ensure that the data being written to pinecone is in the right format.
      - A text splitter is also needed to ensure the data is being chunked into right size and the chunk overlap is appropriate
     
2. A RAG based chatbot that will answer questions based on vectorized data in project 1 - RKM_RAG_chatbot.json
   - A user can interact with the chat bot and ask questions. This will trigger the work flow
   - The AI agent uses:
     - open ai chat model to interpret the original message from the user
     - simple memory node will hold on to historical messages in that session which will be the context window
        - the RKM InvestorsQA node is a "vector store question answer node"
            - this node will connect to the pinecone vector db
              - this vector db node will also need the right embeddings that were used to create the embeddings
         - this node also needs an open ai chat model that will interpret the information retrieved from pinecone and use it to build responses that will be shown to the user
     - Finally a google sheet is attached to this AI agent so any lead information in the chat can be stored and can be used by subsequent workflows for marketing emails
     - This can be enhanced further to make it usable on any website.


        
