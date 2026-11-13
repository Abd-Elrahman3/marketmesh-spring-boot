# Developer Track (D4–D7)

Rules are mandatory and cumulative. README section 5 is authoritative. Testing is part of each milestone; the AQA guide is complementary, not an alternative that skips implementation.

## D4 — API contracts and authorization

**Branch:** `feature/d4-api`

**Goal:** Orchestrate the saga; Handle late and duplicate results.

**You will practise:** Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

| Done | Rule | What to implement |
| --- | --- | --- |
| [ ] | BR-401 | Orchestrate the saga — Restart at every boundary; the order ends CONFIRMED or CANCELLED with no leaked stock/payment authorization. |
| [ ] | BR-402 | Handle late and duplicate results — Deliver success twice and after cancellation: one compensation effect, terminal order remains cancelled. |
**Required tests:** both rule examples, at least one boundary and one failure/rollback scenario from [Acceptance Tests](ACCEPTANCE_TESTS.md).

**Done when:** these tests and every earlier milestone pass; `docs/evidence/D4.md` contains reproducible evidence and an explanation of the invariant.

**Trap:** implementing only the HTTP happy path, or checking a rule in Java while leaving the database race unprotected.

## D5 — Advanced behavior and resource limits

**Branch:** `feature/d5-advanced`

**Goal:** Expose secure REST and order events; Version events and contracts.

**You will practise:** Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

| Done | Rule | What to implement |
| --- | --- | --- |
| [ ] | BR-501 | Expose secure REST and order events — Another buyer gets 404; same creation key+payload returns same order; changed payload gets 409. |
| [ ] | BR-502 | Version events and contracts — Deploy old consumer with new optional field; process successfully. A removed required field is blocked by compatibility tests. |
**Required tests:** both rule examples, at least one boundary and one failure/rollback scenario from [Acceptance Tests](ACCEPTANCE_TESTS.md).

**Done when:** these tests and every earlier milestone pass; `docs/evidence/D5.md` contains reproducible evidence and an explanation of the invariant.

**Trap:** implementing only the HTTP happy path, or checking a rule in Java while leaving the database race unprotected.

## D6 — Failure testing and recovery

**Branch:** `feature/d6-failures`

**Goal:** Reconcile discrepancies; Test systemic failure.

**You will practise:** Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

| Done | Rule | What to implement |
| --- | --- | --- |
| [ ] | BR-601 | Reconcile discrepancies — Seed 20 inconsistent scenarios; reconciliation resolves each through service contracts or marks manual action with reason. |
| [ ] | BR-602 | Test systemic failure — A 2-minute payment outage drains after recovery; all accepted orders are accounted for in a reconciliation report. |
**Required tests:** both rule examples, at least one boundary and one failure/rollback scenario from [Acceptance Tests](ACCEPTANCE_TESTS.md).

**Done when:** these tests and every earlier milestone pass; `docs/evidence/D6.md` contains reproducible evidence and an explanation of the invariant.

**Trap:** implementing only the HTTP happy path, or checking a rule in Java while leaving the database race unprotected.

## D7 — Operations and design defense

**Branch:** `feature/d7-operations`

**Goal:** Define SLOs and deploy safely; Defend the design.

**You will practise:** Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

| Done | Rule | What to implement |
| --- | --- | --- |
| [ ] | BR-701 | Define SLOs and deploy safely — Load at 50 orders/s for 10m, report p50/p95/p99 and settlement lag; show zero lost accepted orders during rollout. |
| [ ] | BR-702 | Defend the design — A reviewer can trace every accepted order to a terminal state or explicit recovery record without guessing. |
**Required tests:** both rule examples, at least one boundary and one failure/rollback scenario from [Acceptance Tests](ACCEPTANCE_TESTS.md).

**Done when:** these tests and every earlier milestone pass; `docs/evidence/D7.md` contains reproducible evidence and an explanation of the invariant.

**Trap:** implementing only the HTTP happy path, or checking a rule in Java while leaving the database race unprotected.
