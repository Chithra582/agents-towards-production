---
name: "agent-security-guardrails"
description: "Integrates defensive firewalls, prompt injection filters, and secure tool-calling authorization."
license: MIT
---

# Agent Security Guardrails

## Overview
This skill hardens production agent systems against adversarial threats, malicious jailbreaks, indirect prompt injection, and unauthorized data exfiltration.

## Key Capabilities
- **Firewall Filtering**: Integrates real-time prompt classification models (LlamaFirewall, Apex) to intercept jailbreaks.
- **Secure Tool Invocation**: Implements scoped API tokens, user authorization handshakes, and input schema validation (Arcade).
- **Sensitive Data Masking**: Detects and sanitizes PII, API tokens, and confidential corporate data before logging or LLM transmission.

## Operational Workflow
1. **Threat Modeling**: Identify untrusted ingestion surfaces (user chat, scraped web data, third-party APIs).
2. **Guardrail Deployment**: Position input-scanning interceptors at entry points and output scrubbers at exit boundaries.
3. **Permission Scoping**: Restrict tool privileges to minimal necessary operations with user approval gates.
4. **Security Auditing**: Emit tamper-evident security telemetry whenever an injection or violation is blocked.
