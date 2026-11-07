# Synthetic example: request delivery and test coverage

[scenario.json](scenario.json) contains a fictional inventory-dashboard request in a proposed three-week cycle.

1. The request has **24 hours** of remaining work; other selected work contributes **32 hours**.
2. Available cycle capacity is **80 hours**, after other commitments.
3. Workload is `24 + 32 = 56 hours`; utilization is `56 / 80 × 100 = 70%`.
4. The one required acceptance criterion has a reviewed scenario, so criterion coverage is **100%**.
5. No test has been executed. Test pass rate is **N/A**, and the request **cannot be completed**.
6. A tester executes the scenario and records evidence. Only after all required tests pass and the referent accepts the delivery may an authorized action mark it Done.

This deliberately illustrates why scenario coverage does not prove successful testing. The JSON is a logical example, not a deployable application or automatic ontology import bundle.
