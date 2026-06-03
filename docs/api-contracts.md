# Field Sales Agent API Contracts

These are proposed API contracts for the private implementation. They are public-safe examples, not runnable implementation code.

## POST /api/intake/session/start

Starts a natural-language intake session.

```json
{
  "message": "I’m meeting Westlake High School about helmets and jerseys. Build a draft quote."
}
```

Response:

```json
{
  "intake_session_id": "intake_demo_001",
  "correlation_id": "corr_demo_001",
  "intent": "quote_assist_request",
  "requires_clarification": true,
  "missing_fields": ["quantity", "discount_type"],
  "next_question": "Please provide quantities and requested discount type."
}
```

## POST /api/intake/session/{session_id}/reply

Adds a clarification reply.

```json
{
  "message": "They need 50 varsity helmets and the standard booster club discount."
}
```

## POST /api/workflows/quote-assist/start

Starts the governed quote workflow after required facts are collected.

```json
{
  "correlation_id": "corr_demo_001",
  "account_name": "Westlake High School",
  "requested_items": [
    {
      "product_family": "helmet",
      "quantity": 50,
      "configuration": {
        "color": "matte navy",
        "level": "varsity"
      }
    }
  ],
  "discount_request": {
    "type": "booster_club_standard"
  }
}
```

## GET /api/workflows/{workflow_id}

Returns final workflow state and outcome.

## GET /api/workflows/{workflow_id}/audit

Returns audit events for replay.

## GET /api/monitoring/summary

Returns workflow outcome counts, guardrail outcomes, and system health indicators.

## GET /api/cost/{correlation_id}

Returns cost telemetry for a workflow correlation.

## Draft Quote Response Example

```json
{
  "workflow_id": "wf_quote_demo_001",
  "correlation_id": "corr_demo_001",
  "workflow_type": "quote_assist",
  "workflow_status": "completed",
  "outcome": "draft_quote_created",
  "draft_quote_id": "dq_demo_001",
  "guardrail_decision": "allow",
  "requires_manager_approval": false,
  "rep_summary": "Draft quote prepared for 50 varsity helmets in matte navy with standard booster club discount. Confirm final configuration before customer signature."
}
```

## Audit Event Example

```json
{
  "event_id": "evt_demo_001",
  "workflow_id": "wf_quote_demo_001",
  "correlation_id": "corr_demo_001",
  "event_type": "product_spec_retrieved",
  "node_name": "retrieve_product_specs",
  "tool_name": "search_product_specs",
  "evidence_reference": "spec_helmet_varsity_v1",
  "output_summary": {
    "product_family": "helmet",
    "compatible_color": true
  }
}
```

## Cost Telemetry Event Example

```json
{
  "correlation_id": "corr_demo_001",
  "workflow_id": "wf_quote_demo_001",
  "workflow_type": "quote_assist",
  "llm_calls": 2,
  "rag_calls": 1,
  "retrieved_chunks": 4,
  "mcp_tool_calls": 5,
  "input_tokens": 1200,
  "output_tokens": 320,
  "total_tokens": 1520,
  "estimated_cost_usd": 0.013
}
```

## Monitoring Summary Example

```json
{
  "workflow_type": "quote_assist",
  "total_runs": 25,
  "draft_quote_created": 14,
  "clarification_required": 4,
  "blocked_by_policy": 3,
  "approval_required": 4,
  "average_estimated_cost_usd": 0.014
}
```
