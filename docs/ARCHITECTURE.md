---
title: AetherFi System Architecture  
summary: Modular Multi-Agent Platform for AI-Driven Infrastructure Triage  
---

# 🧠 AetherFi System Architecture

AetherFi is a modular, AI-augmented DevOps platform designed to automate infrastructure triage, observability, and debugging workflows. It is built around event-driven microservices, multi-agent collaboration, and banking-grade deployment standards.

This document outlines the system's architecture, its migration journey from monolith to microservices, and design rationales for its core modules.

---

## 🧱 Core Architectural Principles

- **Domain-Driven Microservices**  
  Each service (e.g., Triage, Event Logging, Auth) owns a clearly defined business capability.

- **Agent-Oriented Design**  
  Autonomous agents (e.g., `GitLabPipelineAgent`) encapsulate decision logic triggered by infrastructure events.

- **Zero Trust by Default**  
  OAuth2, OIDC, IAM, and JWT are integrated at all boundaries; no implicit trust between components.

- **Event-Driven Orchestration**  
  Kafka serves as the backbone for async coordination, audit trails, and inter-service decoupling.

- **Observable by Design**  
  Circuit breakers, correlation IDs, JSON logging, metrics, and health checks are first-class citizens.

---

## 🌀 Migration: Monolith → Microservices

> AetherFi began as a single-process FastAPI monolith. It has since evolved into language-agnostic modular services (Java + Python) connected through Kafka and containerized interfaces.

### ✅ Milestones:

- Defined `pipeline_events` schema; persisted GitLab triage payloads.
- Introduced Spring Boot + JPA for transactional event storage.
- Docker Compose added for local Kafka replay testing.
- Refactored agents to use dependency injection (Python & Java).
- Kafka fan-out, vector memory, and tenant-aware RBAC in progress.

### 📊 Milestone Roadmap

<img src="./assets/aetherfi-milestones-roadmap.png" alt="Milestone Roadmap" width="40%" />
> A high-level view of AetherFi's technical phases, from audit trail setup through AI-powered FinTech agents.

---

## 🧩 Modular Components

### `vizier-gateway` (Java)
- Accepts incoming API and webhook requests.
- Routes events to services and agents (Kafka producers, downstream APIs).

### `pipeline-triage-service` (Java)
- Stores `PipelineEvent` data.
- Exposes RESTful interfaces for querying pipeline metadata.

### `aetherfi-ai` (Python)
- `GitLabPipelineAgent` consumes pipeline data.
- Annotates failures, performs pattern classification.
- Sends alerts to Notion and Slack.
- Integrates Claude/Bedrock for AI-assisted triage (via structured prompts).

### `eidolon-memory` (WIP)
- Vector search over historical failures, PDFs, and architecture recaps.
- Enables RAG-powered, context-aware debugging.

### `eidolon-datalake` (Planned)
- Stores raw, semi-structured data: HTML chat exports, logs, financial filings, web-scraped sources.
- Acts as a long-term archive to support future enrichment and ETL pipelines.
- Integrated with RAG as a secondary retrieval source post-curation.

### `etl-pipeline` (Planned)
- Ingests data from the datalake into Qdrant or Postgres.
- Handles chunking, embedding, deduplication, and tagging.
- Planned to be modular: each source (HTML, Slack threads, web) has a dedicated ingestion module. 

### `jira-integration` (Planned)
- Supports escalated incidents with structured ticket creation and lifecycle tracking.
- Future replacement for Notion.
- Uses JIRA REST API for bidirectional updates (AI triage → JIRA ticket → resolved PR/commit status).

---

## 🔒 Security & Reliability

- **OIDC Auth**: Federated access using GitLab & AWS IAM.
- **Circuit Breakers**: Implemented via `pybreaker` and `Resilience4j`.
- **Structured Logging**: JSON logs with CloudWatch export support.
- **Idempotency**: Events uniquely keyed via `idempotency_key` across services.

---

## 🔭 Observability Features

