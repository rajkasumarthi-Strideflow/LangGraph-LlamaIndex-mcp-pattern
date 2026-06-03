# Field Sales Agent Demo Script

## Purpose

This is a 5-minute demo narrative for the DecisionTrace — Quote Assist Agent reference workflow.

## 1. Opening

Field Sales Agent is a DecisionTrace AI reference app for governed field-sales workflows. The first workflow is Quote Assist Agent, which helps a mobile rep prepare a grounded draft quote without creating a final order or unsupported commitment.

## 2. Control Model

This app uses the same DecisionTrace control model as the warranty workflow, but with a different tool access pattern:

- LangGraph controls workflow state and routing.
- MCP-style tools/resources provide bounded access to account, inventory, pricing, and quote functions.
- LlamaIndex retrieves grounded product/spec evidence.
- Guardrails decide whether draft quote creation is allowed, blocked, or requires approval.
- Cost telemetry is captured from day one.

## 3. Scenario

A rep says:

> “I’m meeting Westlake High School about helmets and jerseys. They want 50 varsity helmets in matte navy and matching jerseys. Build a draft quote with the standard booster club discount.”

## 4. Walkthrough

1. Show natural-language intake and required-facts extraction.
2. Explain that the router interprets the request but does not create quotes.
3. Show account context retrieval from synthetic CRM data.
4. Show LlamaIndex-backed product/spec retrieval.
5. Show inventory and pricing checks through MCP-style tools.
6. Show quote guardrail decision.
7. Show draft quote created only if controls pass.
8. Show audit replay and correlation ID.
9. Show cost telemetry for LLM, RAG, and MCP usage.

## 5. Key Message

The AI assists the rep, but the control model governs the workflow. The app is draft-only, evidence-grounded, approval-aware, auditable, and cost-visible.

## 6. Closing

Field Sales Agent demonstrates how DecisionTrace AI can extend from support workflows into revenue workflows while preserving the same governance pattern: route, retrieve, validate, guard, audit, measure, and improve.
