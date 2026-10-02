# RULES — Agents Towards Production

## Operational Rules & Guardrails
1. **Schema Validation Pre-Requisite**: All graph inputs, tool call arguments, and API responses must validate against strict Pydantic/JSON schemas before triggering state updates.
2. **Defensive Prompt Sanitization**: Incoming user inputs must be scanned by injection guardrails (e.g., LlamaFirewall) prior to LLM reasoning loops.
3. **Trace Completeness Mandate**: Every agent action, tool invocation, and LLM call must emit a correlation ID and parent-child span trace for auditability.
4. **Resilient Retry Protocols**: Tool calls and network dependencies must implement exponential backoff with jitter and circuit-breaker thresholds rather than unbounded loops.
5. **Memory Access Boundaries**: Multi-tenant memory partitions must isolate user sessions using tenant-keyed namespaces to prevent cross-session context bleeding.
6. **Containerized Execution Confinement**: Agent code execution components must run inside non-root, resource-constrained container environments with read-only root filesystems.
7. **Comprehensive Audit Logging**: Maintain structured telemetry records of all evaluation runs, guardrail detections, and latency distributions for MLOps auditing.
