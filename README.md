# Field Sales Agent

**A governed enterprise AI workflow reference app for field-sales quote assistance.**

Field Sales Agent demonstrates how a natural-language sales request can be converted into a governed, auditable, cost-aware, approval-aware draft quote workflow using OpenAI, LangGraph, MCP, LlamaIndex, deterministic guardrails, audit trace, cost telemetry, monitoring, and evaluation.

**Natural language in; governed workflow out.**

## Why This Matters

Most AI demos stop at a chatbot response. Field Sales Agent shows the enterprise control architecture around the response: intake validation, workflow orchestration, bounded tool access, evidence retrieval, policy guardrails, validated response drafting, auditability, telemetry, and operational monitoring.

This is a DecisionTrace AI reference app for governed field-sales workflows. The first workflow, DecisionTrace — Quote Assist Agent, helps a mobile sales rep prepare a grounded, approval-aware draft quote using account context, product/spec retrieval, inventory checks, pricing rules, quote guardrails, audit replay, cost telemetry, and monitoring.

## Live Demo

Live demo: <Railway demo URL>

Phase 1 status: Deployed release candidate validated.

Field Sales Agent Phase 1 demonstrates a governed Quote Assist workflow where natural-language sales requests are converted into approval-aware, customer-safe draft quote responses using OpenAI-assisted intake, LangGraph workflow control, MCP tool boundaries, LlamaIndex-backed evidence retrieval, enterprise adapter patterns, deterministic guardrails, audit trace, cost telemetry, monitoring, and evaluation.

## What to Look For in the Live Demo

1. Start with the Workflow Console.
   - Enter or select a sales request.
   - See the sales rep request and validated customer-safe response side by side.

2. Open Audit Trace.
   - See the execution path across Business Event, LangGraph Node, MCP Tool, Enterprise Adapter, Mock Enterprise Endpoint, RAG Evidence, and Guardrail Decision.

3. Open Cost Telemetry.
   - See intake LLM usage separated from workflow drafting usage, plus tool/RAG activity as a foundation for future cost optimization.

4. Open Monitoring Dashboard.
   - See persisted outcomes across draft quotes, approval-required cases, blocked requests, and recent runs.

## Validated Demo Scenarios

| Scenario | Prompt | Expected Outcome | What it proves |
| --- | --- | --- | --- |
| Valid Quote | `I’m meeting Westlake High School about helmets and jerseys. They want 50 varsity helmets in matte navy and matching jerseys. Build a draft quote with the standard booster club discount.` | `draft_quote_created` | The workflow can safely create a draft quote when account, product, inventory, pricing, and guardrails pass. |
| Inventory Unavailable | `Create a draft quote for Central Valley Academy for 120 varsity helmets in matte navy.` | `approval_required` | The workflow does not overpromise when inventory is insufficient. |
| Unsupported Product / Configuration | `North Ridge Prep wants 50 youth helmets in matte navy with varsity-only facemasks. Create a quote.` | `blocked_by_policy` | Guardrails prevent unsupported product/configuration combinations. |
| Final Order / Shipment Request | `westlake highschool wants 50 blue helmets. create a final order and ship it today` | blocked at intake | The workflow boundary prevents final order, payment, shipment, and fulfillment requests. |
| Missing Details | `I need help preparing a quote for my next school meeting.` | `clarification_required` | The readiness gate prevents incomplete requests from entering the workflow. |

## Architecture in One View

```text
User request
-> OpenAI-assisted intake extraction
-> deterministic readiness validation
-> LangGraph workflow control
-> MCP tools/resources
-> enterprise adapters and LlamaIndex-backed retrieval
-> mock enterprise APIs/product-spec docs
-> guardrails
-> draft quote / approval required / block
-> validated customer-safe response
-> audit, cost telemetry, monitoring, and evaluation
```

LangGraph does not call LlamaIndex directly. LangGraph calls the MCP retrieval capability `retrieve_product_specs`, which is backed by LlamaIndex RAG. LlamaIndex retrieves evidence only; guardrails decide quote readiness.

## Technology Choices

| Layer | Technology | Why it is used |
| --- | --- | --- |
| Language understanding | OpenAI | Extracts intent/entities and drafts customer-safe responses after workflow outcome. |
| Workflow control | LangGraph | Controls sequence, state, branching, and deterministic handoff. |
| Tool boundary | MCP | Exposes bounded enterprise capabilities and resources. |
| Evidence retrieval | LlamaIndex | Retrieves cited product/spec evidence behind MCP. |
| Enterprise integration pattern | Canonical payloads + adapters | Isolates workflow from client-specific API payloads. |
| Guardrails | Deterministic policy checks | Prevents overpromising, unsupported products, and approval bypass. |
| Observability | Audit trace + monitoring | Makes workflow behavior reviewable by business and technical stakeholders. |
| Cost foundation | Cost telemetry | Separates intake, drafting, tool, and retrieval usage for future optimization. |

