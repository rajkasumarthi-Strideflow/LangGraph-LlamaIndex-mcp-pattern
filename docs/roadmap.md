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

## Phase 2C Status: Lightweight Agentforce Prototype Complete

Phase 2C validated a lightweight Agentforce implementation path using agent instructions, actions, Flow, and Prompt Builder. The goal was not to recreate the full custom Quote Assist reference app in a limited trial org, but to show how the same enterprise AI control patterns map into Salesforce-native capabilities.

The full Field Sales Agent architecture remains tool-agnostic. Phase 2C validates how selected control-plane concepts can be implemented in Agentforce using scoped agent behavior, bounded actions, Flow-backed workflow handoff, prompt-governed response generation, and safe response boundaries.

## Updated Phase 2 Roadmap

Completed:

- **Phase 2B — Agentforce Implementation Mapping**
- **Phase 2C — Lightweight Agentforce Prototype**

Next:

1. **Phase 2D — Evaluation and Release Quality Gates**
2. **Phase 2E — Cost Rate Configuration and Cost-per-Outcome Analytics**
3. **Phase 2F — Human Approval Handoff Pattern**
4. **Later — Policy Version Promotion / Policy Workbench**

## Later Enhancements

- LangSmith evaluation
- LLM-as-judge evaluation
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

## Public-Safe Boundary

The roadmap describes architecture direction. Implementation details, internal accelerator logic, reusable private components, and proprietary schemas should remain in a private implementation repo.

## Executive Summary

For an executive and architecture-leader overview of the reference app, see [Field Sales Agent Executive Summary](executive-summary.md).
