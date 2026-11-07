# Delivery Bridge

Delivery Bridge is a proposed Palantir Foundry solution for tracking requests from intake through development, testing and business acceptance, with capacity planning, delivery analytics and human-reviewed AI test drafting.

**Architecture portfolio · Palantir Foundry · Ontology · AIP · Human-reviewed decisions**

## Why this project exists

Business referents and developers often track the same request differently. Priorities, ownership, implementation progress and test evidence become disconnected. Delivery Bridge brings the request lifecycle into one ontology-backed workspace, with explicit handoffs and a traceable definition of done.

**Intended outcome:** Follow a request from intake and prioritization through implementation, testing and business acceptance, while comparing planned effort with available capacity.

## Solution design

**Original Solution Designer export:**

[![Open the full-size Delivery Bridge Solution Designer diagram](docs/diagrams/solution-design.png)](docs/diagrams/solution-design.png)

This detailed diagram is the proposed Foundry solution design. It groups the design into five areas: data and build orchestration; ontology and controlled changes; applications and reporting; AIP and human review; workflow and operations. The linked PNG is 2048 × 1299 pixels. Its resolution is suitable for a portfolio, but the diagram is dense: small labels are hard to read in the README preview. Click the image to open it at full size and zoom in. The companion [workflow.svg](docs/diagrams/workflow.svg) presents the request lifecycle in a simpler, more readable view.

```mermaid
flowchart TD
    U["Referents · developers · testers · managers"] --> I["Request intake and reference data"]
    I --> P["Pipeline Builder · validation · curated datasets"]
    P --> O["Ontology: Request · Team · Cycle · Test Evidence"]
    O --> W["Workshop · Slate · Gantt · Quiver · Notepad"]
    O --> A["AIP Chatbot · Analyst · Logic · approved LLM"]
    A --> H["Human review and acceptance"]
    W --> X["Action Types · controlled state changes"]
    H --> X
    X --> M["Automate · notifications · audit history"]
    M --> O
```

The editable [Solution Designer JSON](docs/diagrams/solution-design.json) accompanies the diagram and can be imported into a compatible Solution Designer. Importing the JSON draws the design; it does not provision Foundry resources. See [the component and data flow details](docs/architecture.md).

## What the design covers

- Structured request intake and ownership
- Proposed three-week planning and Gantt timeline
- Effort-based workload and capacity analysis
- Controlled transitions with timestamped event history
- AI-assisted test drafting and human validation
- Cycle reviews, blocker analysis and delivery handover

## Who uses it

Business referents define needs and accept delivery; developers implement requests; testers record verification evidence; managers prioritize work and balance capacity.

## End-to-end workflow

![Delivery Bridge workflow diagram](docs/diagrams/workflow.svg)

```mermaid
flowchart TD
    I["Referent submits request"] --> B["Triage and backlog"]
    B --> P["Prioritize against cycle capacity"]
    P --> D["Assigned development and Gantt"]
    D --> AI["AIP drafts test scenarios"]
    AI --> T["Tester reviews and executes"]
    T --> G{"Tests pass and criteria covered?"}
    G -->|No| D
    G -->|Yes| A["Referent accepts delivery"]
    A --> F["Done and handover"]
    D --> Q["Quiver workload and delivery metrics"]
    F --> Q
```

## Start here

1. Read the [architecture and tool responsibilities](docs/architecture.md).
2. Inspect the [ontology and data contracts](docs/ontology.md).
3. Follow the [workflow and business rules](docs/workflows.md).
4. Review the [AIP and automation design](docs/aip-and-automation.md).
5. Walk through the [synthetic example](examples/README.md).
6. Use the [implementation and validation guide](docs/implementation.md) to plan a Foundry build.

## Example scenario

A fictional team receives a request for an inventory dashboard. A manager assigns it to a three-week cycle, a developer implements it, AIP proposes test scenarios, and a tester verifies them. Completion requires passing required tests and business acceptance.

## Repository contents

| Path | Contents |
| --- | --- |
| `docs/diagrams/solution-design.png` | Full-resolution architecture diagram |
| `docs/diagrams/solution-design.json` | Editable Solution Designer diagram |
| `docs/diagrams/solution-design.png` | Original detailed Solution Designer diagram |
| `docs/diagrams/workflow.svg` | Readable companion workflow graphic from intake through acceptance |
| `docs/architecture.md` | Layers, component roles and engineering decisions |
| `docs/ontology.md` | Object grains, links, keys and data ownership |
| `docs/workflows.md` | States, actions, calculations and completion rules |
| `docs/aip-and-automation.md` | AI inputs/outputs, review gates and automation triggers |
| `docs/implementation.md` | Suggested build sequence, validation and operations |
| `examples/` | Fictional records and an illustrative walkthrough |
| `docs/references.md` | Official Palantir capability references |

## Status and scope

This is a **conceptual solution-design repository**, not a deployable Foundry application. It contains documentation, diagrams and synthetic records; it does not contain production code, provisioned ontology objects, live connections or configured AI agents. Detailed schemas, formulas and workflow rules are proposed implementation choices.

Importing the JSON draws the solution architecture; it does not create Foundry resources. Some tools appear as generic custom cards for compatibility with the supplied export format. The JSON has been structurally validated; import behavior depends on your Solution Designer version.

## Technology coverage

Ontology Manager, Workshop, Slate, Action Types, PySpark, TypeScript, Code Repositories, Pipeline Builder, Scheduler, Automate, Quiver, Notepad, Gantt Chart, AIP Chatbot, AIP Analyst, AIP Logic and LLMs.

## Foundry tools and their roles

These are proposed components in the conceptual design; they are not claims that a production Foundry environment has already been configured.

| Tool | Role in Delivery Bridge |
| --- | --- |
| Ontology Manager | Model requests, teams, delivery cycles, capacity, acceptance criteria and test evidence as linked objects. |
| Pipeline Builder | Ingest, standardize and validate request, team and capacity inputs. |
| Code Repository (PySpark / TypeScript) | Version transformations, validation functions and controlled business logic. |
| Scheduler | Refresh curated data and dependent metrics on a defined cadence. |
| Action Types | Create and assign requests, prioritize work, plan cycles, record test results and accept delivery. |
| Workshop | Provide the primary manager, developer and reviewer workspace. |
| Slate | Offer a focused request portal where a custom interface is useful. |
| Gantt chart | Display planned development dates, dependencies and three-week cycle capacity. |
| Quiver | Analyze throughput, cycle time, blocked work, rework and capacity utilization. |
| Notepad | Capture cycle decisions, blockers, test evidence and handover notes. |
| AIP Chatbot | Answer grounded questions about authorized request and delivery records. |
| AIP Analyst | Investigate bottlenecks and workload patterns using accessible data. |
| AIP Logic | Draft acceptance criteria and test scenarios for human review. |
| LLM | Provide the approved model runtime behind AIP features; outputs require grounding and evaluation. |
| Automate | Send deduplicated notifications and escalations after approved workflow events. |

## Contributing

Suggest changes with a clear problem statement and the affected documentation or diagram. Keep examples fictional, state assumptions explicitly, and update the ontology and workflow references when a design changes. Do not submit credentials, internal URLs or organization-specific data.
