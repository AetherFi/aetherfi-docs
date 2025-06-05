# AetherFi: AI-Native Fintech Debugging Platform

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-blue.svg" alt="Java 21"/>
  <img src="https://img.shields.io/badge/Spring_Boot-3.2-brightgreen.svg" alt="Spring Boot 3.2"/>
  <img src="https://img.shields.io/badge/FastAPI-Python%203.11-blue.svg" alt="FastAPI Python 3.11"/>
  <img src="https://img.shields.io/badge/Kafka-Event_Bus-orange.svg" alt="Kafka Event Bus"/>
  <img src="https://img.shields.io/badge/PostgreSQL-Metadata-blue.svg" alt="PostgreSQL Metadata"/>
  <img src="https://img.shields.io/badge/Qdrant-VectorDB-red.svg" alt="Qdrant Vector DB"/>
  <img src="https://img.shields.io/badge/Terraform-Infrastructure-purple.svg" alt="Terraform Infra"/>
  <img src="https://img.shields.io/badge/Prometheus-Monitoring-orange.svg" alt="Prometheus Monitoring"/>
  <img src="https://img.shields.io/badge/Grafana-Dashboards-yellow.svg" alt="Grafana Dashboards"/>
  <img src="https://img.shields.io/badge/OAuth2-ZeroTrust-critical.svg" alt="OAuth2 Security"/>
</p>

## Overview
AetherFi is an event-driven, AI-augmented infrastructure designed for cloud DevOps debugging, risk triage, and future fintech intelligence modules.

It blends cloud-native engineering (Kafka, Spring Boot, FastAPI) with emerging AI workflows (RAG, vector search) to automate triage and future decision support.

---

## Architecture Overview
- Ingress Layer: Kong Gateway, secured API ingress
- Messaging Layer: Kafka Event Bus (partitioned + resilient)
- Core API Layer: Vizier API (Spring Boot Java)
- Agent Layer: Eidolon Agents (Python FastAPI)
- Persistence Layer: PostgreSQL, Qdrant Vector Store
- Observability Layer: Prometheus, Grafana
- Security Layer: OAuth2, JWT, Secrets Management

---

## Project Goals
- 🔥 Intelligent Debug-as-a-Service (DaaS) offering
- 🔒 Zero Trust architecture
- 📊 Observability-first design
- 🛡️ Scalable, event-driven AI agent system
- 📚 Phase 2: Fintech market analysis and Shadow Banker Terminal integration

---

## Documentation
- [System Design Overview](./docs/system_design.md)
- [Architecture Diagram](./diagrams/aetherfi_architecture.svg)
- [Feature Roadmap](./FEATURE_ROADMAP.md)
- [Tech Stack Details](./TECH_STACK.md)

---

## Status
🔵 Actively in development — first live end-to-end webhook test milestone achieved.

---
