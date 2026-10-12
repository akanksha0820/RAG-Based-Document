# RAG-Based Document Intelligence System

A **Retrieval-Augmented Generation (RAG)** application that lets users upload PDF documents, ask questions grounded in their contents, and request AI-generated analysis and recommendations. Built with **Python, LangChain, Google Gemini, Hugging Face embeddings, ChromaDB, and Streamlit**.

## Features

* **PDF question answering:** Extract text from uploaded PDFs and answer questions using retrieved document context.
* **AI-powered recommendations:** Generate strategic or technical suggestions using document evidence and the language model's general knowledge, with instructions to distinguish recommendations from document facts.
* **Semantic retrieval:** Search vectorized PDF chunks using ChromaDB and Maximum Marginal Relevance (MMR).
* **Page references:** Display the pages associated with retrieved chunks and instruct the model to cite supporting pages in its responses.
* **Local embeddings:** Generate 384-dimensional embeddings using `sentence-transformers/all-MiniLM-L6-v2`, without calling an external embedding API.
* **Interactive interface:** Upload PDFs, ask questions, view chat history, inspect retrieved chunks, clear the chat, and upload another document.
* **Cached models:** Use Streamlit resource caching to avoid repeatedly initializing the embedding model and LLM client.

## Tech Stack

|Component|Technology|
|-|-|
|Language|Python|
|Web interface|Streamlit|
|LLM|Google Gemini (`gemini-3.1-flash-lite` in the current code)|
|RAG framework|LangChain|
|PDF loading|PyPDFLoader|
|Text splitting|RecursiveCharacterTextSplitter|
|Embeddings|Hugging Face Sentence Transformers (`all-MiniLM-L6-v2`)|
|Vector database|ChromaDB|
|Retrieval|Maximum Marginal Relevance (MMR)|

## Architecture

```text
PDF upload (Streamlit)
       |
       v
PDF text extraction (PyPDFLoader)
       |
       v
Recursive text splitting (1,000 characters; 200 overlap)
       |
       v
Local Hugging Face embeddings (384 dimensions)
       |
       v
ChromaDB vector store
       |
User question --> MMR retrieval (up to 6 chunks)
                       |
                       v
             Retrieved document context
                       |
                       v
             Google Gemini LLM
                       |
                       v
             Answer or recommendation
                       |
                       v
             Streamlit chat interface
```

## Getting Started

### Prerequisites

* Python installed on your computer
* A Google Gemini API key from [Google AI Studio](https://aistudio.google.com/api-keys)
* Internet access for the initial embedding-model download and Gemini API requests

### 1\. Clone the repository

```bash
git clone https://github.com/akanksha0820/RAG-Based-Document.git
cd RAG-Based-Document
```

### 2\. Create a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\\.venv\\Scripts\\Activate.ps1
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3\. Install dependencies

```bash
python -m pip install -r requirements.txt
```

Ensure `requirements.txt` includes `streamlit`, `python-dotenv`, `langchain-community`, `langchain-text-splitters`, `langchain-google-genai`, `langchain-huggingface`, `langchain-chroma`, `sentence-transformers`, and `pypdf`.

### 4\. Configure your Gemini API key

Create a `.env` file in the project root. You can copy `.env.example` if it exists:

**Windows (PowerShell):**

```powershell
Copy-Item .env.example .env
```

**macOS / Linux:**

```bash
cp .env.example .env
```

Set the following value in `.env`:

```dotenv
GOOGLE\_API\_KEY=your\_actual\_google\_api\_key\_here
```

**Never commit your real `.env` file or API key to GitHub.** Add `.env` to `.gitignore`. The `.env.example` file must contain only a placeholder.

### 5\. Run the application

```bash
python -m streamlit run app.py
```

Open the local URL shown in the terminal (usually `http://localhost:8501`).

## How to Use

1. Upload a **text-based PDF** in the Streamlit interface.
2. Wait for the document to be split into chunks and indexed in ChromaDB.
3. Ask a factual question about the document, or request analysis and recommendations.
4. Optionally enable **Show Retrieved Chunks** in the sidebar to inspect retrieved text and page numbers.
5. Use **Clear Chat** to reset the displayed conversation, or **Upload New Document** to replace the PDF.

### Example Prompts

**Document-grounded questions**

* What are the main products described in this document?
* Summarize the operational challenges mentioned in the PDF.
* Which technologies are used, according to the document?

**AI-assisted analysis and recommendations**

* Based on the document, what three changes could improve operational efficiency?
* Suggest improvements to the cloud architecture described in the PDF.
* If you were advising this company, what would you prioritize and why?

The assistant is instructed to distinguish **document facts** from **AI-generated suggestions**. Recommendations are hypothetical and should be evaluated independently.

## Retrieval Configuration

|Parameter|Current value|
|-|-|
|Chunk size|1,000 characters|
|Chunk overlap|200 characters|
|Embedding dimensions|384|
|Retrieval strategy|MMR|
|Retrieved chunks (`k`)|6|
|Candidate chunks (`fetch\_k`)|15|

## Limitations

* Scanned or image-only PDFs are not supported without OCR.
* The app processes one PDF at a time in the current interface.
* Chat messages are displayed in the session, but prior turns are **not** passed to the LLM for conversation-aware follow-up questions.
* Displayed source pages correspond to retrieved chunks; they are not independently verified citations for every generated claim.
* Gemini answer generation requires an API key and remains subject to API quotas and availability.
* The vector store is created for the active session rather than configured for persistent storage.

## Security

Keep secrets and local artifacts out of version control. A recommended `.gitignore` includes:

```gitignore
.env
.env.\*
!.env.example
.venv/
venv/
\_\_pycache\_\_/
\*.pyc
.streamlit/secrets.toml
chroma\_db/
chroma.sqlite3
```

If an API key was ever committed to a public repository, revoke it and create a replacement. Adding `.gitignore` does not remove previously committed secrets from Git history.

## Future Improvements

* Add conversation-aware retrieval for follow-up questions.
* Support multiple PDFs and persistent document collections.
* Add OCR support for scanned documents.
* Build automated evaluations for retrieval quality, factual accuracy, and latency.
* Add a FastAPI backend and Docker deployment.

## Project Status

Local Streamlit RAG prototype with document retrieval, Gemini-powered responses, and AI recommendation prompts.

