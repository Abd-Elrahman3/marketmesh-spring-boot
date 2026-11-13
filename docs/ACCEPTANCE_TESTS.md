# Acceptance Tests

Every row is mandatory. M1 includes provided examples in starters; later test skeletons must become real behavior tests. Test names below are descriptions, not a hidden API.

| Milestone | Rule | Scenario and expected result |
| --- | --- | --- |
| M1 | BR-101 | Two units at 19.95 plus one at 10.00 → 49.90; later catalog changes do not alter the order. |
| M1 | BR-102 | Turning off payments does not prevent catalog reads; an architecture test rejects imports of another service’s persistence package. |
| M2 | BR-201 | 100 requests for stock 10 confirm at most 10 units; duplicate release changes available stock once. |
| M2 | BR-202 | A local rollback leaves neither business effects nor an outgoing event; cross-service lag is visible in order status. |
| M3 | BR-301 | Client cancellation stops unnecessary work; deadline timeout is treated as uncertain, then queried by stable reservation key. |
| M3 | BR-302 | Three nested retries cannot turn one order into 27 provider requests; demonstrate attempt counters during an outage. |
| D4 | BR-401 | Restart at every boundary; the order ends CONFIRMED or CANCELLED with no leaked stock/payment authorization. |
| D4 | BR-402 | Deliver success twice and after cancellation: one compensation effect, terminal order remains cancelled. |
| D5 | BR-501 | Another buyer gets 404; same creation key+payload returns same order; changed payload gets 409. |
| D5 | BR-502 | Deploy old consumer with new optional field; process successfully. A removed required field is blocked by compatibility tests. |
| D6 | BR-601 | Seed 20 inconsistent scenarios; reconciliation resolves each through service contracts or marks manual action with reason. |
| D6 | BR-602 | A 2-minute payment outage drains after recovery; all accepted orders are accounted for in a reconciliation report. |
| D7 | BR-701 | Load at 50 orders/s for 10m, report p50/p95/p99 and settlement lag; show zero lost accepted orders during rollout. |
| D7 | BR-702 | A reviewer can trace every accepted order to a terminal state or explicit recovery record without guessing. |

## Failure drills

1. Kill orchestrator after payment authorization before inventory confirmation.
2. Return payment success after compensation begins.
3. Roll out a new protobuf/event schema while old consumers are active.

## Evidence standard

Record setup, exact command, controlled failure point, durable before/after state, expected result and actual result. A test that only asserts an exception or mocks all persistence cannot prove a database invariant. Use bounded timeouts and deterministic coordination; avoid sleeps as a race strategy. Record a seed for randomized tests. Do not turn an unavailable Docker dependency into a silently skipped passing test.

For D6, deliberately introduce one representative bug and verify a test detects it. For D7, record machine configuration, dataset, concurrency, p50/p95/p99, throughput, errors and resource usage. Restore tests use a different database from the source.