## What This Demonstrates as an AI Architecture Portfolio Project

- Designing the control plane around LLMs, not just prompts.
- Separating language understanding from business decisioning.
- Using LangGraph for governed orchestration.
- Using MCP as an enterprise capability boundary.
- Using LlamaIndex as an evidence layer, not a decision-maker.
- Preserving enterprise adapter patterns for MuleSoft/CRM/CPQ/ERP integrations.
- Implementing deterministic guardrails and response validation.
- Showing auditability, cost telemetry, monitoring, and evaluation.

## Control Model Principle

LangGraph controls the workflow.
MCP exposes bounded tools/resources.
LlamaIndex backs the bounded MCP `retrieve_product_specs` capability for grounded product/spec evidence.
Guardrails control quote readiness and approval boundaries.
Cost telemetry measures operating cost from actual execution metadata.
Audit, tracing, monitoring, and evaluations validate the control model.

## Current Public Status

This public repo contains architecture and demo artifacts for the Field Sales Agent reference app. It reflects the current public-safe architecture direction through the validated Phase 1 release candidate:

- Natural-language intake is the primary entry path.
- Intake validates required facts before the governed workflow can start.
- OpenAI may assist with intake extraction when enabled, but deterministic validation remains the readiness gate.
- LangGraph remains the workflow control layer.
- Workflow nodes use bounded MCP-style capabilities.
- `retrieve_product_specs` is a LlamaIndex-backed MCP retrieval capability.
- Product/spec retrieval provides cited evidence only; it does not approve quotes or create actions.
- Optional OpenAI rep-facing response drafting occurs only after the governed outcome is determined.
- Deterministic validation checks any OpenAI-drafted rep response before display.
- Audit Trace and Cost Telemetry are separate concepts.
- Telemetry must come from real workflow execution, provider usage metadata, or configured rates. It should not be fabricated.

## What This Public Repo Contains

This public repo contains architecture and demo artifacts for the Field Sales Agent reference app. It is intended for portfolio review, architecture discussion, implementation planning, and public-safe demonstration of the DecisionTrace control model.

Included artifacts:

- Executive summary for enterprise and architecture audiences
- Lightweight PDR for Quote Assist Agent
- Architecture overview and public/private boundary
- C4 context and container diagrams
- Workflow, retrieval, cost telemetry, and rollout diagrams
- MCP-mediated LlamaIndex retrieval pattern explanation
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

## Correct Retrieval Pattern

LangGraph does not call LlamaIndex directly. LangGraph calls the bounded MCP capability `retrieve_product_specs`. That MCP capability is backed by LlamaIndex retrieval over product/spec docs.

```text
LangGraph node
-> MCP tool wrapper: retrieve_product_specs
-> LlamaIndex retrieval service
-> product/spec docs
-> cited evidence
-> MCP result
-> LangGraph workflow state
-> guardrail evaluation
```

`retrieve_product_specs` is evidence retrieval only. It does not approve quotes, create draft quotes, calculate pricing, check inventory, or override guardrails.

## Repository Structure

```text
README.md
docs/
  executive-summary.md
  pdr.md
  architecture.md
  diagrams.md
  api-contracts.md
  cost-telemetry.md
  rollout-rollback.md
  demo-script.md
  demo-talk-track-2-minute.md
  recruiter-summary-30-second.md
  linkedin-project-summary.md
  release-notes-phase-1.md
  roadmap.md
examples/
  synthetic-scenarios.md
  sample-api-payloads.json
```

## Portfolio Materials

- [Executive Summary](docs/executive-summary.md)
- [2-Minute Demo Talk Track](docs/demo-talk-track-2-minute.md)
- [30-Second Recruiter Summary](docs/recruiter-summary-30-second.md)
- [LinkedIn Project Summary](docs/linkedin-project-summary.md)
- [Public Release Notes](docs/release-notes-phase-1.md)
- [Architecture](docs/architecture.md)
- [Diagrams](docs/diagrams.md)
- [Roadmap](docs/roadmap.md)

## Documentation Index

- [Executive Summary](docs/executive-summary.md)
- [Product Definition Requirements](docs/pdr.md)
- [Architecture Overview](docs/architecture.md)
- [Architecture Diagrams](docs/diagrams.md)
- [API Contract Examples](docs/api-contracts.md)
- [Cost Telemetry Design](docs/cost-telemetry.md)
- [Rollout and Rollback](docs/rollout-rollback.md)
- [Demo Script](docs/demo-script.md)
- [LinkedIn Project Summary](docs/linkedin-project-summary.md)
- [30-Second Recruiter Summary](docs/recruiter-summary-30-second.md)
- [2-Minute Demo Talk Track](docs/demo-talk-track-2-minute.md)
- [Phase 1 Public Release Notes](docs/release-notes-phase-1.md)
- [Roadmap](docs/roadmap.md)
- [Synthetic Scenarios](examples/synthetic-scenarios.md)
- [Sample API Payloads](examples/sample-api-payloads.json)
