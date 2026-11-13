# Advanced Backend Gates

CRUD alone does not complete this project. Every README rule is required, including the following demonstrations.

| Gate | Required demonstration |
| --- | --- |
| D5 | Another buyer gets 404; same creation key+payload returns same order; changed payload gets 409. |
| D5 | Deploy old consumer with new optional field; process successfully. A removed required field is blocked by compatibility tests. |
| D6 | Seed 20 inconsistent scenarios; reconciliation resolves each through service contracts or marks manual action with reason. |
| D6 | A 2-minute payment outage drains after recovery; all accepted orders are accounted for in a reconciliation report. |
| D7 | Load at 50 orders/s for 10m, report p50/p95/p99 and settlement lag; show zero lost accepted orders during rollout. |
| D7 | A reviewer can trace every accepted order to a terminal state or explicit recovery record without guessing. |

## Explain before advancing

1. Which invariant belongs in the domain, database, transport and worker respectively?
2. Where is the transaction boundary, and what happens if the process dies immediately after commit?
3. Which operations can safely retry, and how are duplicates or uncertain results resolved?
4. What is bounded: threads, connections, queues, buffers, retries and query sizes?
5. How is authorization enforced below the controller and across caches/messages?
6. Which metric tells you this system is failing before users report it?
7. How do you restore data and prove correctness after recovery?

Project-specific concepts to defend: Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

Record commands and results in evidence files. An owner can alter CI; the gates are an honest learning contract, not tamper-proof certification. Mark incomplete behavior openly.
