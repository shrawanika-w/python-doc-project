# ADR 001: Use FastAPI

**Status:** Accepted  
**Date:** 2026-01-22  

## Context
We are building a RAG-based document search AI service that will:
- Accept user queries from multiple clients
- Interface with a vector database
- Call a large language model for answers
- Serve multiple concurrent requests efficiently

## Decision
We will use **FastAPI** as the backend framework.

## Rationale
1. Performance: Supports async and high concurrency
2. Developer Productivity: Type hints, dependency injection
3. Auto-generated API docs (OpenAPI/Swagger)
4. Easy testing & CI/CD integration
5. Strong community and ecosystem

## Consequences
- All endpoints async
- Frontend can rely on auto-generated docs
- Security patching is mandatory
- Migration to other frameworks will require refactoring
