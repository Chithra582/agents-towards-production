---
name: "observability-evaluation-pipeline"
description: "Deploys real-time tracing, telemetry instrumentation, and rigorous agentic evaluation benchmarks."
license: MIT
---

# Observability and Evaluation Pipeline

## Overview
This skill implements production observability and offline/online evaluation frameworks, providing comprehensive visibility into agent decision quality, latency, token costs, and system failures.

## Key Capabilities
- **Distributed Tracing**: Captures complete invocation call trees across nested LLM steps, tool calls, and retriever queries (LangSmith, OpenTelemetry).
- **Automated Benchmarking**: Executes standardized evaluation datasets (IntellAgent, Ragas) to measure precision, recall, and faithfulness.
- **Regression Detection**: Quantifies prompt engineering and model updates against historical baselines before production rollout.

## Operational Workflow
1. **Instrumentation**: Inject tracing callbacks and correlation headers into graph orchestrator steps.
2. **Telemetry Collection**: Stream latency metrics, token consumption, and error counts to monitoring dashboards.
3. **Benchmark Execution**: Run test suites against designated ground truth datasets to score agent accuracy.
4. **Evaluation Analysis**: Generate scorecard visualizations and highlight regression edge cases for remediation.
