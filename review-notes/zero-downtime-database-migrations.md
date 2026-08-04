# Review notes

Migrated from the validated legacy wiki review package under Ghassan's standing automatic-publication approval.

## Evidence and claim boundary

- **Supported first-person claims:** none. This reference architecture does not claim that Ghassan executed this exact migration protocol in production.
- **Adjacent evidence:** [[databases-system]] shows a design-only PostgreSQL topology, and [[pipeline]] shows a design-only multi-environment release pipeline. Neither source proves online schema migration implementation, scale, availability, or outcomes.
- **General technical explanation:** PostgreSQL lock behavior, concurrent index creation, constraint validation, parallel change, and multi-release migration concerns are grounded in the linked PostgreSQL, Martin Fowler, GitLab, Prisma, and Squawk sources.
- **Original contribution:** the compatibility-protocol framing, five-phase sequence, cutover gate, backfill controls, rollback boundary, and transition-focused test plan are original synthesis.
- **Inference:** recommendations about ownership, observation windows, safety thresholds, and semantic parity are engineering judgments whose exact implementation depends on the system.
- **Open or unverified:** no production result, dataset size, migration duration, availability percentage, search volume, or personal implementation claim is made.
- **Privacy exclusions:** no employer, client, private repository, proprietary schema, credential, address, or confidential metric appears.

## Keyword and search intent

- **Primary topic/query:** `zero downtime database migrations`.
- **Intent:** implementation guidance and architecture decision support.
- **Reader outcome:** design a PostgreSQL schema change that supports overlapping application versions, bounded backfills, verifiable cutover, rollback, and delayed cleanup.
- **Secondary concepts:** expand and contract migration, parallel change, backward-compatible database schema, PostgreSQL lock timeout, `CREATE INDEX CONCURRENTLY`, `NOT VALID`, `VALIDATE CONSTRAINT`, online backfill, rolling deployment database migration.
- **Language/region:** English; global technical audience with relevance to Germany-based backend and platform hiring.
- **Demand confidence:** **provisional**. Live search on 2026-08-03 returned current official documentation, product guides, and implementation articles for the same problem, but ghassan.de Search Console volume remains too small for topic selection and no search-volume estimate is claimed ([[search-console-baseline-2026-07-29]]).
- **Internal-link candidates:** [[databases-system]], [[pipeline]], `/en/articles`, and `/en/about`. Publication routes are suggestions, not claims that this draft is live.
- **Measurement:** after separate wording and publication approval, verify indexing and compare relevant non-brand impressions, clicks, CTR, query mix, and qualified conversations at 28 and 90 days.

## Competitor gap

Retrieved 2026-08-03:

- [GitLab Docs — Avoiding downtime in migrations](https://docs.gitlab.com/development/database/avoiding_downtime_in_migrations/): detailed operational rules and framework-specific helpers for column deletion, rename, type changes, views, and data migration. This article adds a framework-neutral compatibility contract, explicit cutover invariants, rollback boundary, and transition test plan.
- [Prisma Data Guide — Using the expand and contract pattern](https://www.prisma.io/dataguide/types/relational/expand-and-contract-pattern): clear end-to-end explanation with a worked schema transformation. This article is narrower about production controls: lock queues, bounded backfills, runtime caller evidence, PostgreSQL online DDL caveats, and contract gating.
- [Harness — Zero-Downtime Database Migrations](https://www.harness.io/blog/zero-downtime-database-migrations-safe-schema-changes): concise pattern overview emphasizing backward compatibility, dual writes, and phased rollout. This article adds executable PostgreSQL examples, semantic parity, failure recovery, instrumentation, and destructive-cleanup criteria.
- [DeployHQ — Database Migration Strategies for Zero-Downtime Deployments](https://www.deployhq.com/blog/database-migration-strategies-for-zero-downtime-deployments-a-step-by-step-guide): step-by-step expand-contract introduction with a column-rename example. This article differentiates local transaction atomicity from deployment-wide compatibility and treats rollback plus transition testing as first-class design work.

**Differentiated value:** a PostgreSQL-oriented but framework-neutral protocol that connects application-version overlap, lock behavior, restartable backfills, parity evidence, read cutover, rollback semantics, delayed destruction, and failure-injection tests.

### Publication metadata

- **SEO title:** Zero-Downtime Database Migrations: A Compatibility Protocol
- **SEO description:** Design PostgreSQL schema changes as a compatibility protocol across old code, new code, backfills, constraints, rollback, and cleanup.
- **Canonical slug:** `zero-downtime-database-migrations`
- **Category:** Backend Engineering
- **Tags:** PostgreSQL, database migrations, backend engineering, platform engineering, reliability
- **Target audience:** senior backend engineers, platform engineers, DevOps engineers, engineering managers, and technical founders
- **Cover asset:** `wiki/articles/assets/zero-downtime-database-migrations-cover.png`
- **Cover alt:** Old and new application versions sharing parallel database schema paths before the legacy path is removed.

## Validation

Frontmatter, the 1,840-word article body, article wikilinks, ten source URLs, 1672×941 cover integrity, and `git diff --check` passed on 2026-08-03. The final Markdown and cover were uploaded directly to the [Ready for Review ticket](https://app.notion.com/p/Zero-Downtime-Database-Migrations-Need-Compatibility-Not-Just-Transactions-3b146d83e1c881119625f5e997631c13), then the ticket properties, page body, unique slug/title, and two hosted files were read back through the Notion API. Ghassan's wording review remains open; publication remains a separate approval gate.
