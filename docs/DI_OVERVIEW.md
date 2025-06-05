# AetherFi Dependency Injection & Logging Overview

This document provides a production-grade overview of the **Dependency Injection (DI)** strategy powering AetherFi AI agents, including core container separation, logger wiring, and composition best practices.

---

## ✅ Layered DI Containers

| Layer       | Container          | Responsibilities                                                                |
| ----------- | ------------------ | ------------------------------------------------------------------------------- |
| 🧠 Core     | `CoreContainer`    | `settings`, `logger`, and config sources                                        |
| 🔌 Services | `ServiceContainer` | External service clients (Slack, Notion, AWS, etc.)                             |
| 🤖 Agents   | `AgentContainer`   | Business logic agents like `GitLabPipelineAgent`, injected with core + services |

> **Key Principle:**
> Composition happens in `main.py`, **not** inside containers. No circular wiring. Explicit dependencies only.

---

## 🔊 Logging System

| Component         | Description                                                                    |
| ----------------- | ------------------------------------------------------------------------------ |
| `get_logger(...)` | JSON logger with file+console, rotation ready                                  |
| `ContextLogger`   | Subclass of `LoggerAdapter` injecting `request_id`, `pipeline_id`, `tenant_id` |
| `LoggerFactory`   | (Optional) Creates scoped loggers per component                                |
| Output            | Structured logs with ISO 8601 timestamps, source context, and log level        |

> You now log like a cloud-native SaaS platform built for observability 🔍

---

## 🔧 DI Wiring & Injection Best Practices

| Pattern                      | Practice                                          |
| ---------------------------- | ------------------------------------------------- |
| `@inject` + `Provide[...]`   | ✅ Used to inject config, clients, and loggers     |
| `core_container.wire([...])` | ✅ Required wherever DI is used                    |
| Avoid `Settings()` calls     | ✅ Use `Provide[core.config]` instead              |
| `logger.getChild("...")`     | ✅ Used for per-component loggers (e.g., `gitlab`) |

---

## 🧰 Planned Extensions

| Task                                      | Status      |
| ----------------------------------------- | ----------- |
| Implement `pybreaker` circuit breakers    | 🔜 Next     |
| Kafka async logging bridge                | 🔜 Planned  |
| Add `LoggerAdapter` to FastAPI middleware | 🤔 Optional |
| Tenant-aware DI context support           | 🤔 Planning |

---

## 🖊️ Quick Reference

* DI Container entrypoint: `main.py`
* Logger structure: `ContextLogger > LoggerAdapter`
* Composition style: functional + explicit wiring

> “We don’t just wire dependencies — we architect resilient, traceable systems.”

---
