# Disaster Recovery Runbook

**Service:** RAG Document Search AI  
**Environment:** Production  
**Date:** 2026-01-22  
**Owner:** AI Platform Team  

---

## 1. Purpose

This document outlines procedures for **recovering the RAG service** in case of catastrophic failures, including database outages, API failures, or cloud region failures.

---

## 2. Recovery Strategy

- Maintain **daily backups** of PostgreSQL database and vector embeddings.
- Use **multi-region deployment** for high availability if supported.
- Maintain **Docker images in registry** for quick redeployment.
- Keep **LLM API keys** and configuration stored securely.

---

## 3. Backup Procedures

### 3.1 PostgreSQL Backup

```bash
pg_dump -h <host> -U <user> -d <database> -F c -b -v -f "/backups/rag_backup_$(date +%F).dump"
```

 Verify backup integrity

Store copies in secure, redundant storage

### 3.2 Configuration Backup

- Kubernetes manifests (deployment.yaml, service.yaml)
- LLM API keys securely stored
- Env variables and secrets in Vault/Secret Manager

## 4. Recovery Steps

### 4.1 Database Failure

Restore latest backup:

```code
pg_restore -h <host> -U <user> -d <database> "/backups/rag_backup_latest.dump"
```

Restart API and worker pods:

```code
kubectl rollout restart deployment rag-api -n rag-prod
kubectl rollout restart deployment rag-worker -n rag-prod
```

### 4.2 API / Worker Failure

Scale up pods:

```code
kubectl scale deployment rag-api --replicas=5 -n rag-prod
kubectl scale deployment rag-worker --replicas=3 -n rag-prod
```

Monitor logs to confirm recovery:

```code
kubectl logs -f <pod_name> -n rag-prod
```

### 4.3 LLM Connectivity Issue

- Check Gemini API status
- Validate API keys
- Retry requests or switch to backup endpoints if available

## 5. Post-Recovery Actions

- Validate API health: /status and /metrics
- Run sample RAG queries to confirm correct embeddings and results
- Notify stakeholders of downtime and recovery
- Document root cause in incident management system

## 6. Contacts

- DevOps: devops@example.com
- AI Platform: ai-platform@example.com
- LLM Provider Support: support@gemini.com

## 7. References

- Production Runbook: /docs/runbooks/prod.md
- ADRs: /docs/adr/001-use-fastapi.md, /docs/adr/002-llm-provider.md, /docs/adr/003-vector-db.md
- Backup scripts: /scripts/db_backup.sh


```
