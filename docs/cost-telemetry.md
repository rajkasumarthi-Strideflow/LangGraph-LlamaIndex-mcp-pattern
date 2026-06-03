# Field Sales Agent Cost Telemetry

Phase 1 includes cost telemetry, not full cost-optimized orchestration. The goal is to make operating cost visible from day one so teams can understand the cost of workflow execution before adding dynamic routing, caching, or optimization.

## Telemetry Fields

Track:

- `workflow_id`
- `correlation_id`
- `workflow_type`
- LLM calls
- RAG calls
- Retrieved chunks
- MCP tool calls
- Input tokens
- Output tokens
- Total tokens
- Estimated cost if configured rates are available
- Cost per draft quote attempt
- Cost by outcome

## Cost per Draft Quote Attempt

```text
cost_per_attempt = llm_cost + rag_cost + mcp_tool_cost + storage_cost + monitoring_cost
```

If pricing rates are not configured, the system should report usage metrics without estimating dollars.

## Cost by Outcome

Cost should be compared across outcomes:

- Clarification required
- Invalid product or identifier
- Blocked by policy
- Approval required
- Draft quote created

This helps distinguish cheap failed attempts from more expensive successful workflows and identifies where clarification, retrieval, or guardrail behavior may need improvement.

## Phase 1 Boundary

Do not claim these are implemented in Phase 1:

- Dynamic model routing
- Semantic caching
- Prompt caching
- Cost-aware orchestration
- Automated model downgrade/upgrade decisions

## Future Cost-Optimized Orchestration

Future enhancements may include:

- Dynamic model routing by risk and complexity
- Prompt caching for stable system instructions
- Semantic caching for repeated low-risk product explanations
- Retrieved chunk limits
- Tool-call caps
- Retry caps
- Escalation instead of repeated expensive loops
