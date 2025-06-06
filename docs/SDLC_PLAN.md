# AetherFi SDLC (Software Development Lifecycle) Plan

---

## 📚 Methodology

* Hybrid Agile (Milestone-based sprints + Kanban for task tracking)
* Microservice-oriented architecture with isolated deployability
* Agent-based modularity for AI logic
* Terraform-based infrastructure-as-code with CI/CD
* Observability-first development: structured logging, traceability

---

## 🛠️ Development Phases & Timeline

| Phase    | Deliverables                                              |
| -------- | --------------------------------------------------------- |
| Sprint 0 | Repo Setup, DI and Logging Architecture                   |
| Sprint 1 | Webhook Ingestion E2E, Logging w/ Trace ID, ContextLogger |
| Sprint 2 | Eidolon Agent Base API, JSON RAG pipeline scaffold        |
| Sprint 3 | Secrets Handling, Pybreaker Circuit Breaker               |
| Sprint 4 | Modular aetherfi-core extraction, Notion/Slack clients    |
| Sprint 5 | Kafka plan, Memory ingestion, Qdrant metadata test suite  |

---

## 📊 Deployment Strategy

* **Dev Environments**: Docker Compose, Makefile-based CLI tools
* **CI/CD**: GitLab Pipelines, OIDC IAM Role Assumption for AWS
* **Environments**:

  * `dev`: per-feature deploy via dynamic Terraform state
  * `staging`: integration tests, cost estimation (Infracost)
  * `main`: production via `main` branch deploys

---

## 🔐 Security

* OIDC authentication for GitLab CI pipelines
* AWS IAM roles scoped per environment
* Secrets managed via `.env` in dev, AWS Secrets Manager planned
* Circuit breaker + structured error fallback

---

## 📈 Observability & Logging

* Structured JSON logs with `ContextLogger`
* Correlation ID, Tenant ID, Request ID traced across services
* Logs routed to file, console, and prepared for CloudWatch
* Kafka event emission (planned) for triage lifecycle events

---

## 📅 Sprint Cadence

| Sprint Length | Deliverables                              | Validation                               |
| ------------- | ----------------------------------------- | ---------------------------------------- |
| 5-7 days      | End-to-end flow, new feature, or refactor | Must include test coverage + log tracing |

Each sprint results in:

* Tagged Git commit: `v0.1-webhook-ingest`, etc.
* Updated Notion changelog + `/recap` logs

---

## 📃 Documentation Layers

| File                    | Purpose                                         |
| ----------------------- | ----------------------------------------------- |
| `README.md`             | High-level system intro                         |
| `docs/ARCHITECTURE.md`  | System design, DI layers, container structure   |
| `docs/OBSERVABILITY.md` | Log format, dashboard links, Slack/Notion flows |
| `docs/DI_OVERVIEW.md`   | DI container wiring, logger hierarchy           |
| `docs/MILESTONES.md`    | Feature roadmap + progress                      |
| `docs/SDLC_PLAN.md`     | This doc — full lifecycle and planning strategy |

---

## 🤝 External Alignment (Hiring, Portfolios, Investors)

You can speak to:

* Event-driven platform architecture
* Terraform IaC with GitLab CI/CD and OIDC IAM security
* Structured memory and retrieval via Qdrant + Postgres
* Multi-agent coordination (Eidolon, Vizier, Shadow Banker)

---

## 🌟 MVP Launch Targets

| Milestone                     | Tag                | Status         |
| ----------------------------- | ------------------ | -------------- |
| Webhook ➝ Triage ➝ Notion Log | `v0.2-core-agent`  | ✅ Complete     |
| Eidolon Memory API            | `v0.3-memory-api`  | 🚧 In Progress |
| Shadow Banker CLI             | `v0.4-shadow-cli`  | 🔜 Planned     |
| Infra AI-Ready                | `v0.5-aws-oidc`    | ✅ In Review    |
| Production RAG Agent          | `v1.0-public-beta` | 🔜 Q3 2025     |

---

## 🤍 Future Focus

* 🔒 Migrate secrets to AWS Secrets Manager
* 🧠 Launch Triage Memory Store with event graph enrichment
* 🛰️ Kafka backbone for triage event streaming
* ☁️ ECS/EKS deployment of Eidolon + Vizier
* 📈 Cloud-native dashboards via Grafana + CloudWatch
