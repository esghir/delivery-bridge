# AIP and automation

## Three distinct AI responsibilities

| Component | Inputs | Output | Boundary |
| --- | --- | --- | --- |
| AIP Chatbot | Authorized request, owner, status and blocker context | Grounded answers and intake drafts | Does not silently submit or accept work |
| AIP Analyst | Requests, cycles, capacity and transition history | Inspectable bottleneck and work-mix analysis | Does not rank people from raw ticket counts |
| AIP Logic | Request description, acceptance criteria and delivery revision | Categorization suggestions and test scenario drafts | A generated scenario is not an executed or passed test |

The LLM is a configured platform-supported model. Validate the proposed output contract and track model/prompt versions before allowing generated records into the review queue.

## Proposed test-draft output

```json
{
  "request_id": "REQ-DEMO-001",
  "delivery_revision": 1,
  "scenarios": [{
    "scenario_id": "TEST-DEMO-001",
    "acceptance_criterion_ids": ["AC-DEMO-001"],
    "steps": ["Open the inventory view", "Filter by a known demo warehouse"],
    "expected_result": "Only inventory records for the selected warehouse appear.",
    "review_status": "draft"
  }]
}
```

The tester checks requirement coverage, edits the draft and records a review decision. TestExecution records are created only when someone actually executes a reviewed scenario. Failed results or gaps return the request to development. Business acceptance remains an authorized referent action.

## Automation rules

| Trigger | Conditions | Effect | Recovery |
| --- | --- | --- | --- |
| Assignment changes | Valid new owner | Notify assignee and relevant referent | Deduplicate by request and transition |
| Request ready for testing | Acceptance criteria exist; new delivery revision | Invoke Logic and create draft scenarios | Keep failure visible; allow controlled retry |
| Request overdue or blocked | Relevant due date/blocked duration and responsible owner | Send a scoped reminder | Rate-limit repeated notices |
| Planning-cycle boundary | Configured cycle and audience | Notify planning participants; generate Notepad digest | Log cycle ID and as-of timestamp |

Use `request_id + delivery_revision + automation_purpose` as a candidate idempotency key. Generate a fresh draft for a new delivery revision only when the workflow requires it. Do not create an endless loop from generated-object changes.

## Evaluation and access

Test scenario relevance, criterion coverage, executable steps, valid criterion IDs and refusal to infer unprovided facts. Also test behavior when a user cannot access a linked request or evidence item. Track failed invocations, review acceptance and latency; avoid auto-completion based on an AI recommendation.
