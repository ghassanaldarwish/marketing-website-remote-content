## Evidence and claim boundary

- **Framing:** public-safe technical analysis and reference design. It does not claim that Ghassan deployed this exact idempotency system or achieved a production outcome.
- **Supported general explanation:** HTTP idempotent semantics are grounded in RFC 9110; caller-provided request identity and late-request concerns are grounded in the Amazon Builders' Library; response replay, parameter comparison, and retention examples are grounded in Stripe's API documentation; PostgreSQL uniqueness and `ON CONFLICT` behavior are grounded in the PostgreSQL documentation.
- **Original synthesis:** the scoped guarantee, state model, request-fingerprint boundary, local transaction design, concurrent-retry choices, fencing requirement, outcome classification, observability set, and failure-injection checklist are original synthesis.
- **Bounded inference:** recommendations about canonicalization, operation resources, retention selection, fencing, and unknown external outcomes are engineering judgments whose implementation depends on the service contract.
- **Not claimed:** no personal implementation, employer or client system, throughput, availability, incident result, exactly-once external effect, universal retention duration, or search-volume metric.

## Keyword and search intent

- **Primary topic/query:** `idempotency key API design`.
- **Intent:** implementation guidance and architecture decision support.
- **Reader outcome:** design a retry-safe `POST` API that handles concurrent duplicates, payload mismatch, crashes around commit, response replay, stale ownership, external effects, and key expiry.
- **Secondary concepts:** idempotent API, retry-safe API, idempotency key PostgreSQL, duplicate request prevention, request fingerprint, response replay, fencing token, retry backoff and jitter.
- **Language and audience:** English; senior backend and platform engineers, engineering managers, and technical founders.
- **Demand confidence:** provisional. Current search results and authoritative guidance show sustained implementation interest, but no first-party query volume or search-volume estimate is claimed.

## Competitor gap

Sources retrieved 2026-08-04:

- [Amazon Builders' Library — Making retries safe with idempotent APIs](https://aws.amazon.com/builders-library/making-retries-safe-with-idempotent-APIs/): authoritative reasoning about caller-provided intent, semantic equivalence, late-arriving requests, and reused identifiers. This article adds a framework-neutral PostgreSQL state model, local transaction boundary, concurrent-request policy, fencing check, retention operations, and executable failure tests.
- [Stripe API Reference — Idempotent requests](https://docs.stripe.com/api/idempotent_requests): a clear real API contract for saved results, parameter comparison, validation boundaries, and key pruning. This article explains how to implement the surrounding server-side state machine without presenting Stripe's policy as universal.
- [RFC 9110 — Idempotent Methods](https://www.rfc-editor.org/rfc/rfc9110.html#name-idempotent-methods): normative HTTP semantics. This article focuses on adding application-level retry safety to non-idempotent operations.
- [AWS Builders' Library — Timeouts, retries, and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/): strong operational treatment of retry amplification, timeouts, backoff, and jitter. This article narrows the problem to server-side operation identity and crash-boundary correctness.
- [PostgreSQL — INSERT](https://www.postgresql.org/docs/current/sql-insert.html): authoritative uniqueness and `ON CONFLICT` behavior. This article connects that primitive to API semantics, stable results, and recovery ownership.

**Differentiated value:** one end-to-end design that follows a timed-out `POST` through atomic claim, request binding, local commit, concurrent retry, stable replay, stale-worker fencing, external-effect limits, retention, observability, and failure injection.

## Validation

Validated on 2026-08-04 against the current production parser. The package passed MDX compilation, production filtering, `draft: false`, exact `translationKey`, no body H1, no embedded cover block, no editorial-package leakage, exact single index entry, 1,851 body words, expected main-branch cover URL, PNG signature, four-path scope, and `git diff --check`. The cover is an original 1536×864 public-safe illustration generated for this article. Publication remains outside this review branch and requires a separate approval gate.
