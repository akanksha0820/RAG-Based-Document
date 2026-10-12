# \# RAG-Based Document Intelligence System

# 

# An AI-powered PDF chatbot built using \*\*Python, LangChain, Google Gemini, ChromaDB, Hugging Face, and Streamlit\*\*.

# 

# Users can upload PDF documents, ask questions about their content, and receive AI-generated answers and recommendations using \*\*Retrieval-Augmented Generation (RAG)\*\*.

# 

# \## Features

# 

# \- \*\*PDF Chatbot:\*\* Upload a PDF and ask questions about its content.

# \- \*\*AI Recommendations:\*\* Get suggestions and insights based on the document.

# \- \*\*Semantic Search:\*\* Retrieve relevant information using ChromaDB and MMR.

# \- \*\*Page References:\*\* View the source pages used to generate answers.

# \- \*\*Local Embeddings:\*\* Use Hugging Face embeddings without an external embedding API.

# \- \*\*Interactive UI:\*\* Chat with documents using Streamlit.

# 

# \## Tech Stack

# 

# | Technology | Purpose |

# |---|---|

# | Python | Backend programming |

# | Streamlit | Web interface |

# | Google Gemini | AI-generated responses |

# | LangChain | RAG pipeline |

# | Hugging Face | Text embeddings |

# | ChromaDB | Vector database |

# | PyPDFLoader | PDF text extraction |

# 

# \## How It Works

# 

# 1\. \*\*Upload PDF:\*\* The user uploads a PDF through Streamlit.

# 2\. \*\*Extract Text:\*\* PyPDFLoader reads the document.

# 3\. \*\*Split Text:\*\* LangChain divides the text into smaller chunks.

# 4\. \*\*Create Embeddings:\*\* Hugging Face converts the chunks into vectors.

# 5\. \*\*Store Vectors:\*\* ChromaDB stores the document embeddings.

# 6\. \*\*Retrieve Context:\*\* MMR search finds relevant chunks for the user's question.

# 7\. \*\*Generate Response:\*\* Google Gemini generates an answer using the retrieved context.

# 8\. \*\*Display Answer:\*\* Streamlit shows the response with source page references.

# 

# \## Installation

# 

# \*\*1. Clone the repository\*\*

# 

# ```bash

# git clone https://github.com/akanksha0820/RAG-Based-Document.git

# cd RAG-Based-Document

# ```

# 

# \*\*2. Install dependencies\*\*

# 

# ```bash

# pip install -r requirements.txt

# ```

# 

# \*\*3. Configure the API key\*\*

# 

# Create a `.env` file in the project folder:

# 

# ```env

# GOOGLE\_API\_KEY=your\_google\_api\_key\_here

# ```

# 

# Get your API key from \[Google AI Studio](https://aistudio.google.com/).

# 

# Never upload your actual `.env` file to GitHub.

# 

# \*\*4. Run the application\*\*

# 

# ```bash

# python -m streamlit run app.py

# ```

# 

# Open `http://localhost:8501` in your browser.

# 

# \## Example Questions

# 

# \- What is this document about?

# \- Summarize the key findings in this PDF.

# \- What are the main challenges discussed?

# \- Suggest three improvements based on this document.

# \- What recommendations would you make based on the findings?

# 

# \## RAG Configuration

# 

# | Parameter | Value |

# |---|---|

# | Chunk Size | 1,000 characters |

# | Chunk Overlap | 200 characters |

# | Embedding Model | all-MiniLM-L6-v2 |

# | Embedding Dimensions | 384 |

# | Vector Database | ChromaDB |

# | Retrieval Method | MMR |

# | Retrieved Chunks | Up to 6 |

# | LLM | Google Gemini |

# 

# \## Current Limitations

# 

# \- Supports one PDF at a time.

# \- Works best with text-based PDFs.

# \- Chat history is displayed but is not used as conversational memory.

# \- Gemini requires an API key and internet connection.

# 

# \## Future Improvements

# 

# \- Support multiple PDF uploads.

# \- Add conversational memory.

# \- Support scanned PDFs using OCR.

# \- Deploy the application online.

# 

# \## Project Status

# 

# \*\*Working local prototype\*\* with PDF question answering, semantic retrieval, source references, and AI-powered recommendations.

