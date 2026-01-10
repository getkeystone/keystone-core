# Keystone Core

RAG engine for on-premise knowledge retrieval with permission-aware vector search.

## What This Does

**Ingestion Pipeline:**
- Connects to source systems (SharePoint, file shares, databases)
- Extracts documents with metadata and ACL information
- Chunks content preserving semantic boundaries
- Generates embeddings (BGE-large-en-v1.5)
- Stores vectors with permission metadata in Qdrant

**Query Pipeline:**
- Receives user query with identity context
- Generates query embedding
- Performs metadata-filtered vector search (permission-aware)
- Retrieves only chunks user is authorized to see
- Returns citations with source document lineage

**Key Features:**
- Zero raw-text storage in vector DB (hash-based references)
- Query-time permission filtering
- Multi-source ingestion with unified metadata schema
- Deterministic chunk IDs for audit traceability

## Architecture
```
Source Systems → Ingestion → Chunking → Embedding → Qdrant
                                                        ↓
User Query → Query Embedding → Metadata Filter → Retrieval → Response
```

## Technology Stack

- **Python 3.11+** (async/await throughout)
- **FastAPI** (API layer)
- **Ollama** (local LLM inference)
- **Qdrant** (vector storage)
- **PostgreSQL** (permissions, sync state)
- **Microsoft Graph API** (SharePoint integration)

## Getting Started

See [`keystone-deploy`](https://github.com/getkeystone/keystone-deploy) for deployment instructions.

## Status

🚧 **Active Development** — Production-ready Q1 2025

## License

Source-available for evaluation and non-commercial use.

Commercial use requires a license agreement with Keystone AI.  
Contact: arnaldo@getkeystone.ai
