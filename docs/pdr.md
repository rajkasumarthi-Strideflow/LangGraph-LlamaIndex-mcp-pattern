# Field Sales Agent PDR

## 1. Product Summary

Field Sales Agent is a governed AI-assisted workflow app for field sales reps. The Phase 1 workflow, Quote Assist Agent, helps a rep assemble a grounded draft quote for a customer meeting without creating a final order.

## 2. Phase 1 Scope

### In Scope

- Natural-language sales request intake
- Required-facts validation
- Account context retrieval from synthetic CRM data
- Product/spec retrieval using LlamaIndex-backed RAG
- Inventory check using MCP-style tool
- Pricing and discount calculation using deterministic rules
- Quote guardrail check
- Draft quote creation
- Rep-facing summary generation
- Audit events
- Correlation ID
- Cost telemetry
- Local golden-scenario evaluation
- Monitoring dashboard design

### Out of Scope

- Final order submission
- Payment
- Shipment
- Real CRM/CPQ/ERP integrations
- Real customer data
- Real geolocation
- Voice interface
- Salesforce/Agentforce implementation
- CrewAI
- LLM-as-judge
- Rego/OPA policy engine
- Production authentication/security model

## 3. Primary User

Mobile field sales representative preparing for or conducting a school/team equipment sales meeting.

## 4. Business Problem

Field reps need fast access to account history, product/spec details, availability, pricing rules, and discount guardrails while preparing customer-ready quote drafts. Without governed workflow controls, AI-generated quote assistance can overpromise, misuse unsupported product claims, apply unauthorized discounts, or create unapproved commitments.

## 5. Phase 1 Demo Scenario

A rep asks:

> “I’m meeting Westlake High School about helmets and jerseys. They want 50 varsity helmets in matte navy and matching jerseys. Build a draft quote with the standard booster club discount.”

Expected system behavior:

- Identify account context
- Retrieve relevant product/spec evidence
- Validate color/product compatibility
- Check inventory
- Calculate quote lines
- Apply discount rules
- Run quote guardrails
- Create draft quote if allowed
- Produce rep-facing summary with caveats
- Record audit, trace, monitoring, and cost telemetry

## 6. DecisionTrace Control Model

- Router interprets request and extracts facts
- Workflow state controls execution
- MCP tools/resources provide bounded access
- LlamaIndex retrieves grounded evidence
- Deterministic guardrails control quote creation
- LLM does not finalize orders or override policy
- Quote creation is draft-only
- Audit and correlation support replay
- Monitoring tracks business/control outcomes
- Evaluation validates expected workflow behavior

## 7. Business Rules / Policies

Phase 1 policy rules are public-safe examples written in Markdown and YAML/JSON-friendly structures. Rego/OPA is intentionally out of scope for Phase 1.

```yaml
quote_policy:
  final_order_creation_allowed: false
  require_account_context: true
  require_product_spec_reference: true
  require_inventory_available_for_quote: true
  standard_discount_percent: 10
  manager_approval_required_above_percent: 15
  max_discount_percent: 25
  unsupported_product_claims_block_quote: true
  draft_quote_requires_guardrail_allow: true
```

Interpretation:

- A draft quote may be created only when account context, product evidence, inventory, pricing, and guardrail checks pass.
- Discounts above 15 percent require manager approval.
- Discounts above 25 percent are blocked in Phase 1.
- Unsupported product claims block draft quote creation.
- Final order creation is never allowed in Phase 1.

## 8. Phase 1 Workflow Outcomes

- `clarification_required`
- `invalid_product_or_identifier`
- `blocked_by_policy`
- `approval_required`
- `draft_quote_created`

## 9. Success Criteria

- The workflow creates a draft quote only when required facts, product evidence, inventory, pricing, and guardrails pass.
- Unsupported or unavailable product requests are blocked or escalated.
- Discounts above threshold require approval.
- Generated response does not imply final order or shipment.
- Cost telemetry records LLM, RAG, and MCP tool usage.
- Audit trail can replay the decision path.
- Monitoring can show workflow outcomes by workflow type.
