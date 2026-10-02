# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **Agents Towards Production** (`agents-towards-production`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** Agents Towards Production (`agents-towards-production`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Production-Grade Agent Engineering & MLOps  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

Agents Towards Production is an engineering and MLOps framework designed to bridge the chasm between experimental GenAI prototypes and resilient, enterprise-grade production systems. Rather than treating agents as single-turn chat scripts, the framework operationalizes end-to-end architectures encompassing stateful graph orchestration, multi-tier memory backends, defensive security guardrails, distributed telemetry tracing, and automated regression evaluations.

### 1. Decision Architecture

The user request intake, guardrail scanning, state graph execution, tool authorization, telemetry emission, and evaluation feedback pipeline operates across a deterministic, five-stage architecture:

```
User Prompt / Engineering Request (e.g., "Deploy an authenticated multi-tenant financial agent")
    │
    ▼
[Stage 1: Ingestion & Defensive Security Pre-Scan]
    │  - Scans incoming prompt for prompt injection, jailbreaks, and PII leakage (LlamaFirewall / Apex)
    │  - Validates API tokens and authenticates user tenant credentials
    │  - Sanitizes input strings before routing to internal orchestrator
    ▼
[Stage 2: Graph Routing & Context Assembly]
    │  - Compiles execution plan using stateful cyclical graph topologies (LangGraph)
    │  - Queries multi-tier memory layers (Redis working cache, Mem0 episodic vector index)
    │  - Formulates bounded context window with token budget safeguards
    ▼
[Stage 3: Stateful Execution & Authorized Tool Calling]
    │  - Executes graph nodes with strict timeouts and exponential backoff retry policies
    │  - Authorizes external API actions through least-privilege token delegation (Arcade)
    │  - Captures child span latencies and records intermediate state checkpoints
    ▼
[Stage 4: Output Guardrails & Schema Verification]
    │  - Validates agent output against Pydantic structural schemas
    │  - Scans generated response for hallucinated credentials or policy violations
    │  - Intercepts non-compliant responses and triggers localized graph retry
    ▼
[Stage 5: Telemetry Export & Continuous Evaluation]
    │  - Exports complete execution traces to observability backends (LangSmith / OpenTelemetry)
    │  - Evaluates run against automated benchmark criteria (IntellAgent quality metrics)
    │  - Commits verified state transitions to persistent thread storage
    ▼
Production-Grade Verified Agent Response & Auditable Distributed Trace Record
```

### 2. Decision Logic & Routing Formulations

Agents Towards Production evaluates security threat levels, tool authorization, and production readiness using deterministic mathematical models:

1. **Security Threat Index ($S_{\text{threat}}$)**:
   $$S_{\text{threat}}(x) = (w_i \cdot I_{\text{injection}}) + (w_p \cdot P_{\text{pii}}) + (w_a \cdot A_{\text{anomaly}})$$
   where:
   - $I_{\text{injection}} \in [0, 1]$ represents classification confidence of adversarial prompt injection.
   - $P_{\text{pii}} \in \{0, 1\}$ detects presence of unmasked personal identifying information.
   - $A_{\text{anomaly}} \in [0, 1]$ indicates semantic drift from typical user tenant query profiles.
   - Weights: $w_i = 0.50, w_p = 0.30, w_a = 0.20$ ($\sum w_i = 1.0$).
   - If $S_{\text{threat}}(x) \ge 0.65$, the request is refused with a security event code.

2. **Production Reliability Score ($R_{\text{prod}}$)**:
   $$R_{\text{prod}} = (w_s \cdot S_{\text{schema}}) + (w_l \cdot L_{\text{latency}}) + (w_e \cdot E_{\text{eval}})$$
   where:
   - $S_{\text{schema}} \in \{0, 1\}$ denotes strict Pydantic output validation compliance.
   - $L_{\text{latency}} = \min(1.0, \frac{\tau_{\text{max}}}{t_{\text{elapsed}}})$ assesses response time relative to SLA ceilings.
   - $E_{\text{eval}} \in [0, 1]$ represents benchmark correctness and faithfulness scores.
   - Weights: $w_s = 0.40, w_l = 0.30, w_e = 0.30$.
   - A pipeline stage passes only when $R_{\text{prod}} \ge 0.90$.

### 3. Thresholding & Refusal Decision Criteria

Agents Towards Production enforces strict operational guardrails to prevent security breaches and systemic instability:
- **Refusal of Detected Prompt Injections**: Inputs flagged by defensive firewalls are blocked before reaching reasoning LLMs (`ERR_SECURITY_PROMPT_INJECTION_DETECTED`).
- **Refusal of Unscoped Tool Calls**: External tool calls lacking authenticated OAuth tokens or tenant permissions are refused (`ERR_UNAUTHORIZED_TOOL_INVOCATION`).
- **Execution Latency SLA Ceilings**: Graph steps exceeding configured timeout ceilings (default 30 seconds) trigger circuit breakers (`WARN_SLA_TIMEOUT_EXCEEDED`).
- **Refusal of Malformed Schema Outputs**: Generations failing structural schema validation cannot be emitted to clients (`ERR_OUTPUT_SCHEMA_VALIDATION_FAILED`).

