# Implementation Labs and Contract Details

These details are part of the requirements and refine the README rules.

## Required service APIs and seed data

Seed three SKUs with stock 10,0,100 and USD prices, plus two buyers. Each service has independent migrations/runtime credentials. Public create-order line prices come from a server-owned catalog snapshot, never from the buyer. Reject duplicate SKU lines or normalize them before canonical idempotency hashing; document the chosen rule.

Protobuf messages use string UUIDs, int32 quantity and google.protobuf.Timestamp expiry. ReserveRequest {request_id,order_id,sku_id,quantity}; ReserveResponse {reservation_id,status,expires_at}; other requests {request_id,reservation_id}; GetReservation may identify by order_id+sku_id after an uncertain Reserve. Reserve TTL is 5 minutes. Get is side-effect free; Confirm/Release replay returns current state. Map invalid values→INVALID_ARGUMENT, no stock/invalid transition→FAILED_PRECONDITION, missing→NOT_FOUND, overload→RESOURCE_EXHAUSTED and transient failure→UNAVAILABLE.

Payment simulator supports authorize,lookup-by-key,void and capture/refund if you implement capture. Keys remain stable by order and operation. The required saga uses authorization and void; do not charge a real payment method. Model unknown outcomes separately from declined payments. Provide a table for compensation before/after each durable step, including late success.

## Architecture defense

Choose choreography or orchestration explicitly; the baseline requirements use an orchestrator. Show which service can answer each query when another is down. Draw time-ordered traces for reserve success + payment timeout, cancellation + late success, and two simultaneous cancellations. Explain why a successful gRPC call does not commit the caller's database transaction.
