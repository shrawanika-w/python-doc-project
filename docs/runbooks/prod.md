# Production Runbook

**System:** RAG Based Document Search AI  
**Environment:** Production  
**Owners:** AI Platform and DevOps  
**Last Updated:** 2026-01-22  

---

## 1. Purpose
This runbook defines how to **operate, monitor, and support** the RAG AI service in production. It is written for on-call engineers, SREs, and platform teams.

---

## 2. System Overview
The RAG platform provides semantic search over enterprise documents using embeddings and an LLM.

Core components:

- **FastAPI Gateway**: Exposes REST endpoints to clients
- **RAG Worker**: Generates embeddings, performs retrieval, calls LLM
- **Vector Store**: PostgreSQL with pgvector
- **LLM Provider**: Gemini
- **Object Storage**: Stores original documents
- **Observability**: Prometheus, Grafana, centralized logging

High-level flow:
1. User submits query
2. Query is embedded
3. Vector search retrieves relevant chunks
4. Context is sent to Gemini
5. Response returned to user

---

## 3. Service Endpoints

| Endpoint | Purpose |
|--------|--------|
| `/query` | Submit RAG query |
| `/ingest` | Upload documents |
| `/status` | Health check |
| `/metrics` | Prometheus metrics |
| `/docs` | OpenAPI UI |

Health check response:
```json
{
  "api": "ok",
  "vector_db": "ok",
  "llm": "ok",
  "storage": "ok"
}

## 4. Deployment Model

The service runs on Kubernetes.

* rag-api Deployment: FastAPI
* rag-worker Deployment: RAG pipeline
* postgres StatefulSet
* Secrets stored in Kubernetes Secrets or Vault

Typical sizes:

* API: 3 replicas
* Workers: 2 to 5 replicas
* PostgreSQL: HA or managed service  

## 5. Standard Operations

### 5.1 Restart Services

```bash
kubectl rollout restart deployment rag-api -n rag-prod
kubectl rollout restart deployment rag-worker -n rag-prod

### 5.2 Scale for Load

```bash
kubectl scale deployment rag-worker --replicas=5 -n rag-prod

### 5.3 Check Pods

```bash
kubectl get pods -n rag-prod

### 5.4 View Logs

```bash
kubectl logs -f <pod-name> -n rag-prod

## 6. Monitoring

Key dashboards:

* Request volume
* Query latency
* Vector search latency
* Gemini API errors
* Token usage
* PostgreSQL CPU, disk, and query latency

Key alerts:

* API error rate > 2%
* Query latency > 5s
* Embedding failures
* PostgreSQL disk > 80%
* Gemini API failures

## 7. Common Incidents

### 7.1 High Latency

Check:

* Worker CPU and memory
* PostgreSQL slow queries
* Vector index health
* Gemini rate limits

Actions:

* Scale workers
* Enable query caching
* Check embedding batch sizes
