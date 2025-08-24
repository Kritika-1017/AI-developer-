# AI Developer Assignment Implementation

This project implements a simple PDF Retrieval-Augmented Generation (RAG) system.

## Features

- Upload multiple PDF files
- Extract text per page with PyMuPDF
- Chunk text and store embeddings in ChromaDB (persistent local store)
- Generate embeddings with SentenceTransformers (`all-MiniLM-L6-v2` by default)
- Query using natural language; retrieve top-k chunks and optionally synthesize an answer via OpenAI (if `OPENAI_API_KEY` is set)
- React UI for upload and querying in `Document Q&A`
- Shows sources with file name, page number, and similarity

## Tech Stack

- Frontend: React + Vite + Tailwind (existing site) with a new `DocumentQA` component
- Backend: FastAPI
- PDF parsing: PyMuPDF
- Embeddings: sentence-transformers
- Vector DB: ChromaDB (local persistent)
- Optional LLM: OpenAI Chat Completions

## Getting Started

### Backend

1. Create a virtual environment and install dependencies:

```bash
cd project/server
python -m venv .venv
.venv\\Scripts\\activate  # Windows PowerShell
pip install -r requirements.txt
```

2. Run the server:

```bash
uvicorn main:app --reload --port 8000
```

Optional env vars:

- `OPENAI_API_KEY`: enables LLM answer synthesis
- `OPENAI_MODEL`: defaults to `gpt-4o-mini`
- `CHROMA_DIR`: persistence directory for Chroma (defaults to `server/chroma_db`)
- `FRONTEND_ORIGIN`: CORS origin (defaults to `http://localhost:5173`)

### Frontend

```bash
cd project
npm install
npm run dev
```

Open `http://localhost:5173`, navigate to `Document Q&A` in the header.

## Notes

- Queries use documents only; when OpenAI is not configured, the top retrieved chunk is returned.
- Ingestion stores per-page chunks; you can re-upload to append more.
- This is a minimal reference implementation; add auth and rate limiting for production.

