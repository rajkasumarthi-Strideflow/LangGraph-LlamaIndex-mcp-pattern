# LinkedIn Project Summary

I built Field Sales Agent as an enterprise AI architecture reference app.

Most AI demos stop at a chatbot response. This project focuses on the control architecture around the response: intake validation, workflow orchestration, bounded tool access, evidence retrieval, guardrails, response validation, auditability, cost telemetry, monitoring, and evaluation.

The first workflow, DecisionTrace — Quote Assist Agent, turns a natural-language field sales request into a governed draft quote workflow.

Architecture highlights:

- OpenAI-assisted intake extraction and response drafting
- LangGraph workflow control
- MCP-mediated enterprise tool/resource boundary
- LlamaIndex-backed product/spec evidence retrieval
- canonical payload and enterprise adapter pattern
- deterministic quote guardrails
- audit trace, cost telemetry, monitoring, and golden-scenario evaluation

The important design principle:
OpenAI assists with language. LangGraph controls workflow. MCP exposes bounded capabilities. LlamaIndex retrieves evidence. Guardrails make business decisions.

Natural language in; governed workflow out.
