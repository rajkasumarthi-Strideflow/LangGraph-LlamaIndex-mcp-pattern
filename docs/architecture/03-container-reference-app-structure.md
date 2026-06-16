# C4 Level 2 — Container Diagram: Field Sales Agent Reference App Structure

This container-level view shows how the reference app is organized into major runtime areas: the Field Sales Agent reference app, the MCP-style access layer, and the product evidence retrieval area. Some boxes represent key internal capabilities within containers rather than independently deployable services; this is intentional for a public reference architecture diagram.

```mermaid
flowchart TB
  subgraph App["Field Sales Agent Reference App"]
    UI["Browser Demo UI<br/>[Container]<br/><br/>User-facing demo experience for intake, quote outcomes, audit timeline, and review visibility"]
    API["FastAPI-style API Contracts<br/>[Container]<br/><br/>Backend API boundary for workflow start, workflow status, audit, cost, and intake analysis"]
    Router["Intake Router<br/>[Internal Capability]<br/><br/>Routes and normalizes quote-assist intake requests"]
    Graph["LangGraph Quote Workflow<br/>[Container]<br/><br/>Coordinates account lookup, product matching, inventory, pricing, guardrails, retrieval, and final outcomes"]
    Guardrails["Quote Guardrails<br/>[Internal Capability]<br/><br/>Enforces draft-quote-only behavior, supported product/configuration rules, approval paths, and blocked outcomes"]
    Audit["Audit Event Store<br/>[Store]<br/><br/>Persists workflow events, decisions, tool calls, evidence references, and correlation IDs"]
    Cost["Cost Telemetry Store<br/>[Store]<br/><br/>Persists AI/model usage and cost telemetry events"]
    Monitor["Monitoring Summary<br/>[Internal Capability]<br/><br/>Summarizes workflow status, audit events, and telemetry for review"]
  end

  subgraph MCPZone["MCP-style Access Layer"]
    Client["MCP Client Interface<br/>[Internal Capability]<br/><br/>Workflow-facing interface for governed tool and resource calls"]
    Server["MCP Server<br/>[Container]<br/><br/>Exposes demo tools and resources through an MCP-style boundary"]
    Resources["Tools and Resources<br/>[Internal Capability]<br/><br/>Account, product, inventory, pricing, quote, and product/spec retrieval tools/resources"]
  end

  subgraph Retrieval["Product Evidence"]
    Index["LlamaIndex Retrieval Service<br/>[Container]<br/><br/>Retrieves relevant product/spec evidence for grounding"]
    Specs["Synthetic Product Specs<br/>[Data Source]<br/><br/>Demo catalog, product, and specification content"]
  end

  UI -->|"Calls backend APIs"| API
  API -->|"Routes intake"| Router
  Router -->|"Starts workflow"| Graph
  Graph -->|"Applies business and safety controls"| Guardrails
  Graph -->|"Requests tools/resources"| Client
  Client -->|"Calls MCP server"| Server
  Server -->|"Exposes tools/resources"| Resources
  Resources -->|"Retrieves evidence"| Index
  Index -->|"Indexes and queries"| Specs
  Graph -->|"Writes audit events"| Audit
  Graph -->|"Writes cost events"| Cost
  Audit -->|"Feeds operational summary"| Monitor
  Cost -->|"Feeds operational summary"| Monitor
```

- This is a Level 2 container-level structure view.
- It groups the reference implementation into major runtime zones.
- Some boxes are labeled as internal capabilities to avoid implying that every box is a separately deployable container.
