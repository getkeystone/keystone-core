# Keystone Core

Core retrieval and ingestion engine for on-prem knowledge systems with permission-aware retrieval.

Runs fully on customer infrastructure. No external API calls. Air-gap compatible.

## What This Does

### Ingestion Pipeline
- Connects to source systems (SharePoint, file shares, databases)
- Extracts documents with metadata and ACL information
- Chunks content preserving semantic boundaries
- Generates embeddings
- Stores vectors with permission metadata in the configured vector backend (demo defaults to Qdrant)

### Query Pipeline
- Receives user query with identity context
- Generates query embedding
- Performs metadata-filtered vector search (permission-aware)
- Retrieves only chunks the user is authorized to see
- Returns citations with source lineage (document and chunk references)

## Key Features

- Query-time permission filtering (enforced at retrieval, not by trusting the LLM)
- Multi-source ingestion with a unified metadata schema
- Deterministic chunk identifiers for traceability
- Citation generation with document lineage
- Designed for fail-closed behavior when evidence is insufficient

## Architecture

```
Source Systems → Ingestion → Chunking → Embedding → Vector Backend
↓
User Query → Query Embedding → Metadata Filter → Retrieval → Response
```


## Technology Stack

- Python 3.11+ (async/await throughout)
- FastAPI (API layer)
- Ollama (local LLM inference)
- Vector search backend (Qdrant in demo)
- PostgreSQL (permissions, sync state, audit references)
- Microsoft Graph API (SharePoint integration)

## Getting Started

See [`keystone-deploy`](https://github.com/getkeystone/keystone-deploy) for deployment instructions.

## Development Status

🚧 Active Development

- Current milestone: single-machine governed retrieval proof (KDAT-001A)
- Next: production hardening and multi-node deployment patterns

## License

Keystone Core is licensed under the [Business Source License 1.1](LICENSE).

**Non-production use is free:**
- Development, testing, and evaluation environments only
- Up to 100 internal users

**Production use requires a commercial license.**

**Change Date:** 2030-01-01  
After this date, the license automatically converts to Apache License 2.0.

For commercial licensing: arnaldo@getkeystone.ai
