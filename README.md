# Haman Muraya

**Senior Software Engineer — Backend & Distributed Systems · Cloud Platforms · AI/ML Systems**

I design and build backend systems where correctness matters: ledgers and payment flows, high-throughput services, and the platforms they run on. Nine years across fintech, banking, insurance, and e-commerce — from API and data-model design through infrastructure, observability, and production ML.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-haman--mur-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/haman-mur)
[![Email](https://img.shields.io/badge/Email-hamanmuraya009%40gmail.com-555555?style=flat-square&logo=gmail&logoColor=white)](mailto:hamanmuraya009@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-MurayaSoftTouch-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/MurayaSoftTouch)

---

## What I work on

**Distributed systems** — Service boundaries, concurrency control, idempotent and retry-safe operations, and transactional consistency across services that can fail independently.

**Backend & APIs** — Secure REST and GraphQL APIs, OAuth2/JWT and service-to-service authentication, relational data modelling, caching, and performance under load.

**Cloud & platform** — Containers and Kubernetes, infrastructure as code, CI/CD pipelines, and the monitoring and logging that make production systems operable.

**AI/ML systems** — Production ML services, evaluation and benchmarking infrastructure, inference pipelines, and LLM quality and safety workflows.

---

## Selected work

### [LedgerCore](https://github.com/MurayaSoftTouch/LedgerCore)

A double-entry financial ledger and an independent transaction-policy service, built so that money movements stay correct under retries, concurrency, and partial failure.

`C# · ASP.NET Core · Java 21 · Spring Boot · PostgreSQL · Docker · GitHub Actions`

- Balanced-journal invariants enforced twice — in the domain model and by PostgreSQL triggers — with posted history immutable at the database level and least-privilege runtime roles verified in CI.
- Idempotency keys with request fingerprinting and row-level locking in both services; journal postings write outbox events in the same transaction.
- Authenticated service-to-service calls with bounded retries, correlation IDs, and fail-closed approval when the policy service is unavailable.
- 16 ADRs, a versioned OpenAPI 3.1 contract with consumer and provider contract tests, and 400+ automated tests including Testcontainers and Toxiproxy fault-injection suites.

[View repository →](https://github.com/MurayaSoftTouch/LedgerCore)

### [IncidentIQ](https://github.com/MurayaSoftTouch/IncidentIQ)

An incident-triage service that classifies incoming reports, says how uncertain it is, and routes low-confidence cases to a human reviewer.

`Python · scikit-learn · FastAPI · SQLAlchemy · Next.js · Playwright · Docker · GitHub Actions`

- Model selection on validation macro-F1 against a dummy baseline, with a time-ordered split that keeps near-duplicates together to prevent leakage; the test set is scored once.
- Versioned model artifacts verified by SHA-256 hash — the API refuses to serve a model whose metadata or hash doesn't match.
- Every prediction returns its probability margin and is explicitly marked uncalibrated; low-margin predictions are flagged for review, and reviewer feedback is stored append-only.
- Model card, dataset decision record, and 66 tests across the ML pipeline, API, and end-to-end UI, run on every pull request.

[View repository →](https://github.com/MurayaSoftTouch/IncidentIQ)

### [PulseStream](https://github.com/MurayaSoftTouch/PulseStream) · *in active development*

A Rust event-processing platform focused on durable admission and safe concurrent processing.

`Rust · Tokio · axum · sqlx · PostgreSQL · GitHub Actions`

- Idempotent ingestion backed by a unique `(source, idempotency_key)` constraint and request fingerprints; conflicting replays are rejected with `409`.
- Workers claim events with `FOR UPDATE SKIP LOCKED` under time-bound leases, capped by a configurable concurrency limit, so a crashed worker's events become claimable again.
- 7 ADRs and PostgreSQL integration tests that simulate database outages through a controllable TCP proxy. Retries, dead-lettering, and metrics are next on the public roadmap.

[View repository →](https://github.com/MurayaSoftTouch/PulseStream)

---

## Technical stack

| | |
|---|---|
| **Languages** | Python · Go · TypeScript / JavaScript · Java · Kotlin · SQL · Elixir |
| **Backend & data** | Django · Flask · Node.js · Spring Boot · React · REST · GraphQL · PostgreSQL · Redis · OAuth2 · JWT |
| **Cloud & platform** | AWS · Azure · Google Cloud · Docker · Kubernetes · Terraform · CloudFormation |
| **Reliability & delivery** | CI/CD · GitHub Actions · Prometheus · Grafana · ELK |
| **AI / ML** | Production ML · LLM evaluation · RLHF · Supervised fine-tuning · Model benchmarking · MLOps |

---

## How I work

- **Correctness before cleverness.** Invariants belong in the data layer as well as the code — the database should refuse states the business can't have.
- **Design for failure, not only the happy path.** Retries, duplicates, timeouts, and partial outages are normal inputs; every external call needs a defined failure mode.
- **Explicit contracts.** Versioned API schemas and recorded architecture decisions make systems easier to change safely.
- **Security is architecture.** Authentication, authorization, and least privilege are designed in, not added at the end.
- **Observability is part of the feature.** If it can't be diagnosed in production, it isn't finished.
- **Measure before optimizing, and choose boring technology** when boring technology is sufficient.

---

## AI and LLM engineering

Alongside backend work, I build and evaluate AI systems with the same engineering discipline:

- LLM evaluation and benchmarking — rubric design, calibration across reviewers, and reproducible scoring
- RLHF and supervised fine-tuning data workflows
- Adversarial testing and red-teaming of model behaviour
- Review of AI-generated code for correctness and security
- Production ML services, inference pipelines, and MLOps

---

Working on backend platforms, fintech infrastructure, AI systems, or a hard distributed-systems problem? [Let's talk on LinkedIn](https://linkedin.com/in/haman-mur) or [by email](mailto:hamanmuraya009@gmail.com).
