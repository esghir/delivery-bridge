# Delivery Bridge: workflows and business rules

## Lifecycle, actions and measurement

Proposed states: Intake → Triage → Backlog → Planned → Development → Testing → Acceptance → Done. Testing failures return to Development. Blocked work should carry a reason and blocking interval; cancellation and reopening require explicit authorized transitions.

| Action | Control / resulting behavior |
| --- | --- |
| CreateRequest | Capture referent, scope and expected outcome |
| AssignDeveloper / Prioritize | Validate owner and manager/referent authority |
| PlanCycle | Set dates and cycle; surface capacity and dependency conflicts |
| UpdateProgress | Enforce transition rules and append a StatusEvent |
| SubmitForTest | Require acceptance criteria and a testable delivery |
| RecordTestResult | Store actual result and evidence against a specific scenario version |
| AcceptDelivery | Require required tests to pass, coverage checks and referent approval |

### Workload and quality definitions

| Indicator | Proposed definition |
| --- | --- |
| Workload | Remaining estimated hours on selected active requests for the cycle |
| Available capacity | Sum of CapacityAllocation hours for that cycle |
| Utilization | Workload ÷ available capacity × 100; N/A when capacity is zero |
| Indicative required FTE | Workload ÷ agreed productive hours per FTE in the cycle; an estimate, not an automatic staffing decision |
| Cycle time | Time from entry to Development to accepted completion; state how reopened items are handled |
| Blocked duration | Sum of recorded blocked intervals within the selected reporting window |
| Requirement coverage | Criteria with reviewed linked scenarios ÷ required criteria; show separately from execution results |
| Test pass rate | Passed required scenarios ÷ executed required scenarios under a documented latest-execution policy |

A request cannot be completed merely because the tests that happened to run passed. All required scenarios must be executed successfully and required acceptance criteria must have coverage. Team performance analysis should account for effort, complexity and work mix rather than treating raw ticket counts as individual productivity.
