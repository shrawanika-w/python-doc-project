# RAG Document Search AI

## Overview
This repository contains a **Retrieval Augmented Generation (RAG)** based document search platform designed for enterprise use. The system enables semantic search over structured and unstructured documents using embeddings, vector search, and large language models.

The platform is built with **operability, security, and scalability** in mind and follows standard architectural and governance practices expected in regulated environments.

---

## What This System Does
- Ingests enterprise documents
- Converts content into embeddings
- Stores vectors in a scalable vector database
- Retrieves relevant context for user queries
- Generates grounded responses using an LLM
- Exposes APIs for integration with applications and chat interfaces

---

## Intended Audience
This documentation is intended for:
- Software Engineers
- Architects
- SRE and DevOps teams
- AI and ML platform teams
- Security and Risk reviewers
- Product and Business stakeholders

---

## Documentation Structure

### Architecture
High-level and detailed architecture views following the **C4 Model**:
- System overview
- Context diagram
- Container diagram
- Component diagram

### ADRs
Architecture Decision Records explaining **why** key technical choices were made:
- Framework selection
- LLM provider
- Vector database

### API
OpenAPI specification for all public endpoints.

### Runbooks
Operational guides for:
- Production support
- Incident handling
- Disaster recovery

---

## Key Technology Choices
- **API Framework:** FastAPI
- **LLM Provider:** Gemini
- **Vector Store:** PostgreSQL with pgvector
- **Observability:** Prometheus, Grafana
- **Documentation:** Markdown, Mermaid, MkDocs

---

## Non-Goals
This system is not intended to:
- Train foundation models
- Replace enterprise search engines
- Operate without human oversight in regulated workflows

---

## Getting Started
1. Review the **Architecture** section for system design
2. Read ADRs to understand key decisions
3. Refer to API docs for integration
4. Use Runbooks for operational readiness

---

## Governance and Compliance
The platform aligns with:
- Secure SDLC practices
- Model risk management principles
- Audit and traceability requirements
- Data minimization and access control standards

---

## References
- Architecture: `/architecture/system-overview.md`
- ADRs: `/adr`
- API Spec: `/api/openapi.yaml`
- Production Runbook: `/runbooks/prod.md`
