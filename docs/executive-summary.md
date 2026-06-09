# Field Sales Agent Executive Summary

## 1. Executive Overview

Field Sales Agent is a DecisionTrace AI reference app for governed field-sales workflows. The first workflow, DecisionTrace — Quote Assist Agent, helps a sales rep turn a natural-language request into a grounded, approval-aware draft quote while preserving enterprise controls.

**Natural language in; governed workflow out.**

The architecture demonstrates how AI can assist field sales without turning a generic chatbot loose on pricing, inventory, product claims, approvals, or customer commitments. Language models are used only in bounded roles, while deterministic workflow controls, tool boundaries, guardrails, audit trace, cost telemetry, and evaluation define the operating model.

## 2. Portfolio Positioning

Field Sales Agent demonstrates enterprise AI architecture depth across orchestration, governance, integration, retrieval, validation, auditability, cost visibility, monitoring, and evaluation. It is intended as a reference design for moving beyond isolated AI pilots toward reusable enterprise AI control patterns.

## 3. Business Problem

Field sales reps need fast access to account context, product details, inventory availability, pricing rules, discount policy, and quote guardrails. A generic chatbot can overpromise, miss approval boundaries, cite unsupported product claims, or imply commitments such as final order creation or shipment.

Field Sales Agent solves this by separating:

- language understanding
- workflow control
- enterprise tool access
- evidence retrieval
- business guardrails
- response drafting
- auditability
- telemetry

This separation is the core enterprise architecture point: AI can accelerate the experience, but governed systems decide what can happen.

## 4. What the Workflow Demonstrates

The Quote Assist Agent demonstrates an end-to-end governed sales workflow:

1. Rep enters a natural-language request.
2. OpenAI-assisted intake extracts intent and entities when enabled.
3. Deterministic validation decides whether the workflow can start.
4. LangGraph controls the quote workflow sequence.
5. MCP tools expose bounded capabilities.
6. Enterprise adapters map canonical payloads to mock enterprise APIs.
7. LlamaIndex-backed MCP retrieval gets product/spec evidence with citations.
8. Inventory and pricing are checked through governed tool calls.
9. Quote guardrails decide allow, approval required, or block.
10. Draft quote is created only if allowed.
11. OpenAI may draft a rep-facing response only after the outcome is determined.
12. Deterministic validation checks the response before display.
13. Audit trace, cost telemetry, monitoring, and evaluation validate the run.

## 5. Architecture Differentiation

Field Sales Agent is deeper than a simple chatbot because the architecture separates AI assistance from control authority.

Key layers include:

- OpenAI-assisted intake extraction
- deterministic readiness gate
- LangGraph workflow control
- MCP tools/resources
- LlamaIndex-backed product/spec RAG
- canonical enterprise payload model
- enterprise API adapter layer
- mock MuleSoft / enterprise API endpoints
- deterministic guardrails
- audit, cost, monitoring, and evaluation

Warranty-style workflow pattern:

```text
LangGraph -> governed Python tools -> simulated/future enterprise adapters
```

Field Sales Agent pattern:

```text
LangGraph -> MCP tools/resources -> canonical payloads -> enterprise adapters and LlamaIndex-backed retrieval -> mock enterprise APIs/product-spec documents
```

This makes Field Sales Agent a strong reference pattern for revenue workflows where AI needs to help users move quickly without bypassing enterprise controls.

## 6. Intentional LangGraph + MCP + LlamaIndex Design

LangGraph is the control layer. It decides the sequence, branching, and workflow outcome path.

MCP is the capability boundary. It exposes tools/resources such as account lookup, product retrieval, inventory check, pricing calculation, product/spec retrieval, and draft quote creation.

LlamaIndex is not called directly by the workflow. It sits behind the MCP retrieval capability and provides grounded product/spec evidence with citations.

**LlamaIndex has evidence authority, not decision authority.**

Correct retrieval pattern:

```text
LangGraph node
-> MCP tool wrapper: retrieve_product_specs
-> LlamaIndex retrieval service
-> product/spec documents
-> cited evidence
-> MCP result
-> LangGraph workflow state
-> quote guardrail evaluation
```

LlamaIndex does not approve quotes. It does not create draft quotes. It does not calculate pricing. It does not check inventory. It does not override guardrails.

## 7. Enterprise Adapter Pattern

The system uses canonical internal payloads and an adapter layer so client-specific MuleSoft/API payloads do not force workflow redesign.

