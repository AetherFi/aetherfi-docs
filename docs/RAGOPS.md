

# 🧠 RAGOps: Operating AI Agents in Production

## 🎯 What Is RAGOps?

RAGOps is the discipline of maintaining, monitoring, and debugging Retrieval-Augmented Generation systems in production.

AetherFi treats AI agents like production microservices—complete with observability, CI testing, and vector recall metrics.

---

## 🔎 What We Track

| Signal                  | Purpose                                  |
|-------------------------|------------------------------------------|
| Prompt lineage          | Track which memory chunks were cited     |
| Slack feedback          | Feed into reranking and RAR triggers     |
| Vector hit/miss rates   | Gauge embedding effectiveness            |
| Latency + cost metrics  | Monitor response time + token cost       |
| RAR precision           | Score entailment / hallucination risk    |

---

## 🔄 From RAG → RAR

| Capability        | RAG             | RAR                                 |
|------------------|------------------|--------------------------------------|
| Strategy          | Top-1 recall     | Compare top-N chunks for conflicts   |
| UX                | Plain answer     | Explanation + supporting evidence    |
| Slack usage       | Passive logs     | Feedback loop powers reranking       |

---

## 🧪 Observability

We use:
- Prometheus metrics
- JSON logs with correlation IDs
- Grafana (planned)
- Notion/Slack feedback hooks
