# Database Requirements

## 1. Ownership and schema

Three owned PostgreSQL stores: orders(order_id,buyer,status,currency,total,version), order_lines(order_id,sku_id,quantity,unit_price), saga_steps(saga_id,step,state,attempt,deadline); inventory(sku_id,on_hand,reserved,version), reservations(id,order_id,sku_id,quantity,status,expires_at, UNIQUE(order_id,sku_id)); payments(id,order_id UNIQUE,amount,currency,provider_key UNIQUE,status). Every store adds inbox/outbox and audit tables. CHECK reserved>=0 AND reserved<=on_hand. Never use floating point for money. Each store needs independent backup and migrations. Define reconciliation indexes and 30-day idempotency retention. Kafka retains events 14 days, so replay and inbox retention must be coordinated. Only opaque provider tokens, no card numbers.

## 2. Required artifacts

- ERD with cardinality, PK, FK, nullability and ownership.
- Versioned forward migrations for every constraint/index; no automatic schema update in final configuration.
- Seed fixtures for normal, duplicate, missing-reference and boundary cases.
- Explicit transaction isolation, lock order, timeout and retry policy.
- EXPLAIN (ANALYZE, BUFFERS) for the busiest query before and after an index; include row counts and hardware.
- Upgrade test from a prior schema fixture, not only create-from-empty.
- Backup/restore commands for a disposable destination and SQL integrity checks.

## 3. Testing rules

Run actual PostgreSQL semantics. Use separate connections/processes for concurrent transactions and deterministic barriers; bound all waits. A service-level existence check is not a uniqueness guarantee. If the app relies on a constraint, test direct SQL violating it. Explain any SELECT FOR UPDATE, SKIP LOCKED, RLS, serializable retry or projection checkpoint used here.

## 4. Migration discipline

An applied migration is immutable. Use expand/backfill/contract for incompatible changes, and state how old/new application versions coexist. Separate migration privileges from runtime privileges. Document retention and restore behavior for derived data, deduplication records and secrets. Do not ship real user data in fixtures.

See [Implementation Labs and Contract Details](IMPLEMENTATION_LABS.md) for concrete fixtures, payload semantics and boundary experiments. These are required, not optional extras.
