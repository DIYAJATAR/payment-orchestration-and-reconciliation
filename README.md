# Payment Orchestration & Reconciliation

**Status: Starter scaffold — implementation and tests are not yet complete.**

A Java/Spring Boot learning project simulating common payment infrastructure problems with mock providers and synthetic data only. It does not process real money or connect to real payment networks.

## Project 1: Payment Orchestration & Intelligent Routing
Planned features:
- Unified REST API for simulated payment requests
- Rule-based routing among mock providers
- Idempotency keys to prevent duplicate payment creation
- Bounded retries and failover for transient provider failures
- Explicit transaction-state tracking and error handling

## Project 2: Payment Reconciliation & Transaction Monitoring
Planned features:
- Import synthetic provider settlement CSV files
- Compare settlement rows with internal transaction records
- Flag missing, duplicate, and amount-mismatched records
- Generate reconciliation reports
- Add automated tests for failure and edge cases

## Planned stack
Java 21, Spring Boot, PostgreSQL, Redis (optional), JUnit 5, Docker.

## Proposed API
| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/v1/payments` | Create simulated payment; use an `Idempotency-Key` header |
| GET | `/api/v1/payments/{paymentId}` | Read payment status |
| GET | `/api/v1/providers` | Inspect mock provider configuration |
| POST | `/api/v1/reconciliation/import` | Import synthetic settlement CSV |
| GET | `/api/v1/reconciliation/reports/{reportId}` | Read reconciliation results |

These endpoints are proposed and are not implemented yet.

## Test plan
- Concurrent requests using the same idempotency key create at most one payment.
- Transient provider failures follow bounded retry/failover rules.
- Permanent declines are not retried.
- Duplicate, missing, and mismatched settlement rows are flagged.
- Invalid state transitions and malformed CSV files are handled safely.

## Suggested structure
```text
backend/
  pom.xml
  src/main/java/com/diya/payments/
  src/test/java/com/diya/payments/
docs/
  architecture.md
  test-plan.md
docker-compose.yml
```

## Safety
Use mock providers and synthetic data only. Never commit credentials, real card data, or production payment secrets. Do not describe planned features as completed until implemented and tested.

## Roadmap
- [ ] Create Spring Boot app
- [ ] Implement payment/provider domain models
- [ ] Add PostgreSQL persistence
- [ ] Implement idempotency and transaction state transitions
- [ ] Implement mock routing, retry, and failover
- [ ] Implement settlement CSV reconciliation
- [ ] Add automated tests and CI
