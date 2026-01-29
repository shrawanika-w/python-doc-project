# ADR 002: LLM Provider

**Status:** Accepted  
**Date:** 2026-01-22  

## Context
Our RAG-based document search AI service requires a **large language model (LLM)** to:

- Interpret natural language queries from users.
- Summarize and generate relevant answers based on retrieved documents.
- Support multiple languages and domain-specific terminology.
- Scale efficiently with low latency for multiple concurrent requests.

We evaluated multiple LLM providers, including OpenAI GPT, Anthropic Claude, and Gemini.

---

## Decision
We will use **Gemini LLM** as the provider for our RAG service.

---

## Rationale
1. **Performance & Accuracy**: Gemini has high accuracy on reasoning and summarization tasks, particularly with financial documents.  
2. **Cost Efficiency**: Competitive pricing for large-scale API usage compared to other providers.  
3. **Latency & Reliability**: Provides low-latency API endpoints suitable for interactive queries.  
4. **Security & Compliance**: Data handling and storage policies align with banking regulations.  
5. **Ecosystem & Integrations**: Provides SDKs and tools compatible with Python, making integration with FastAPI straightforward.  
6. **Future-proofing**: Continuous updates from the provider ensure access to new capabilities and improvements.

---

## Consequences
- All query requests will route through Gemini APIs.  
- Backend service will handle token limits and implement caching for efficiency.  
- Team will monitor costs and usage to prevent overages.  
- Training custom models on Gemini may be considered in the future for domain-specific enhancements.  
- Switching to another LLM provider will require updating API calls and re-testing response behavior.

