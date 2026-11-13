# Shared Milestones (M1–M3)

Rules are mandatory and cumulative. README section 5 is authoritative. Testing is part of each milestone; the AQA guide is complementary, not an alternative that skips implementation.

## M1 — Domain and invariants

**Branch:** `feature/m1-domain`

**Goal:** Specify money and orders; Draw service ownership.

**You will practise:** Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

| Done | Rule | What to implement |
| --- | --- | --- |
| [ ] | BR-101 | Specify money and orders — Two units at 19.95 plus one at 10.00 → 49.90; later catalog changes do not alter the order. |
| [ ] | BR-102 | Draw service ownership — Turning off payments does not prevent catalog reads; an architecture test rejects imports of another service’s persistence package. |
**Required tests:** both rule examples, at least one boundary and one failure/rollback scenario from [Acceptance Tests](ACCEPTANCE_TESTS.md).

**Done when:** these tests and every earlier milestone pass; `docs/evidence/M1.md` contains reproducible evidence and an explanation of the invariant.

**Trap:** implementing only the HTTP happy path, or checking a rule in Java while leaving the database race unprotected.

## M2 — Database and persistence

**Branch:** `feature/m2-database`

**Goal:** Conserve inventory; Separate local transactions.

**You will practise:** Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

| Done | Rule | What to implement |
| --- | --- | --- |
| [ ] | BR-201 | Conserve inventory — 100 requests for stock 10 confirm at most 10 units; duplicate release changes available stock once. |
| [ ] | BR-202 | Separate local transactions — A local rollback leaves neither business effects nor an outgoing event; cross-service lag is visible in order status. |
**Required tests:** both rule examples, at least one boundary and one failure/rollback scenario from [Acceptance Tests](ACCEPTANCE_TESTS.md).

**Done when:** these tests and every earlier milestone pass; `docs/evidence/M2.md` contains reproducible evidence and an explanation of the invariant.

**Trap:** implementing only the HTTP happy path, or checking a rule in Java while leaving the database race unprotected.

## M3 — Transactional use cases

**Branch:** `feature/m3-transactions`

**Goal:** Design gRPC inventory contracts; Make retry behavior explicit.

**You will practise:** Architecture from scratch: service boundaries, gRPC/Protobuf, REST, Kafka, sagas, money, distributed idempotency, contract evolution, resilience, OpenTelemetry.

| Done | Rule | What to implement |
| --- | --- | --- |
| [ ] | BR-301 | Design gRPC inventory contracts — Client cancellation stops unnecessary work; deadline timeout is treated as uncertain, then queried by stable reservation key. |
| [ ] | BR-302 | Make retry behavior explicit — Three nested retries cannot turn one order into 27 provider requests; demonstrate attempt counters during an outage. |
**Required tests:** both rule examples, at least one boundary and one failure/rollback scenario from [Acceptance Tests](ACCEPTANCE_TESTS.md).

**Done when:** these tests and every earlier milestone pass; `docs/evidence/M3.md` contains reproducible evidence and an explanation of the invariant.

**Trap:** implementing only the HTTP happy path, or checking a rule in Java while leaving the database race unprotected.
