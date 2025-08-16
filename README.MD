# COMP-377 Lab 5 – Full‑Stack Agentic RAG (Working Baseline)

This project contains a **Flask + LangGraph** backend and a **React (Vite)** frontend.

## 1) Prerequisites
- Python 3.10+
- Node.js 18+ / npm or yarn
- An OpenAI API key

## 2) Environment
Copy `.env.template` to `.env` (at repo root) and set values:
```
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4o-mini
```

## 3) Backend – setup & run
```bash
cd backend
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python app.py
```
This starts Flask on **http://localhost:5000**.

> On first run, the vector store is built from `data/*.txt` and persisted to `backend/chroma_db/`.

## 4) Frontend – setup & run
```bash
cd frontend/my-chat
npm install
npm run dev
```
Open the printed URL (usually http://localhost:5173). The app calls the backend at `http://localhost:5000/api/chat`.

## 5) How it works
- **Vector store**: Chroma with OpenAI embeddings (`text-embedding-3-small`), built from files in `data/`.
- **LangGraph** pipeline:
  1. `retrieve` → fetch top-k chunks relevant to the latest user question.
  2. `generate` → LLM answers, citing context snippets like `[1]`.
  3. `summarize` → creates a short memory summary of the conversation (returned to the UI).
- **/api/chat** accepts `{ message, history }` and returns `{ reply, history, memory_summary }`.

## 6) Notes
- Keep your real API key **out of source control**. Commit only `.env.template`.
- If embeddings schema changes, delete `backend/chroma_db/` and rerun.
- To switch LLMs, set `OPENAI_MODEL` in `.env`.

## 7) Packaging for submission
Zip the following as `YourFullNames_COMP377Lab5.zip`:
- `backend/`, `frontend/`, `data/`, `.env.template`, `README.MD`
- **Do not** include `.venv/` or `node_modules/`.

