# Review notes

Migrated from the validated legacy wiki review package under Ghassan's standing automatic-publication approval.

## Evidence and claim boundary

- **Supported first-person claims:** none. This reference architecture does not claim that Ghassan deployed this exact retry system.
- **General technical explanation:** Kafka partition ordering, offsets, consumer processing, Kafka Streams commit behavior, idempotent consumers, bounded retries, and DLQ handling are grounded in the linked sources.
- **Original contribution:** the failure-classification state machine, explicit quarantine transition, ordering decision criteria, failure envelope, replay gate, operational checklist, Mermaid diagram, and test plan are original synthesis.
- **Inference:** recommendations such as terminal-by-default quarantine, dedicated replay topics, and oldest-record-age alerting are bounded engineering judgments, not universal guarantees.
- **Open or unverified:** no throughput, latency, production result, search volume, or exactly-once external-effect claim is made.
- **Privacy exclusions:** no employer, client, private repository, proprietary topology, credential, address, or confidential metric appears.

## Keyword and search intent

- **Primary topic/query:** `kafka consumer retry dead letter queue`.
- **Intent:** implementation guidance and architecture decision support.
- **Reader outcome:** choose blocking versus non-blocking retry, design safe offset transitions, preserve diagnostic context, protect business effects, and operate controlled replay.
- **Secondary concepts:** Kafka DLQ, retry topic, poison pill, consumer offset, partition ordering, idempotent consumer, failure classification, replay, consumer lag.
- **Language/region:** English; global technical audience with relevance to Germany-based backend and platform hiring.
- **Demand confidence:** **provisional**. Live search on 2026-07-31 returned multiple recent implementation guides and current product documentation, but ghassan.de Search Console volume remains too small for topic selection and no search-volume estimate is claimed ([[search-console-baseline-2026-07-29]]).
- **Internal-link candidates:** [[transactional-outbox-reliability]], `/en/articles`, and `/en/about`. Publication routes are suggestions, not claims that this draft is live.
- **Measurement:** after separate wording and publication approval, verify indexing and compare relevant non-brand impressions, clicks, CTR, query mix, and qualified conversations at 28 and 90 days.

## Competitor gap

Retrieved 2026-07-31:

- [Confluent — Apache Kafka Dead Letter Queue](https://www.confluent.io/learn/kafka-dead-letter-queue/): broad explanation of DLQ components, bounded retries, monitoring, and reprocessing; light on the publish-before-offset-commit failure window, ordering loss across retry topics, and replay governance.
- [Factor House — Dead letter queues in Kafka: patterns and pitfalls](https://factorhouse.io/articles/dead-letter-queues-kafka): detailed coverage of Spring Kafka, Connect, Streams, retry tiers, ordering, monitoring, and replay, with a product-led operational section. This article narrows the story around a framework-neutral failure state machine and makes the source-offset/quarantine atomicity gap central.
- [OneUptime — How to Handle Dead Letter Queues in Kafka](https://oneuptime.com/blog/post/2026-01-24-handle-dead-letter-queues-kafka/view): extensive Java, Python, Spring, monitoring, and retry examples. This article adds explicit failure classification, deterministic quarantine identity, replay blast-radius controls, privacy bounds, and tests for crash boundaries.
- [Microservices.io — Idempotent Consumer](https://microservices.io/patterns/communication-style/idempotent-consumer.html): authoritative, concise treatment of duplicate-safe database effects; intentionally does not cover Kafka retry topology, quarantine operations, or replay.

**Differentiated value:** one framework-neutral design that follows a failed record from exception classification through retry choice, source-offset transition, idempotent business effect, terminal quarantine, governed replay, and failure-injection tests.

### Publication metadata

- **SEO title:** Kafka Consumer Retries: Ordering, DLQs, and Safe Replay
- **SEO description:** Design Kafka consumer retries without hidden data loss: classify failures, preserve offsets and context, bound retries, protect ordering, and govern DLQ replay.
- **Canonical slug:** `kafka-consumer-retry-dlq`
- **Category:** Backend Engineering
- **Tags:** Kafka, backend, distributed systems, reliability, event-driven architecture
- **Target audience:** senior backend engineers, platform engineers, engineering managers, and technical founders
- **Cover asset:** `wiki/articles/assets/kafka-consumer-retry-dlq-cover.png`
- **Cover alt:** A partitioned event stream splitting through a decision gate into success, bounded retry, and quarantined dead-letter paths.

## Validation

Frontmatter, the 1,654-word article body, wikilinks, source retrieval, cover integrity, and `git diff --check` passed on 2026-07-31. The final Markdown and cover were uploaded directly to the [Ready for Review ticket](https://app.notion.com/p/Kafka-Retries-Without-Losing-Control-3ae46d83e1c881c8af50fceb804dfc9f) and read back through the Notion API. Ghassan’s wording review remains open; publication remains a separate approval gate.
