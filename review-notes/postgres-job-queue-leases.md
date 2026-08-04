# Review notes: PostgreSQL Job Queues Need Leases, Not Just SKIP LOCKED

Reviewed: 2026-08-04
Canonical slug: `postgres-job-queue-leases`
Privacy: `public-safe`
Knowledge status: `evidenced` for general PostgreSQL behavior; this article is a reference architecture, not a personal production case study.

## Evidence and claim boundary

### Supported claims

The article's claims about `FOR UPDATE SKIP LOCKED`, Read Committed snapshots and row locking, transaction-scoped locks, and transactional notification delivery are grounded in the PostgreSQL 18 documentation listed below.

### General technical explanation

The lease schema, claim query, fencing-token checks, heartbeat, recovery query, metrics, and failure tests are an original reference design assembled from documented PostgreSQL primitives and established distributed-systems failure reasoning. Code values such as a 60-second lease, 30-second retry delay, and eight attempts are illustrative, not measured recommendations.

### Personal evidence boundary

The public article makes no first-person implementation, employer, client, deployment, user, throughput, latency, or outcome claim. It explicitly says that it is a reference architecture and not a measured production deployment. PostgreSQL appears in Ghassan's inspected project evidence, but that evidence is not used to imply that he built or operated this exact queue.

### Inference and open limits

A fencing token protects updates that check the token. It cannot fence an external side effect unless the destination participates through an idempotency key, version check, or another compatible protocol. `SKIP LOCKED` enables concurrent claiming but does not establish strict FIFO or fairness. `NOTIFY` is treated only as a wake-up optimization because durable work remains in the table.

## Source ledger

All sources were retrieved on 2026-08-04.

1. PostgreSQL 18, `SELECT`, locking clause: https://www.postgresql.org/docs/current/sql-select.html
   Supports the precise statement that `SKIP LOCKED` gives an inconsistent view, is unsuitable for general-purpose work, and can avoid lock contention with multiple consumers of a queue-like table.
2. PostgreSQL 18, transaction isolation: https://www.postgresql.org/docs/current/transaction-iso.html
   Supports the default Read Committed behavior, per-command snapshots, and treatment of rows changed or locked by concurrent transactions.
3. PostgreSQL 18, explicit locking: https://www.postgresql.org/docs/current/explicit-locking.html
   Supports row-lock behavior, lock lifetime, deadlock cautions, and the distinction between transaction-level and session-level advisory locks.
4. PostgreSQL 18, `NOTIFY`: https://www.postgresql.org/docs/current/sql-notify.html
   Supports delivery after transaction commit and documents notification-queue limits.
5. PostgreSQL 18, `LISTEN`: https://www.postgresql.org/docs/current/sql-listen.html
   Supports listener activation at commit and the documented setup race, reinforcing periodic table reads as the durable recovery path.

No third-party estimate is presented as first-party performance evidence.

## Keyword and search intent

Primary intent: engineers evaluating or implementing a PostgreSQL-backed job queue with `SKIP LOCKED`.

Primary phrase: `PostgreSQL job queue SKIP LOCKED`.

Supporting phrases: `Postgres job queue lease`, `PostgreSQL worker queue`, `SKIP LOCKED retry`, `Postgres queue worker crash recovery`, and `job queue fencing token`.

Demand confidence is provisional because no first-party Search Console data or verified search-volume dataset was available for this package. The title and description target implementation and failure-recovery intent rather than a generic PostgreSQL tutorial.

## Competitor gap

Pages sampled on 2026-08-04:

- PostgreSQL's `SELECT` documentation explains the primitive but not a complete queue lifecycle: https://www.postgresql.org/docs/current/sql-select.html
- Prisma's tutorial demonstrates claiming, retry scheduling, and a lease-style recovery suggestion: https://www.prisma.io/blog/you-dont-need-a-job-queue-postgres-already-has-skip-locked
- Neon's queue guide demonstrates an atomic CTE claim and a query for stuck tasks: https://neon.com/guides/queue-system

The differentiated value is the failure boundary after the row lock ends. This article connects short transactions to expiring leases, token-based stale-worker fencing, progress-aware renewal, external-side-effect limits, `LISTEN`/`NOTIFY` as a non-durable wake-up path, fairness caveats, operations, and explicit crash-injection tests. It does not copy competitor wording or structure.

## Originality check

The draft was written from the source ledger and independent systems reasoning. It does not copy source phrasing beyond unavoidable PostgreSQL identifiers and short documented terms such as `SKIP LOCKED` and `Read Committed`. It does not reuse another author's anecdote, outline, metrics, or marketing framing.

Internal topic check found no existing article or Notion row for this slug or a PostgreSQL lease-based job-queue topic. Existing articles cover transactional outbox reliability, API idempotency keys, Kafka retry/DLQ design, Kubernetes shutdown, and zero-downtime migrations; this article has a separate concurrency and crash-recovery boundary.

## Factual review

- The claim query locks and updates the candidate in one statement.
- Lease expiry and token checks are shown as application protocol, not native PostgreSQL guarantees.
- The article does not promise exactly-once execution.
- The completion query rejects expired and stale leases.
- Long-job heartbeat renewal remains token-guarded and bounded by a recommended separate maximum runtime.
- Strict FIFO, global ordering, and fairness are not claimed.
- `NOTIFY` is not presented as durable storage.
- Numeric configuration values are explicitly illustrative.
- No employer, client, private repository, personal metric, or credential appears.

## Validation

Required package validation command:

`TSX_TSCONFIG_PATH=/workspace/marketing-website/tsconfig.json corepack pnpm exec tsx /opt/data/article-publication/validate-review-package.mts <review-worktree> postgres-job-queue-leases`

The final run result, exact changed-file scope, commit SHA, and remote branch verification are recorded in the Notion handoff after they pass.

## Publication notes

Category: Backend Engineering
Language: English
Suggested summary: A PostgreSQL queue needs more than concurrent row claiming. This reference design adds short atomic claims, expiring leases, fencing tokens, bounded recovery, and crash-focused tests.

The cover uses a monochrome database-to-worker flow with a cyan lease-recovery loop. It contains no text, logo, client reference, or unsupported result. The public cover URL intentionally points to `main`; it becomes live only after the independent publisher promotes this immutable review commit.
