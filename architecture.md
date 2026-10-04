# Architecture (planned)

```text
Client -> Payment REST API -> Idempotency check -> Routing policy
                                             -> Mock Provider A
                                             -> Mock Provider B
                                             -> Mock Provider C
                     -> Transaction state store -> Monitoring

Synthetic settlement CSV -> Reconciliation service -> Discrepancy report
```

Design principles: explicit state transitions, bounded retries, concurrency-safe idempotency, a common mock-provider interface, and deterministic reconciliation. Update this document to match the implementation.
