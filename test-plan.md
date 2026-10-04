# Test Plan

## Orchestration
- Same idempotency key and same payload returns the original result.
- Same idempotency key with a different payload is rejected.
- Concurrent duplicate requests do not create duplicate records.
- Transient failures follow bounded retry/failover policy.
- Permanent declines are not retried.
- Invalid input and invalid state transitions are rejected.

## Reconciliation
- Exact matches are marked matched.
- Missing settlement rows are flagged.
- Duplicate rows are flagged.
- Amount mismatches and unknown provider transactions are flagged.
- Empty or malformed CSV files return useful validation errors.

Publish test results only after running the tests.
