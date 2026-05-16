# Interviews

# AI System Design Interview — 11 Core Concepts

| # | Concept | Key Ideas | Best For |
|---|---------|-----------|----------|
| 1 | **End-to-End LLM Application Design** | Frontend → Backend → LLM → Tools | Product interviews |
| 2 | **Latency vs Cost vs Quality Trade-offs** | Model routing, fallback strategies | Production systems |
| 3 | **Scalable Inference Architecture** | Load balancing, batching, caching | Traffic spikes |
| 4 | **Data Pipeline for GenAI** | Ingestion → Chunking → Embedding → Storage | RAG systems |
| 5 | **Monitoring & Observability** | Token usage, drift, hallucination rate | Reliability |
| 6 | **Evaluation & A/B Testing** | Shadow mode, canary releases | Continuous improvement |
| 7 | **Security & Prompt Injection Defense** | Input sanitization, output validation | Public-facing apps |
| 8 | **Hybrid Human-AI Workflows** | Human-in-the-loop, escalation | High-stakes domains |
| 9 | **Cost Optimization at Scale** | Model selection, caching, quantization | Business viability |
| 10 | **Disaster Recovery & Versioning** | Model rollback, fallback prompts | Production |
| 11 | **Ethical & Compliance** | Bias audits, data consent | Enterprise |

### Quick Map

```
Architecture → E2E Design
Decisions    → Trade-offs
Performance  → Inference Scale
Grounding    → Data Pipeline
Health       → Observability
Iteration    → Eval & A/B
Protection   → Security
Quality      → Human-in-loop
Economics    → Cost Optimization
Resilience   → Recovery & Versioning
Responsibility → Ethics & Compliance
```

# Applied AI Engineer Interview — 10 Key Skills

## 1. Core Concepts
Transformers, attention mechanisms, tokenization, embeddings, context windows, fine-tuning (LoRA, QLoRA)

## 2. Code & Implementation
Backpropagation, attention from scratch, numerical stability, gradient debugging

## 3. Common Tasks
- End-to-end RAG pipeline (chunking → embeddings → vector DB → reranking)
- Prompt chaining & tool-calling agents
- Fine-tuning + evaluation harness (RAGAS, G-Eval)
- Quantization & inference optimization (bitsandbytes, vLLM)

## 4. Hands-on Projects
Production RAG chatbot, multi-agent workflow (LangGraph / CrewAI), real-time AI feature — deployed with monitoring

## 5. Frameworks & Tooling
LangChain, LlamaIndex, PyTorch, LangSmith tracing, vector stores (Pinecone vs Chroma vs PGVector), memory management, agent loops

## 6. AI System Design
Scalable LLM apps (customer support, document QA) — latency, cost, accuracy, guardrails, fallbacks

## 7. Production Architecture
Modular pipelines, LLMOps (drift monitoring, prompt/model versioning), eval frameworks, A/B testing, human-in-the-loop

## 8. Performance & Optimization
Quantization, distillation, batching, embedding caching, token cost control, inference serving (TGI, vLLM)

## 9. Security
Prompt injection defense, output guardrails (NeMo, LlamaGuard), PII redaction, hallucination mitigation, responsible AI

## 10. MLOps & Backend
MLflow / W&B, CI/CD for models, serving (FastAPI + Triton), vector DB scaling, observability (Prometheus + Grafana)
