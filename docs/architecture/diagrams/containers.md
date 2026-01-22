
# Containers Diagram

```mermaid
%%{init: {'theme': 'forest'}}%%
graph LR
    FPnA[FPnA Copilot System]
    API[FastAPI Service]
    Worker[RAG Worker]
    VectorDB[Chroma Vector DB]
    LLM[Azure OpenAI LLM]

    FPnA --> API
    API --> Worker
    Worker --> VectorDB
    Worker --> LLM
```
