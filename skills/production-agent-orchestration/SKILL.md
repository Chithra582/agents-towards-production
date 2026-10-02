---
name: "production-agent-orchestration"
description: "Architects and orchestrates resilient multi-step agent graphs and microservice endpoints."
license: MIT
---

# Production Agent Orchestration

## Overview
This skill designs, validates, and deploys production-grade agent workflows using cyclical state graph frameworks (LangGraph) and high-concurrency microservice APIs (FastAPI).

## Key Capabilities
- **Graph Topology Design**: Constructs resilient nodes, conditional edges, and state checkpointing mechanisms.
- **State Persistence**: Configures durable thread stores (PostgreSQL, SQLite) for reliable session continuation.
- **Streaming APIs**: Implements real-time token and event streaming over Server-Sent Events (SSE) and WebSockets.

## Operational Workflow
1. **Requirements Mapping**: Analyze multi-step reasoning needs, tool dependencies, and branch conditions.
2. **State Graph Compilation**: Author state schemas, node handlers, and transition predicates.
3. **Checkpoint Binding**: Attach persistent thread storage checkpointers for fault tolerance.
4. **Service Exposure**: Wrap compiled graphs in FastAPI route controllers with asynchronous handlers.
