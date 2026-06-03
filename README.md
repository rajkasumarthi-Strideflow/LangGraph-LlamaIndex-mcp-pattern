# Field Sales Agent

**DecisionTrace — Quote Assist Agent**

Field Sales Agent is a DecisionTrace AI reference app for governed field-sales workflows. The first workflow, Quote Assist Agent, helps a mobile sales rep prepare a grounded, approval-aware draft quote using account context, product/spec retrieval, inventory checks, pricing rules, quote guardrails, audit replay, cost telemetry, and monitoring.

Warranty Replacement proved the DecisionTrace control model using governed Python tool wrappers. Field Sales Agent demonstrates the same control model using an MCP-style tool/resource abstraction and LlamaIndex-backed product/spec RAG.

## Control Model Principle

LangGraph controls the workflow.
MCP exposes bounded tools/resources.
LlamaIndex retrieves grounded product/spec evidence.
Guardrails control quote readiness and approval boundaries.
Cost telemetry measures operating cost.
Audit, tracing, monitoring, and evaluations validate the control model.

## What This Public Repo Contains

This public repo contains architecture and demo artifacts for the Field Sales Agent reference app. It is intended for portfolio review, architecture discussion, implementation planning, and public-safe demonstration of the DecisionTrace control model.

Included artifacts:

- Lightweight PDR for Quote Assist Agent
- Architecture overview and public/private boundary
- C4 context and container diagrams
- Workflow, retrieval, cost telemetry, and rollout diagrams
- MCP/LlamaIndex pattern explanation
- Public-safe API contract examples
- Cost telemetry design
- Rollout and rollback design
- Synthetic demo scenarios
- Demo script and public-safe roadmap

## Public / Private Repo Boundary

This public repo contains architecture and demo artifacts. The full runnable implementation, MCP server, LlamaIndex pipeline, database/schema details, cost telemetry logic, and reusable accelerator internals should remain in a private implementation repo.

This repository does not include proprietary implementation code, private database schemas, secrets, reusable accelerator internals, or a full runnable backend implementation.

## Phase 1 Workflow

Quote Assist Agent supports a governed field-sales scenario where a rep asks for a draft quote before a customer meeting. The workflow gathers required facts, retrieves account and product evidence, checks inventory, applies deterministic pricing rules, evaluates quote guardrails, creates a draft quote only when allowed, and records audit and cost telemetry.

The workflow is draft-only. It does not submit final orders, collect payment, trigger shipment, or create unsupported customer commitments.

## Repository Structure

```text
README.md
docs/
  pdr.md
  architecture.md
  diagrams.md
  api-contracts.md
  cost-telemetry.md
  rollout-rollback.md
  demo-script.md
  roadmap.md
examples/
  synthetic-scenarios.md
  sample-api-payloads.json
```

## Documentation Index

- [Product Definition Requirements](docs/pdr.md)
- [Architecture Overview](docs/architecture.md)
- [Architecture Diagrams](docs/diagrams.md)
- [API Contract Examples](docs/api-contracts.md)
- [Cost Telemetry Design](docs/cost-telemetry.md)
- [Rollout and Rollback](docs/rollout-rollback.md)
- [Demo Script](docs/demo-script.md)
- [Roadmap](docs/roadmap.md)
- [Synthetic Scenarios](examples/synthetic-scenarios.md)
- [Sample API Payloads](examples/sample-api-payloads.json)
