# VitaChat

VitaChat is an end-to-end Retrieval-Augmented Generation (RAG) system for Medicare policy question answering, built on CMS policy documents (NCD, LCD, and Medicare manuals).

## Repository Description

Notebook-first healthcare RAG project with chunking, FAISS retrieval, reranking, fine-tuning, and a FastAPI + React demo app.

## What This Repo Contains

- `1_Chunking.ipynb`: document chunking and corpus creation
- `2-3_Embeddings_FAISS_till_reranking.ipynb`: embeddings, FAISS indexing, and retrieve-rerank pipeline
- `4_Fine_Tuning_and_Evaluation.ipynb`: bi-encoder/reranker fine-tuning and retrieval evaluation
- `llm_answer_synthesis.ipynb`: answer generation/synthesis experiments
- `all_chunks.json`: chunk corpus used by retrieval
- `faiss_index/`: FAISS artifacts and metadata
- `backend/`: FastAPI API for retrieval + answer generation
- `frontend/`: React + Vite web interface
- `main.tex`: project report source

## Project Workflow

1. Build structured chunks from Medicare source docs.
2. Encode chunks with `BAAI/bge-base-en-v1.5`.
3. Build FAISS index and retrieve top-k candidates.
4. Rerank with `BAAI/bge-reranker-v2-m3`.
5. Optionally fine-tune bi-encoder and reranker.
6. Evaluate with retrieval metrics (Recall@k, MRR).
7. Serve through backend + frontend app.

## Quickstart

### 1) Backend

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

### 2) Frontend

```bash
cd frontend
npm install
npm run dev
```

Optional environment variable:

- `VITE_API_BASE_URL` (default: `http://127.0.0.1:8000`)

## API Endpoints

- `GET /health`
- `POST /chat`

Example request:

```json
{
  "message": "Does Medicare cover acupuncture for chronic low back pain?"
}
```

## Notes

- If FAISS or sentence-transformers dependencies are unavailable, backend may fall back to lexical retrieval.
- Fine-tuning notebooks are compute-heavy and are best run on a GPU runtime.

