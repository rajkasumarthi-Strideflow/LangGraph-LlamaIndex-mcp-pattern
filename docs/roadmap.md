# Field Sales Agent Roadmap

## Phase 1

- Quote Assist Agent MVP
- Natural-language intake readiness gate
- Optional OpenAI-assisted intake extraction with deterministic validation
- MCP-style tools/resources
- LlamaIndex-backed MCP `retrieve_product_specs` capability
- Cost telemetry with intake/workflow drafting usage separation
- Optional validated OpenAI rep-facing response drafting
- Draft quote workflow
- Audit Trace and Cost Telemetry UI concepts
- Audit/monitoring/evaluation architecture
- Synthetic account/product/inventory/pricing data
- Public-safe API contract examples
- Controlled rollout/rollback design

## Phase 1 Validation Status

Phase 1 is a deployed release candidate validated against the public demo scenarios. The validated release confirms the Quote Assist control model, audit trace, cost telemetry, monitoring, and evaluation narrative while preserving the public/private implementation boundary.

## Future Enhancements

- Cost rate configuration and cost-per-outcome analytics
- LangSmith evaluation
- LLM-as-judge evaluation
- OPA/Rego policy-as-code
- Salesforce/CPQ integration mapping
- Agentforce pattern mapping
- CrewAI review crew if needed
- Persistent production database
- Production authentication/security hardening
- Persistent intake funnel metrics
- Production hardening for workflow response drafting
- Dynamic model routing
- Prompt caching
- Semantic caching
- Voice interface
- Tau-bench-inspired dynamic evaluation
- Persistent trace-to-evaluation improvement loop
- Enterprise API adapter framework
- Human approval workflow integration

## Public-Safe Boundary

The roadmap describes architecture direction. Implementation details, internal accelerator logic, reusable private components, and proprietary schemas should remain in a private implementation repo.

## Executive Summary

For an executive and architecture-leader overview of the reference app, see [Field Sales Agent Executive Summary](executive-summary.md).
