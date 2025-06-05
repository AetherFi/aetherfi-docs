# AetherFi — AI-Native Fintech Debugging Platform

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-blue.svg" />
  <img src="https://img.shields.io/badge/Spring_Boot-3.2-brightgreen.svg" />
  <img src="https://img.shields.io/badge/FastAPI-Python%203.11-blue.svg" />
  <img src="https://img.shields.io/badge/Kafka-Event_Bus-orange.svg" />
  <img src="https://img.shields.io/badge/PostgreSQL-Metadata-blue.svg" />
  <img src="https://img.shields.io/badge/Qdrant-VectorDB-red.svg" />
  <img src="https://img.shields.io/badge/Terraform-Infrastructure-purple.svg" />
  <img src="https://img.shields.io/badge/Prometheus-Monitoring-orange.svg" />
  <img src="https://img.shields.io/badge/Grafana-Dashboards-yellow.svg" />
  <img src="https://img.shields.io/badge/OAuth2-ZeroTrust-critical.svg" />
  <img src="https://img.shields.io/badge/Codebase-Private-informational.svg" />
</p>

---

## 🧠 Overview

**AetherFi** is a modular, event-driven platform for **AI-assisted DevOps debugging**, **risk triage**, and **FinTech intelligence automation**. It merges robust microservice architecture with retrieval-augmented AI workflows to reduce resolution time and improve infrastructure observability.

> 🔒 This GitHub repo is a public mirror.  
> Production codebase is hosted privately on GitLab and deployed to AWS via GitLab CI/CD.

---

## 🔍 What It Does

- 🔄 Webhook-to-Kafka async triage flows
- 🧠 AI memory recall with RAG + VectorDB (Qdrant)
- 🔐 Multitenant observability with correlation + trace ID
- 🛠️ FAANG-grade DI, Flyway migrations, Terraform IaC
- 📈 Dashboards: Prometheus + Grafana (mocked + planned)

---

## 🧩 System Architecture

<details>
<summary><strong>Expand: Technical Layers</strong></summary>

### System Components

| Layer              | Description                                                |
|-------------------|------------------------------------------------------------|
| **Infra**         | GitLab CI → Secure Webhook Ingest                          |
| **Orchestration** | Java-based Vizier Orchestrator (Spring Boot, Resilience4j) |
| **Agent Layer**   | Python-based Eidolon AI Agent (FastAPI, OpenAI, Claude)    |
| **Memory Layer**  | Vector Search (Qdrant) + future metadata store (Postgres)  |
| **Observability** | Prometheus, Grafana, OTel Tracing, Slack + Notion output   |
| **Security**      | OAuth2, Zero Trust, Tenant Isolation                       |

📌 See [System Architecture](docs/ARCHITECTURE.md)

</details>

---

## 🗺 Roadmap

| Milestone                          | Status     |
|-----------------------------------|------------|
| ✅ Webhook ingestion demo (E2E)    | Complete   |
| 🚧 Eidolon RAG agent launch        | In Progress|
| 🚧 Qdrant + Postgres orchestration | In Progress|
| 🚧 FinTech CLI (ShadowBanker)      | Planned    |
| 🚧 Observability integrations      | Planned    |

📌 See [Project Milestones](docs/MILESTONES.md)

---

## 🔧 Project Goals

- Build a **Debug-as-a-Service** (DaaS) FinTech platform
- Enforce **Zero Trust + Secrets Rotation**
- Deliver **Graph-augmented AI memory tools**
- Achieve **modular scale across microservices**

---

## 📚 Deep Dives

- 📐 [System Architecture](docs/ARCHITECTURE.md)
- 🧱 [Dependency Injection Overview](docs/DI_OVERVIEW.md)
- 🗃️ [Flyway Migration Guide](docs/MIGRATIONS.md)
- 🧪 [E2E Test Architecture](docs/TESTING.md)
- 🧭 [SDLC Plan](docs/SDLC_PLAN.md)

---

## 📊 Status

> 🚧 **Active Development**  
> ✅ End-to-end webhook ingestion tested  
> 📎 Logs, mock dashboards, and architecture docs available

---

## 🤝 Want to Collaborate or Demo?

> 💬 Contact for demo access to private GitLab or live dashboard views.
> AI agents available for Slack/Notion observability output.

---
