# API Test Specification

The authoritative contract is [API Requirements](../API_REQUIREMENTS.md). Build a test matrix for all 6 operations.

For each: test successful response/status/headers, malformed payload, boundary values, missing resource, duplicate request, authorization denial and relevant unavailable dependency. Check database side effects after rejection. Use exact request bytes for signatures, real JWT validation tests for issuer/audience, and protocol-specific assertions for GraphQL/gRPC/streaming.

| Rule | Required sample |
| --- | --- |
| BR-401 | Restart at every boundary; the order ends CONFIRMED or CANCELLED with no leaked stock/payment authorization. |
| BR-402 | Deliver success twice and after cancellation: one compensation effect, terminal order remains cancelled. |
| BR-501 | Another buyer gets 404; same creation key+payload returns same order; changed payload gets 409. |
| BR-502 | Deploy old consumer with new optional field; process successfully. A removed required field is blocked by compatibility tests. |

Do not call real carrier/payment/customer services. Build deterministic local provider fixtures and record request counts and idempotency keys.
