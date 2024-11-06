# Cybernetyx-s-Assignment

This project implements a lightweight FastAPI server for RAG (Retrieval-Augmented Generation). The server uses ChromaDB’s persistent client for ingesting and querying documents (PDF, DOC, DOCX, TXT) and leverages the sentence-transformers/all-MiniLM-L6-v2 model from Hugging Face for generating embeddings.

Table of Contents
Dependencies
Setup and Installation
Configurations
API Endpoints
Ingest Documents
Query Documents


1. Dependencies
Before setting up the server, make sure you have the following dependencies installed.

pip install -r requirements.txt


Required Python Libraries:
FastAPI: Web framework for building the API.
ChromaDB: A vector database for document storage and retrieval.
sentence-transformers: For generating embeddings from documents using the Hugging Face model all-MiniLM-L6-v2.
pyngrok: To create a public URL for the FastAPI server (especially useful for exposing the local server during development).
python-docx, PyMuPDF: For document parsing (DOCX, PDF).
Uvicorn: ASGI server for running the FastAPI app.


Example requirements.txt:

fastapi
uvicorn
chromadb
sentence-transformers
pyngrok
python-docx
PyMuPDF


2. Setup and Installation

i. git clone https://github.com/your-username/fastapi-rag-server.git
cd fastapi-rag-server

ii. Install the dependencies:
pip install -r requirements.txt

iii. Get your ngrok Authtoken:
If you are using ngrok to expose your FastAPI server publicly, you need to authenticate it with your ngrok account. Follow these steps:

Sign up for an account at ngrok.

After signing up, go to your ngrok dashboard and copy your authtoken.

Run the following command in your terminal to set the authtoken:
ngrok authtoken YOUR_AUTHTOKEN

iv. Run the FastAPI Server:
To run the FastAPI server locally:
uvicorn app.main:app --reload

v. Expose the server using ngrok:
If you want to access the server publicly, use ngrok to tunnel the localhost:

from pyngrok import ngrok

public_url = ngrok.connect(8000)
print(f"FastAPI public URL: {public_url}")


This will print the public URL, which you can use to interact with the API from anywhere.


3. Configurations

ChromaDB Configuration: The server uses ChromaDB for document storage. It is configured by default to use an in-memory database, but you can modify it to use a persistent database (like SQLite) if needed.

ngrok: Ensure you have the correct authtoken configured as described above to expose your FastAPI server publicly.

a. API Endpoints

i. Ingest Documents

Endpoint: POST /ingest
Description: Ingests documents (PDF, DOCX, TXT) into ChromaDB. This endpoint processes the document, generates embeddings, and stores them in the database.

Request Body:
{
  "file": "<file-object>"
}

file: The document file (PDF, DOCX, TXT) to be ingested.


ii. Query Documents
Endpoint: POST /query

Description: Queries the ChromaDB for documents related to a given query. This endpoint uses the sentence-transformers model to generate query embeddings and performs the retrieval from the database.

Request Body:
{
  "query": "What is the capital of France?"
}

query: The text query to search the documents for relevant information.

