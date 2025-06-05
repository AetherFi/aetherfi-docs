
# 🤖 AGENT.md – AetherFi AI Triage Agents

This document describes the design, responsibilities, and lifecycle of AetherFi Vizier's AI-driven triage agents.

---

## 🎯 Purpose

AI Agents are used to augment pipeline triage decisions with contextual analysis, log parsing, and historical memory. Agents are modular, traceable, and auditable.

---

## 🧱 Core Responsibilities

- Receive structured pipeline events
- Retrieve historical or similar incidents from memory
- Analyze root causes or risk signals
- Return actionable `TriageDecision` suggestions

---

## 🧠 Agent Lifecycle

```
Trigger → Load Context → Retrieve Memory → Analyze → Return TriageDecision
```

### 1. **Trigger**
- Initiated by `TriageOrchestrator` when `requiresTriage = true`
- Called asynchronously (future: via job queue or event bus)

### 2. **Context Ingestion**
- Inputs:
  - `PipelineEvent.rawPayload`
  - `pipelineId`, `status`, `tenantId`
  - Timestamp + correlation metadata

### 3. **Memory Augmentation**
- Future: fetch related cases from Pinecone/Qdrant vector DB
- Cache or embed past triage outcomes and explanations

### 4. **Analysis**
- Uses LLM prompt with structure:
  - System: "You're a pipeline triage agent..."
  - User: [formatted pipeline context]
- LLM model: Claude, GPT-4, or Bedrock Titan

### 5. **Return**
- Returns `TriageDecision` with:
  - `action`, `reason`, `confidence`
  - Embedded audit trace for compliance

---

## 🔐 Security & Observability

- All agent calls are logged with:
  - `correlationId`, `tenantId`, `agentName`, `decisionTime`
- LLM interactions are redacted for PII before logging
- Future: support token usage metering and rate limiting

---

## 📊 Example Decision

```json
{
  "action": "notify_slack",
  "reason": "Pipeline failed on a flaky test also seen in issue #1432.",
  "confidence": 0.92
}
```

---

## 🚀 Future Enhancements

- [ ] Implement `AgentRegistry` with per-tenant config
- [ ] Enable feedback loop for agent learning
- [ ] Store token logs for billing + observability
- [ ] Add fallback agents (rule-based) for failsafe mode
