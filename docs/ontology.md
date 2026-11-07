# Delivery Bridge: ontology and data contracts

All names and schemas here are proposed. They define a logical model to adapt in Ontology Manager rather than an export of provisioned object types.

## Object types and relationships

| Object | Grain / identifier | Main relationships and fields |
| --- | --- | --- |
| UseCaseRequest | One request | Project, referent, developer, priority, status, effort, dates and acceptance owner |
| Person / Team | One member / team | Role and team membership; visibility scope |
| PlanningCycle | One planning period | Start/end dates and selected requests |
| CapacityAllocation | Member × cycle | Available hours after leave and other commitments |
| AcceptanceCriterion | One criterion per request | Expected observable outcome and required verification |
| TestScenario | One scenario version | Steps, expected result, criterion links, reviewer and AI draft provenance |
| TestExecution | One execution of a scenario | Actual result, evidence, tester and execution timestamp |
| StatusEvent | One request transition | From/to state, actor, timestamp and reason |

## Contract conventions

| Concern | Design rule |
| --- | --- |
| Primary keys | Stable string IDs; enforce uniqueness before ontology synchronization |
| Relationships | Store explicit foreign keys and verify referenced records exist |
| Timestamps | Use timezone-aware UTC timestamps for events; document date-only planning conventions |
| Provenance | Retain source system/reference, source timestamp and ingestion timestamp where appropriate |
| Null values | Distinguish unknown or not-yet-entered values from zero or false |
| Units | Record units for measurements and use hours consistently for effort/capacity |
| Versions | Retain revisions for approvals, scenario definitions, prompts and business rules |
| Access | Scope both source data and object/property access; action criteria govern mutations |

## Property ownership

Source-derived descriptions, measurements and reference attributes are managed by the data pipeline unless the design explicitly allows an override. Workflow status, assignment, review decisions and approval metadata are managed through actions. Document the conflict-resolution strategy for any property that can receive both a pipeline value and a user edit.

## Data quality gates

Reject duplicate primary keys, invalid foreign keys and malformed required dates. Quarantine records that cannot be interpreted safely. Surface missing mandatory evidence or test context to the user instead of inventing values. Record freshness and validation outcomes so a successful pipeline run cannot be mistaken for trustworthy business data.

The [synthetic example](../examples/README.md) illustrates the model without using operational data.
