# ADR 003: Vector Database

**Status:** Accepted  
**Date:** 2026-01-22  

## Context
The RAG-based document search AI service needs a **database to store documents and embeddings**:

- Must handle **structured and unstructured data** efficiently.
- Support **fast vector similarity search** for embeddings.
- Ensure **ACID compliance** for transactional consistency.
- Integrate well with Python, FastAPI, and the overall service architecture.

Several options were considered, including PostgreSQL, Chroma, and Pinecone.

---

## Decision
We will use **PostgreSQL** as the primary database for storing documents, metadata, and vector embeddings.

---

## Rationale
1. **Maturity & Reliability**: PostgreSQL is a proven, enterprise-grade relational database with strong consistency guarantees.  
2. **Vector Search Support**: Native support for vector data types and indexing (via `pgvector` extension) allows efficient similarity search.  
3. **Integration**: Excellent Python support via `psycopg2` / `SQLAlchemy`, making integration with FastAPI straightforward.  
4. **Security & Compliance**: Enterprise security, encryption, and auditing features align with banking standards.  
5. **Cost-Effective**: Open-source, widely supported, and can scale vertically or horizontally with extensions.  
6. **Operational Simplicity**: Teams already have PostgreSQL expertise, reducing onboarding and operational overhead.  

---

## Consequences
- Use the `pgvector` extension to store embeddings efficiently.  
- Backend must implement batch writes and similarity queries optimized for RAG workflows.  
- Migration to another vector DB in the future would require changes in query logic and indexing.  
- PostgreSQL maintenance, backups, and scaling strategies must be defined and monitored.  
- Hybrid approach is possible: PostgreSQL for metadata + specialized vector DB if needed for extreme scale.  