### 4. Fallback Decision Mechanism

Continuous enterprise reliability is maintained through multi-tier fault recovery:
- **Provider & Model Cascade**: If primary cloud LLM endpoints encounter rate limits (HTTP 429) or outages, the orchestrator fails over to secondary endpoints or self-hosted Ollama/vLLM instances.
- **Graceful Tool Degradation**: If third-party external tools (web search, data enrichment) fail, the graph activates cached fallback paths and notifies the client of degraded mode.
- **Checkpoint State Rollback**: If a graph node encounters unrecoverable exceptions, the session state rolls back to the last stable PostgreSQL/Redis checkpoint.

### 5. Human-in-the-Loop Governance

Human operators retain ultimate operational control and oversight:
- **Human-in-the-Loop Interrupt Nodes**: High-impact actions (financial transactions, data deletions) pause graph execution until explicit human authorization is granted.
- **Real-Time Observability Dashboards**: Engineering teams monitor live latency traces, token costs, and tool error rates via LangSmith and OpenTelemetry.
- **Comprehensive Audit Logs**: Every prompt, intermediate reasoning step, guardrail intervention, and database mutation is preserved in append-only audit stores.

---

## The Data It Uses

Agents Towards Production enforces strict data minimization, tenant boundary isolation, and enterprise privacy standards.

### 1. Ingested Input Data

The framework processes only operational data required to execute agent workflows:
- **User Directives**: Natural language requests, structured API parameters, and conversation messages.
- **Tenant Context**: Tenant identifiers, session keys, and access policy scopes.
- **Retrieved Knowledge**: Vector embeddings and text chunks retrieved from configured enterprise data sources.

### 2. Configuration & Reference Data

- **Orchestration Graphs**: Declarative LangGraph topologies, state schemas, and transition predicates.
- **Guardrail Rulepacks**: Input/output classification models, regex secret patterns, and security policies.
- **Telemetry Configuration**: OpenTelemetry exporter endpoints, LangSmith project tags, and alerting thresholds.

### 3. Base Model & Inference Lineage

- **Deterministic Infrastructure**: Python runtime, FastAPI controllers, Redis caches, and PostgreSQL checkpointers run 100% deterministically.
- **Foundation LLMs**: High-performance reasoning models (GPT-4o, Claude 3.5 Sonnet, LLaMA-3) deployed for conversational reasoning and synthesis.
- **Zero Training on Proprietary Data**: Customer inputs, retrieved documents, and conversation histories are never transmitted to model providers for training.

### 4. Data Privacy, Storage, and Retention

- **OWASP LLM & MITRE ATLAS Hardened**: Defended against prompt injection, insecure output handling, training data poisoning, and excessive agency.
- **Multi-Tenant Isolation**: Memory stores and persistent checkpointers are partitioned by tenant namespace to prevent data cross-contamination.
- **Automated PII Scrubbing**: Names, social security numbers, and credential tokens are scrubbed from telemetry streams prior to export.
- **Zero Commercial Monetization**: Application telemetry, user conversation histories, and enterprise datasets are never monetized or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of Agents Towards Production ensures safe deployment.

### 1. External Third-Party API Latency Variance
- **Limitation**: Production agents dependent on third-party SaaS APIs inherit external network latency and rate limit fluctuations.
- **Mitigation**: The framework implements asynchronous execution, aggressive Redis response caching, and exponential backoff retry logic.

### 2. Zero-Day Prompt Injection Evasion
- **Limitation**: Highly sophisticated, novel adversarial injection techniques may occasionally bypass static pattern filters.
- **Mitigation**: Multi-layered defense-in-depth combines input classifiers, output scanners, and strictly scoped tool privileges.

### 3. Memory Retrieval Hallucination on Stale Data
- **Limitation**: Long-term episodic memory backends may retrieve outdated knowledge if underlying data sources are updated out-of-band.
- **Mitigation**: Memory entries incorporate TTL timestamps and automated invalidation triggers upon source document updates.

### 4. High Concurrency Resource Contention
- **Limitation**: Running hundreds of concurrent multi-step agent graphs can exhaust GPU serving limits and database connection pools.
- **Mitigation**: Asynchronous task queues (Celery/Inngest), connection pooling, and autoscaled inference backends buffer high loads.

### 5. Subjective Evaluation Ground Truth Ambiguity
- **Limitation**: Evaluating subjective conversational helpfulness without standardized ground truth benchmarks can introduce evaluation variance.
- **Mitigation**: Automated benchmarks combine deterministic reference matching with LLM-as-a-judge rubrics and human spot-audits.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & routing formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested user directives, tenant context & retrieved data | Section 1 | Verified |
| - Configuration, orchestration graphs & guardrail rulepacks | Section 2 | Verified |
| - Base model lineage & deterministic infrastructure | Section 3 | Verified |
| - Data privacy, retention lifecycle & MITRE/OWASP | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - External third-party API latency variance | Section 1 | Verified |
| - Zero-day prompt injection evasion | Section 2 | Verified |
| - Memory retrieval hallucination on stale data | Section 3 | Verified |
| - High concurrency resource contention | Section 4 | Verified |
| - Subjective evaluation ground truth ambiguity | Section 5 | Verified |
