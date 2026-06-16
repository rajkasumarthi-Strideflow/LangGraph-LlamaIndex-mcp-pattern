# C4 Level 2 — Container Diagram: Quote Assist Runtime Interaction View

This container-level view shows the primary runtime request path for the quote-assist workflow. It explains how a field sales rep uses the UI, how the UI enters the controlled DecisionTrace API layer, how the API starts the LangGraph workflow, and how the workflow reaches governed tools, resources, retrieval, audit, and telemetry capabilities.

```mermaid
flowchart LR
  Rep["Field Sales Rep<br/>[Person]"] -->|"Submits quote request"| UI["Field Sales Agent UI<br/>[Container]<br/><br/>Browser-based demo interface for quote intake, readiness, outcomes, audit review, and approval visibility"]

  Reviewer["Manager / Reviewer<br/>[Person]"] -->|"Reviews approval-required outcomes"| UI

  UI -->|"Calls workflow APIs"| API["DecisionTrace API Layer<br/>[Container]<br/><br/>Controlled backend entry point for validation, request shaping, correlation IDs, workflow start/status, audit access, and error handling"]

  API -->|"Starts quote-assist workflow"| Workflow["Quote Assist LangGraph Workflow<br/>[Container]<br/><br/>Orchestrates intake, product lookup, inventory checks, pricing, guardrails, retrieval, and final workflow outcome"]

  Workflow -->|"Calls governed tools and resources"| MCP["MCP Tool / Resource Layer<br/>[Container]<br/><br/>Provides tool/resource abstraction for account, inventory, pricing, policy, and retrieval access"]

  MCP -->|"Reads account context"| CRM["Synthetic CRM Data<br/>[External Data Source]"]
  MCP -->|"Checks availability"| Inventory["Synthetic Inventory Data<br/>[External Data Source]"]
  MCP -->|"Applies rules"| Pricing["Pricing Rules<br/>[External Data Source]"]
  MCP -->|"Retrieves evidence"| RAG["LlamaIndex Product / Spec Retrieval<br/>[Container]"]

  Workflow -->|"Writes workflow trace and decisions"| Audit["Audit Trace / Monitoring<br/>[Container or Store]"]
  Workflow -->|"Writes cost events"| Cost["Cost Telemetry<br/>[Container or Store]"]
```

- This is a Level 2 container-level runtime interaction view.
- It emphasizes the path of a quote request through the UI, API layer, workflow, MCP access layer, data sources, retrieval, audit, and cost telemetry.
- The DecisionTrace API Layer is not just a router; it is the controlled backend entry point that validates requests, shapes canonical payloads, establishes correlation IDs, starts workflows, exposes status/audit APIs, and protects internal orchestration from direct UI coupling.