```text
LangGraph node
-> MCP tool contract
-> canonical request model
-> enterprise API adapter
-> client-specific MuleSoft/API payload
-> enterprise endpoint/system of record
```

This is a reusable accelerator pattern: the control model stays stable while client-specific API mappings are isolated in adapters.

For example, a mock inventory endpoint can later be replaced by a real MuleSoft inventory API without redesigning:

- LangGraph workflow
- MCP tool contract
- guardrails
- audit model
- monitoring dashboard
- evaluation scenarios

## 8. Safety and Governance Boundaries

The app intentionally prevents unsupported commitments.

Allowed:

- draft quote preparation
- account/product/inventory/pricing analysis
- approval-aware recommendations
- rep-facing summary drafting

Not allowed:

- final order submission
- payment processing
- shipment creation
- fulfillment execution
- bypassing approval
- unsupported product claims

OpenAI is used in bounded roles:

- intake understanding
- optional response drafting after outcome

OpenAI does not choose tool order, approve quotes, calculate pricing, decide inventory, create draft quotes, override guardrails, or submit final orders.

## 9. Observability, Auditability, and Cost Telemetry

Field Sales Agent demonstrates enterprise operating controls, not just generation.

The architecture includes:

- correlation ID across intake and workflow
- audit timeline
- architecture-layer labels: Business Event, LangGraph Node, MCP Tool, Enterprise Adapter, Mock Enterprise Endpoint
- MCP tool call details
- RAG evidence details with citations
- cost telemetry separating intake LLM usage from workflow drafting LLM usage
- monitoring dashboard with persisted workflow outcomes

Cost telemetry does not fake dollar cost. Estimated cost requires configured rates. Token values should appear only when returned by provider usage metadata.

## 10. Evaluation Strategy

The app includes local golden-scenario evaluation. Golden scenarios validate:

- missing details -> clarification
- unsupported product combination -> block
- inventory shortage -> approval required
- discount above threshold -> approval required
- valid quote -> draft quote created

Assertions check:

- outcome correctness
- no final order/payment/shipment/fulfillment
- audit integrity
- RAG grounding
- cost telemetry integrity
- guardrail behavior
- response safety

Local deterministic evaluation is the source of truth for control behavior. LLM-as-judge and LangSmith evaluation are future enhancements.

## 11. Demo Story

Example prompt:

> “westlake highschool wants 50 blue helmets. create a quote”

Expected narrative:

- OpenAI intake extracts Westlake High School, 50, blue helmets when enabled.
- Deterministic readiness validation allows the workflow to start.
- LangGraph executes governed workflow steps.
- MCP tools retrieve account context, product evidence, inventory, pricing, and quote creation capabilities.
- LlamaIndex-backed MCP retrieval provides cited product/spec evidence.
- Guardrails decide whether the quote can proceed.
- Draft quote is created only if allowed.
- Response is drafted safely after the outcome.
- Audit and cost telemetry prove what happened.

Contrasting case:

> “westlake highschool wants 100 blue helmets. prepare a quote”

If inventory is insufficient, the workflow may require approval. No draft quote is created when guardrails require approval.


## 12. Phase 1 Validation Status

Phase 1 has been validated as a deployed release candidate for public demo and architecture review. The validated scenarios confirm:

- deployed demo validated
- valid quote creates a draft quote
- inventory shortage requires approval
- unsupported product configuration is blocked
- final order/shipment request is blocked at intake
- no final order/payment/shipment/fulfillment is created

This validation does not claim production readiness, real enterprise integration, or regulatory compliance. It confirms that the public demo narrative aligns with the governed Quote Assist control model and release-candidate behavior.

## 13. Public vs Private Repo Boundary

This public repo contains architecture, executive summary, diagrams, API examples, and demo narrative. The full runnable implementation, MCP server code, LlamaIndex pipeline, database/schema details, cost telemetry logic, reusable orchestration code, and proprietary accelerator internals remain in a private implementation repo.

Do not include:

- secrets
- API keys
- database files
- private implementation code
- real customer data
- real product data
- proprietary accelerator internals

## 14. Roadmap

Future directions include:

- cost rate configuration and cost-per-outcome reporting
- model routing and prompt optimization
- semantic/prompt caching
- LangSmith evaluation integration
- LLM-as-judge for response quality
- tau-bench-inspired dynamic agent evaluation
- persistent trace-to-evaluation improvement loop
- production-grade authentication and authorization
- Salesforce/CPQ integration
- human approval workflow integration
