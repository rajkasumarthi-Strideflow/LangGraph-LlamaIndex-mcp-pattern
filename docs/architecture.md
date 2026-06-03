# Field Sales Agent Architecture

## Purpose

Field Sales Agent demonstrates how the DecisionTrace control model can be applied to governed field-sales workflows. The reference workflow, Quote Assist Agent, helps a rep prepare a grounded draft quote while keeping high-risk business actions under deterministic control.

## Architecture Pattern

Field Sales Agent is an architecture/demo repository, not a full implementation. It describes a future implementation pattern where LangGraph manages stateful workflow execution, MCP-style interfaces expose bounded tools and resources, LlamaIndex retrieves product/spec evidence, and deterministic guardrails control draft quote readiness.

## Same Control Model, New Tool Access Pattern

Warranty Replacement:

```text
LangGraph node -> governed Python tool wrapper -> simulated/future enterprise API adapter
```

Field Sales Agent:

```text
LangGraph node -> MCP client/tool interface -> MCP server -> LlamaIndex RAG + simulated enterprise tools/resources
```

The control principle stays the same: workflow state and guardrails control execution. The access pattern changes from direct Python tool wrappers to MCP-style tools/resources and a retrieval layer.

## Core Components

- **Natural-language intake router:** Interprets rep requests, extracts required facts, and asks clarifying questions.
- **LangGraph workflow:** Controls state, node execution, routing, outcomes, and correlation.
- **MCP client/tool interface:** Gives workflow nodes bounded access to tools and resources.
- **MCP server:** Public-safe pattern for account, inventory, pricing, quote, and product/spec resource access.
- **LlamaIndex RAG layer:** Retrieves grounded product/spec evidence for quote readiness.
- **Quote guardrails:** Determine whether draft quote creation is allowed, blocked, or requires approval.
- **Audit and trace capture:** Records workflow events, evidence references, decisions, and outcomes.
- **Cost telemetry:** Tracks LLM, RAG, and MCP usage from day one.
- **Monitoring/evaluation layer:** Validates workflow health, control outcomes, and golden scenarios.

## MCP Tool/Resource Layer

The MCP-style layer separates workflow control from enterprise data access. Tools and resources should be bounded, typed, and auditable.

Example public-safe interfaces:

- `get_account_context(account_name_or_id)`
- `search_product_specs(query, filters)`
- `check_inventory(product_id, quantity, configuration)`
- `calculate_quote_lines(items, discount_code)`
- `create_draft_quote(account_id, quote_lines, guardrail_result)`
- `get_quote_policy(policy_version)`

Tools should return summarized, minimum necessary data. They should not expose private schemas or sensitive customer records in public artifacts.

## LlamaIndex RAG Layer

The RAG layer retrieves product/spec evidence used to ground recommendations and validate quote readiness. It should support:

- Product family filters
- Spec/version references
- Compatibility evidence
- Unsupported claim detection
- Evidence IDs for audit replay
- Retrieved chunk counts for cost telemetry

LlamaIndex helps organize retrieval, metadata filtering, citation-ready evidence, and future evaluation workflows.

## Cost Telemetry Layer

Cost telemetry is included in Phase 1 design, even though cost-optimized orchestration is future work. The platform should track:

- LLM calls and token usage
- RAG calls and retrieved chunks
- MCP tool calls
- Estimated cost when configured rates are available
- Cost per draft quote attempt
- Cost by workflow outcome

## Audit / Trace / Monitoring / Evaluation

The control model is validated through multiple evidence layers:

- **Audit:** Business-readable event history for replay.
- **Trace:** Technical execution path and spans.
- **Monitoring:** Operational and control health metrics.
- **Evaluation:** Golden scenarios that validate required behavior before rollout.

Production issues should eventually become regression tests, but this public repo describes that architecture rather than implementing it.

## Public vs Private Repo Boundary

This public repo documents the architecture and demo design. A private implementation repo should hold runnable backend code, MCP server logic, LlamaIndex ingestion/retrieval code, private schema details, credentials, reusable accelerator internals, and deployment-specific configuration.
