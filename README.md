# crdc-ctdc-starter-kit

## Components:

Frontend [?]: Represents the user interface and client-side of the web application.  
Backend [crdc-ctdc-backend] : Represents the server-side of the web application, responsible for handling business logic and communicating with databases.  
Data Loader [icdc-dataloader] : A service responsible for loading data into databases.  
Neo4j Database: A graph database used to store and manage data.  
OpenSearch Database: A search engine/database used to store and index data.  
JSON Data: Represents the data in JSON format, which needs to be loaded into the databases.  
IndexFile: A file containing information needed to index data in the OpenSearch database.  


## Communication Flow:

The Frontend communicates with the Backend using GraphQL. GraphQL is a query language for APIs that allows the Frontend to request specific data from the Backend. 
The Backend communicates with both the Neo4j and OpenSearch databases to perform queries and handle responses. The Backend is responsible for orchestrating data retrieval and storage.  
The JSON Data is used to load data into the Data Loader service, which is responsible for processing and preparing the data for storage in the databases.  
The Data Loader service is connected to both the Neo4j and OpenSearch databases. It loads the processed data into the Neo4j database.  
Additionally, the Data Loader service uses the IndexFile to help load data from the Neo4j database into the OpenSearch database using the ES Loader (Elasticsearch Loader).   

## System diagram

```mermaid

graph TD
  subgraph Frontend
    F[Frontend]
  end

  subgraph Backend
    B[Backend]
  end

  subgraph Data Loader
    DL[Data Loader]
  end

  subgraph Neo4j Database
    N[Neo4j]
  end

  subgraph OpenSearch Database
    O[OpenSearch]
  end

  subgraph JSON Data
    JSON[JSON Data]
  end

  F -->|GraphQL| B
  B -->|Queries/Responses| N
  B -->|Queries/Responses| O

  JSON -->|Data Loading| DL
  IndexFile -->|ES Loader| O
  DL -->  IndexFile 
  DL -->|Data Loader| N


```
