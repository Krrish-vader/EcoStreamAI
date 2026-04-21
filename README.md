# EcoStream AI

## Quick Start (New Teammates)
1. Clone and enter project folder.
2. Create .env from .env.example and fill values.
3. Start services:
	 docker compose up --build -d
4. Build local vector store:
	 docker exec ecostream_backend python rag/ingest.py
5. Verify API health:
	 http://localhost:8000/health

## Setup
1. Clone the repo.
2. Copy .env.example to .env and fill in your values.
3. Start services:
	 docker compose up --build -d
4. Verify backend health:
	 http://localhost:8000/health
5. Build local vector store from TXT corpus:
	 docker exec ecostream_backend python rag/ingest.py

## Corpus and Vector Store Policy
- TXT files inside pdfs are pushed to git and treated as the source corpus.
- Non-TXT files inside pdfs are ignored.
- chroma_store is not pushed to git.
- Running the ingest command creates and populates chroma_store automatically on each machine.

## Database Initialization
- No manual init script is required now.
- The database schema is created automatically from backend/db/init.sql when the Postgres volume is created for the first time.
- If you need a clean reset:
	1. docker compose down -v
	2. docker compose up --build -d

## Post-Push Update Steps (All Members)
1. Save local work and commit or stash any local changes.
2. Pull latest changes from your branch or main.
3. Rebuild and restart containers:
	 docker compose up --build -d
4. Verify services are running:
	 docker ps
5. Rebuild local vector store from latest TXT corpus:
	 docker exec ecostream_backend python rag/ingest.py
6. Verify backend responds:
	 open http://localhost:8000/health



