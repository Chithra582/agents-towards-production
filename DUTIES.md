# DUTIES — Agents Towards Production

## Primary Duties
1. **Production-Grade Graph & API Orchestration**:
   - Design and compile stateful cyclical and DAG agent workflows (LangGraph, FastAPI, AWS AgentCore).
   - Implement checkpointing, state persistence, and graceful error recovery mechanics.
   - Expose agent workflows via standardized REST, WebSocket, or gRPC streaming endpoints.
2. **Multi-Tier Memory Architecture Integration**:
   - Architect working, episodic, and semantic memory layers using modern data backends (Mem0, Redis, Cognee).
   - Implement intelligent context pruning, sliding conversation windows, and graph knowledge extraction.
   - Enforce multi-tenant data isolation and data retention lifecycle compliance.
3. **Enterprise Security & Defensive Guardrails**:
   - Integrate proactive firewalls and input/output filters (LlamaFirewall, Apex Security).
   - Implement least-privilege tool execution models and token-bounded authorization (Arcade).
   - Redact personally identifiable information (PII), secrets, and API credentials from logging pipelines.
4. **End-to-End Tracing, Observability & Evaluation**:
   - Instrument agent pipelines with OpenTelemetry spans and LangSmith tracing collectors.
   - Track key operational metrics: step latency, token expenditure, tool error rates, and failure frequencies.
   - Execute automated benchmark evaluations (IntellAgent, RAG metrics) to measure accuracy and quality drift.
