📘 Project Name: Academy Assistant

A multilingual virtual assistant designed for the needs of students and staff at a higher education institution.
It combines Retrieval-Augmented Generation (RAG) with multi-agent orchestration to provide accurate, structured, and context-aware academic support.

⸻

🚀 Overview

Academy Assistant delivers:

 •	Structured Q&A for exam schedules, academic deadlines and information about exams
	
 •	Informational responses about general information about the institution
	
 •	Multilingual support with formal tone and Serbian Latin (Ekavian) script

It blends LLM reasoning with semantic vector search to ensure grounded answers based strictly on available data.

⸻

🧠 Features

•	Example prompts:
	“When is the Programming 101 exam?”
	“What date is the Math final?”

•	Uses semantic search + LLM synthesis for factual answers.

•	Embedding & Vector Search

•	Text embedded with paraphrase-multilingual-MiniLM-L12-v2.

•	Stored in Pinecone with metadata for fast, semantic retrieval.

•	Web Scraping + Chunking

•	Transliterates Cyrillic to Latin.

•	Cleans HTML and removes irrelevant sections.

•	Chunks content using RecursiveCharacterTextSplitter.

•	Short-Term Memory

•	User sessions and chat history stored securely in MySQL.

•	Streamlit Frontend

⸻

✅ Usage

1. Scrape and embed data from the website

python scrapeAndVectorise.py

Scrapes site content, processes and chunks it, embeds it, and uploads vectors to Pinecone.

1.1 Embed local data

python vectorise.py

Embeds text files with options for chunking (sentence-based or delimiter-based).

2. Start the UI app

streamlit run streamlit_app.py

3. Authenticate and chat

Log in using MySQL credentials to access personalized chat sessions.

⸻

⚙️ Environment Variables

GOOGLE_API_KEY=
PINECONE_API_KEY=
PINECONE_INDEX_NAME=
TOP_K=
EMBEDDING_MODEL="text-embedding-3-large"
LLM_MODEL_NAME="gemini-2.0-flash"

⸻

🗄️ Database Schema

CREATE TABLE clients (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE examDates (
    id INT AUTO_INCREMENT PRIMARY KEY,
    predmet VARCHAR(255) NOT NULL,
    profesor VARCHAR(255) NOT NULL,
    datum DATE NOT NULL,
    vise_detalja TEXT
);

CREATE TABLE conversations (
    id CHAR(36) PRIMARY KEY,
    client_id INT NOT NULL,
    chatName VARCHAR(255) NOT NULL,
    messages JSON NOT NULL,
    FOREIGN KEY (client_id) REFERENCES clients(id)
);