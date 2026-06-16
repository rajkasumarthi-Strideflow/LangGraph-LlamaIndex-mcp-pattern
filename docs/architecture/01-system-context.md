# C4 Level 1 — System Context Diagram: DecisionTrace Field Sales Agent

This diagram shows the DecisionTrace Field Sales Agent as a software system in its external ecosystem. It identifies the primary users, reviewer role, demo enterprise data sources, product/spec knowledge, foundation model dependency, and monitoring/observability relationship. Internal implementation details such as the API layer, LangGraph workflow, MCP layer, LlamaIndex retrieval, audit store, and cost telemetry store are intentionally excluded from this Level 1 view.

```mermaid
flowchart LR
  Rep["Field Sales Rep<br/>[Person]<br/><br/>Creates draft quote requests and reviews AI-assisted quote outcomes"]
  Reviewer["Manager / Reviewer<br/>[Person]<br/><br/>Reviews approval-required outcomes and audit context"]

  System["DecisionTrace Field Sales Agent<br/>[Software System]<br/><br/>Helps field sales reps create governed draft quotes using account, product, inventory, pricing, policy, retrieval, and audit-aware AI workflow support"]

  CRM["Synthetic CRM / Account Data<br/>[External System]<br/><br/>Demo account, customer, and sales context"]
  Inventory["Synthetic Inventory Data<br/>[External System]<br/><br/>Demo product availability and stock constraints"]
  Pricing["Pricing Rules<br/>[External System]<br/><br/>Demo pricing and discount policy inputs"]
  ProductKnowledge["Product / Spec Knowledge<br/>[External System]<br/><br/>Demo product specifications, catalog evidence, and policy-like reference content"]
  LLM["Foundation Model Provider<br/>[External System]<br/><br/>Optional model provider used for AI-assisted intake or response drafting when enabled"]
  Monitoring["Monitoring / Observability<br/>[External System]<br/><br/>Receives audit, trace, workflow, and cost signals for review and operational visibility"]

  Rep -->|"Uses quote assist capabilities"| System
  Reviewer -->|"Reviews approval-required outcomes"| System

  System -->|"Reads account context"| CRM
  System -->|"Checks inventory constraints"| Inventory
  System -->|"Applies pricing and discount rules"| Pricing
  System -->|"Retrieves product/spec evidence"| ProductKnowledge
  System -->|"Sends governed prompts when AI features are enabled"| LLM
  System -->|"Publishes audit, trace, and cost signals"| Monitoring
```

- This is the C4 Level 1 view.
- The DecisionTrace Field Sales Agent is shown as one software system.
- Internal containers are intentionally hidden and are shown in the Level 2 diagrams.
