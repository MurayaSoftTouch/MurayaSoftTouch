# Haman Muraya

**Senior Software Engineer in Test · Quality Engineering for backend & distributed systems**

I build test architecture for systems where correctness matters: ledgers and payment flows, policy services, event pipelines, and ML services. That covers API and integration suites, contract tests, fault injection, regression coverage, and CI quality gates. Nine years across fintech, banking, insurance, and e-commerce designing those systems means I test them from the data model and failure modes outward.

[![Portfolio](https://img.shields.io/badge/Portfolio-hamman--portfolio.vercel.app-1B1A17?style=flat-square)](https://hamman-portfolio.vercel.app/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-haman--mur-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/haman-mur)
[![Email](https://img.shields.io/badge/Email-hamanmuraya009%40gmail.com-555555?style=flat-square&logo=gmail&logoColor=white)](mailto:hamanmuraya009@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-MurayaSoftTouch-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/MurayaSoftTouch)

---

## Testing & quality engineering

- **API & integration testing:** pytest, xUnit, and JUnit 5 suites against real PostgreSQL through Testcontainers, plus REST API regression tests in open source.
- **Contract testing:** a versioned OpenAPI 3.1 contract with consumer- and provider-side contract tests between independently deployed services.
- **Fault injection & reliability testing:** Toxiproxy and a controllable TCP proxy simulate database and dependency outages to verify fail-closed behaviour and recovery.
- **Regression prevention:** tests that pin the exact permission or failure branch a change touches, checked red against the old behaviour and green against the new.
- **End-to-end testing:** Playwright suites running a real browser against a real backend and a disposable database.
- **CI quality gates:** GitHub Actions running formatting, linting, unit, integration, contract, database-isolation, and end-to-end jobs on every pull request.

## Backend & systems engineering

- **Distributed systems:** service boundaries, concurrency control, idempotent and retry-safe operations, and transactional consistency across services that can fail independently.
- **Backend & APIs:** secure REST and GraphQL APIs, OAuth2/JWT and service-to-service authentication, relational data modelling, caching, and performance under load.
- **Cloud & platform:** containers and Kubernetes, infrastructure as code, CI/CD pipelines, and the monitoring and logging that make production systems operable.

---

## Open source contributions

### [CVAT](https://github.com/cvat-ai/cvat): [#11307 Add regression tests for org worker export permissions](https://github.com/cvat-ai/cvat/pull/11307) · *Open, in review*

`Python · pytest · REST API · OPA/Rego permissions · GitHub Actions`

- Adds REST API regression coverage for a permission change ([#10685](https://github.com/cvat-ai/cvat/pull/10685)) that stopped organization workers who are assignees, but not owners, from exporting job datasets, task datasets, and project backups.
- Corrects an existing project-backup test whose fixture selection never reached the changed policy branch. It now selects a worker who is project staff but not the owner.
- Validated with the targeted and neighbouring REST API suites: red against the pre-#10685 Rego policies, green against the current ones, and green in upstream CI.

---

## Selected engineering projects

### [LedgerCore](https://github.com/MurayaSoftTouch/LedgerCore)

A double-entry financial ledger and an independent transaction-policy service, built so money movements stay correct under retries, concurrency, and partial failure.

`C# · ASP.NET Core · Java 21 · Spring Boot · PostgreSQL · Testcontainers · Toxiproxy · Docker · GitHub Actions`

- **400+ automated tests** (xUnit and JUnit 5) across domain, API, policy-service, contract, and cross-service integration suites, including Testcontainers and Toxiproxy fault-injection suites.
- A versioned OpenAPI 3.1 contract with consumer and provider contract tests, and fail-closed approval when the policy service is unavailable.
- Balanced-journal invariants are enforced twice, in the domain model and by PostgreSQL triggers. Posted history is immutable at the database level, and CI verifies the least-privilege runtime roles.
- Idempotency keys with request fingerprinting and row-level locking in both services. Journal postings write outbox events in the same transaction.
- Authenticated service-to-service calls with bounded retries and correlation IDs. 16 ADRs.

*Built with two collaborators. My contributions include the policy service's domain model, PostgreSQL persistence, evaluation API, and its contract and concurrency tests.*

### [IncidentIQ](https://github.com/MurayaSoftTouch/IncidentIQ)

An incident-triage service that classifies incoming reports, says how uncertain it is, and routes low-confidence cases to a human reviewer.

`Python · pytest · FastAPI · SQLAlchemy · scikit-learn · Next.js · Playwright · Docker · GitHub Actions`

- **67 automated tests:** 57 pytest tests across the ML pipeline and API, plus 10 Playwright end-to-end tests against a real backend, real model, and disposable database. All of them run on every pull request.
- Model selection on validation macro-F1 against a dummy baseline, with a time-ordered split that keeps near-duplicates together to prevent leakage. The test set is scored once.
- Versioned model artifacts are verified by SHA-256 hash, and the API refuses to serve a model whose metadata or hash doesn't match.
- Every prediction returns its probability margin and is explicitly marked uncalibrated. Low-margin predictions are flagged for review, and reviewer feedback is stored append-only. The repo includes a model card and a dataset decision record.

### [PulseStream](https://github.com/MurayaSoftTouch/PulseStream) · *in active development*

A Rust event-processing service focused on durable admission, safe concurrent processing, and bounded failure handling.

`Rust · Tokio · axum · sqlx · PostgreSQL · GitHub Actions`

- PostgreSQL integration tests simulate database outages through a controllable TCP proxy and verify recovery without restarting the service. Real-database tests run as a separate CI job.
- Idempotent ingestion is backed by a unique `(source, idempotency_key)` constraint and request fingerprints. Conflicting replays are rejected with `409`.
- Workers claim events with `FOR UPDATE SKIP LOCKED` under time-bound leases, capped by a configurable concurrency limit, so a crashed worker's events become claimable again.
- Retryable and permanent failures use capped exponential backoff and a durable dead-letter state. Processing is explicitly at-least-once. 8 ADRs.

*Built with two collaborators. I owned the retry and dead-letter milestone, including its PostgreSQL tests.*

---

## Technical stack

| | |
|---|---|
| **Testing & quality** | pytest · Playwright · xUnit · JUnit 5 · Testcontainers · Toxiproxy · OpenAPI contract testing · `cargo test` |
| **Languages** | Python · Go · TypeScript / JavaScript · Java · Kotlin · Rust · C# · SQL · Elixir |
| **Backend & data** | FastAPI · Django · Flask · Node.js · Spring Boot · ASP.NET Core · React · REST · GraphQL · PostgreSQL · Redis · OAuth2 · JWT |
| **Cloud & platform** | AWS · Azure · Google Cloud · Docker · Kubernetes · Terraform · CloudFormation |
| **Reliability & delivery** | CI/CD · GitHub Actions · Prometheus · Grafana · ELK |
| **AI / ML** | Production ML · LLM evaluation · RLHF · supervised fine-tuning · model benchmarking · MLOps |

---

## How I work

- **Test the failure modes, not only the happy path.** Retries, duplicates, timeouts, and partial outages are normal inputs, and each one deserves a test.
- **A regression test must be able to fail.** I check that it goes red against the old behaviour before trusting that it's green.
- **Invariants belong in the data layer too.** The database should refuse states the business can't have, and tests should prove it.
- **Explicit contracts.** Versioned API schemas, contract tests, and recorded architecture decisions make systems safer to change.
- **Quality gates belong in CI.** If a check matters, it runs on every pull request.
- **Security and observability are part of the design.** Least privilege is built in, and if a system can't be diagnosed in production, it isn't finished.

---

## AI and LLM quality

I apply the same discipline to AI systems: LLM evaluation and benchmarking (rubric design, reviewer calibration, reproducible scoring), RLHF and supervised fine-tuning data workflows, adversarial testing and red-teaming of model behaviour, and review of AI-generated code for correctness and security.

---

More on my work at [hamman-portfolio.vercel.app](https://hamman-portfolio.vercel.app/).

Hiring for test automation, quality engineering, or backend reliability? [Let's talk on LinkedIn](https://linkedin.com/in/haman-mur) or [by email](mailto:hamanmuraya009@gmail.com).
