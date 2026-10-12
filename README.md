# 📄 RAG-Based Document Intelligence System

**Chat with your PDFs using AI.** A Retrieval-Augmented Generation (RAG) application that answers questions about uploaded documents and provides context-aware recommendations.

Built with **Python · Streamlit · LangChain · Google Gemini · Hugging Face · ChromaDB**.

## ✨ Features

- **Ask questions about PDFs** — get answers grounded in retrieved document content.
- **AI-powered recommendations** — request suggestions informed by the PDF and general AI knowledge.
- **Semantic search** — find relevant passages using vector embeddings and MMR retrieval.
- **Page references** — see which PDF pages were retrieved for a response.
- **Interactive chat** — upload a document, ask questions, review chat history, and inspect retrieved chunks.
- **Local embeddings** — generate embeddings on your computer without an external embedding API.

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Language | Python |
| User interface | Streamlit |
| Language model | Google Gemini (`gemini-3.1-flash-lite`) |
| RAG framework | LangChain |
| PDF extraction | PyPDFLoader |
| Text splitting | RecursiveCharacterTextSplitter |
| Embeddings | Hugging Face (`all-MiniLM-L6-v2`) |
| Vector database | ChromaDB |
| Retrieval | Maximum Marginal Relevance (MMR) |

## 🔄 How It Works

```text
Upload PDF (Streamlit)
         ↓
Extract Text (PyPDFLoader)
         ↓
Split into Chunks (1,000 characters, 200 overlap)
         ↓
Create Local Embeddings (Hugging Face)
         ↓
Store Vectors (ChromaDB)
         ↓
User Question → Retrieve Relevant Chunks (MMR)
         ↓
Generate Answer (Google Gemini)
         ↓
Display Response + Page References (Streamlit)
```

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/akanksha0820/RAG-Based-Document.git
cd RAG-Based-Document
```

### 2. Create a virtual environment (recommended)

**Windows PowerShell:**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Set up your Gemini API key

Get an API key from [Google AI Studio](https://aistudio.google.com/).

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_google_api_key_here
```

> **Security:** Never upload `.env` or your actual API key to GitHub. Add `.env` to `.gitignore`.

### 5. Run the application

```bash
python -m streamlit run app.py
```

Open **http://localhost:8501** in your browser.

## 💬 Example Questions

**Document questions**
- What are the key findings in this PDF?
- Summarize the main challenges discussed.
- Which technologies are mentioned in the document?

**AI-assisted analysis**
- Suggest three improvements based on this document.
- What would you prioritize and why?
- Recommend ways to improve the architecture described in the PDF.

> Recommendations may include general AI knowledge beyond the uploaded document. Verify important suggestions independently.

## ⚙️ Retrieval Settings

| Setting | Value |
|---|---|
| Chunk size | 1,000 characters |
| Chunk overlap | 200 characters |
| Embedding dimensions | 384 |
| Search method | MMR |
| Retrieved chunks (`k`) | 6 |
| Candidate chunks (`fetch_k`) | 15 |

## 📌 Current Limitations

- Processes one PDF at a time in the current interface.
- Text-based PDFs work best; scanned PDFs need OCR support.
- Chat history is displayed but previous messages are not passed to the model as conversational memory.
- Page references identify retrieved passages, not independently verified citations for every claim.
- Requires internet access for Gemini requests and the initial embedding model download.

## 🔮 Future Improvements

- Support multiple PDFs and persistent document collections.
- Add conversational memory for follow-up questions.
- Support scanned PDFs using OCR.
- Add automated evaluation and deployment with Docker.

---

**Project status:** Working local RAG prototype for PDF question answering and AI-assisted recommendations.