- **Correlation ID Propagation**: Consistent request tracking across services.
- **Kafka Replay Setup**: Docker Compose for re-ingesting real events.
- **Dashboards**: WIP Grafana + Notion boards.
- **RAGOps observability**: trace prompt lineage, Slack feedback cycles, and vector hit/miss rates (planned)

### 🔄 Kafka Streaming Flow

<img src="./assets/aetherfi_streaming.png" alt="Kafka Streaming Flow" width="50%" />
> Shows how webhook events are pushed into Kafka, enriched via AI, and orchestrated across services for triage and Redis-based TTL caching.

---

## 🧠 AI Agent Vision

AetherFi’s long-term goal is to evolve into a true AI teammate for DevOps and FinTech:

- Ingests logs, CI/CD results, and cloud metrics.
- Cross-references historical patterns using vector memory (Qdrant) and structured documents extracted from a raw datalake. Future support for Retrieval-Augmented Reasoning (RAR) enables the agent to build reasoning trees across retrieved knowledge chunks.
- Proposes resolutions with traceable justifications.
- Automatically logs findings to Notion and notifies stakeholders via Slack.

### 🧠 RAG vs RAR

The architecture supports both:

- **RAG (Retrieval-Augmented Generation)**: Enables fast memory lookups by retrieving the most relevant document chunks and embedding them directly into the LLM prompt.
  
- **RAR (Retrieval-Augmented Reasoning)**: Enhances insight quality by retrieving multiple related chunks, detecting contradictions, and prompting the LLM to reason across sources to explain root causes.

This dual-mode design allows AetherFi to balance speed with depth, supporting both instant answers and nuanced, human-grade debugging insights.

<img src="./assets/aetherfi-ai-agent_architecturev2.png" alt="AetherFi AI Agent Orchestration" width="50%" />
> Illustrates a full pipeline from GitLab webhook trigger → AI agent analysis → human-in-the-loop notification with Slack and GitLab integration.

---

## 🛣️ Roadmap

- ✅ Monolith → Microservices Migration (Complete)
- 🔄 Kafka + GitLab CI Ingestion
- 🧠 RAG Memory Integration (Qdrant, Claude)
- 🧪 Secure Multi-Tenant Orchestration
- 🔔 Slack/Notion Automation
- 🪵 Datalake Ingestion Module (HTML, Slack, Web Scrapes)
- 🔄 ETL Service → Embedding into Qdrant/Postgres
- 🔍 RAR Prototype: Reasoning agent w/ evidence traces

- 🌐 Public Demo Deployment

---

## 📎 References

- [`AetherFi AI Triage Agents`](AGENT.md)
- [`Flyway Migration Guide`](Flyway_Migration_Guide.md) – Versioned DDL and schema lifecycle
- [`Dependency Injection Overview`](DI_OVERVIEW.md)
- [`MILESTONES.md`](E2E_TRIAGE.md)
- [`ETL_Pipeline.md`](ETL_Pipeline.md) — WIP plan for ingestion, tagging, and chunking from raw datalake to vector + metadata storage.
- [`DataLake_Vision.md`](DataLake_Vision.md) — Motivation and use cases for long-term unstructured storage.


---

### 📐 Architecture Visuals

#### 🔁 Gateway + Redis Event Orchestration

<img src="./assets/aetherfi-vizier-arch.png" alt="Webhook Controller Flow: Evaluator vs Kafka Triage Path" width="350"/>

> 🔀 This diagram illustrates AetherFi’s dual-path webhook routing: simple evaluable events are resolved via Redis/Evaluator; complex ones are escalated to Kafka and routed to AI Orchestrators. Designed for modular fallback, async retries, and low-latency responses.

--- 

#### 🧠 Full AI Agent System Flow

<img src="./assets/aetherfi-ai-agent_architecturev2.png" alt="Full System Architecture: GitLab + AWS → AI Agent Orchestration → Slack/Notion" width="800"/>

> Demonstrates the system-wide interaction of GitLab, AWS, Datadog, Notion, and Slack with various agents coordinating event-driven debugging.

---

> _“AetherFi isn't just a tool — it's your infrastructure apprentice.”_
