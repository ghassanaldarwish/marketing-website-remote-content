# Review notes: Cache Stampedes Need Request Coalescing, Not Longer TTLs

package_type=multilingual_full

## Evidence and claim boundary

This package is a public-safe technical reference architecture. It makes no first-person implementation, production, employer, client, traffic, latency, or outcome claim. The numerical arrival-rate example is explicitly illustrative and explains concurrency amplification rather than reporting a measured system.

Primary public sources checked on 2026-08-08:

- RFC 5861, "HTTP Cache-Control Extensions for Stale Content": https://www.rfc-editor.org/rfc/rfc5861
- Go `singleflight` package documentation: https://pkg.go.dev/golang.org/x/sync/singleflight
- Meta Engineering, "Cache made consistent": https://engineering.fb.com/2022/06/08/core-infra/cache-made-consistent/

Claim limits:

- `stale-while-revalidate` and `stale-if-error` are cited as HTTP cache-control semantics and adapted only as general internal-service design ideas.
- Request coalescing suppresses duplicate refresh work within its coordination scope; it does not imply exactly-once execution across failures.
- A lease is not described as proof that an expired owner stopped. The article requires version or fencing protection when stale owners can still publish.
- Configuration is separated from behavioral evidence; concurrency and failure-injection tests are required to substantiate the runtime contract.

## Keyword and search intent

Primary intent: engineers searching for how to prevent a cache stampede or cache dogpile in a distributed backend.

Primary phrase: `cache stampede request coalescing`.

Supporting phrases: `single flight cache`, `stale while revalidate backend`, `distributed cache refresh lock`, `hot key cache miss`, and `cache stampede prevention`.

Demand confidence is provisional because no first-party Search Console data was available to this run. The article answers implementation intent rather than claiming search-volume estimates: it distinguishes TTL, jitter, stale serving, per-process coalescing, fleet-wide leases, origin admission control, key versioning, observability, and race tests.

## Competitor gap

Public material commonly explains one mechanism at a time: RFC 5861 defines stale serving, Go documents duplicate call suppression, and Meta discusses cache consistency and versions. This package does not copy their wording or structure. Its differentiated value is the end-to-end failure contract that connects those mechanisms.

The article explicitly covers boundaries that short recipes often omit: per-process versus fleet-wide scope, caller deadlines while waiting on shared work, stale-data safety by data class, stale-owner writes after lease expiry, origin protection during mass misses, atomic metadata updates, out-of-order invalidation, and tests that distinguish configured locks from verified behavior.

## Validation

Expected changed path set, exactly eight paths:

- `en/cache-stampede-request-coalescing.mdx`
- `de/cache-stampede-request-coalescing.mdx`
- `ar/cache-stampede-request-coalescing.mdx`
- `en/index.json`
- `de/index.json`
- `ar/index.json`
- `assets/articles/cache-stampede-request-coalescing/cover.png`
- `review-notes/cache-stampede-request-coalescing.md`

Validation command:

`TSX_TSCONFIG_PATH=/workspace/marketing-website/tsconfig.json corepack pnpm --dir /workspace/marketing-website exec tsx /opt/data/article-publication/validate-review-package.mts <worktree> cache-stampede-request-coalescing multilingual_full`

Pre-commit validator result on 2026-08-08: passed. Body counts were English 1,673 words, German 1,575 words, and Arabic 1,555 whitespace-delimited words. The run passed language checks, matching translation key and canonical metadata, identical fenced code blocks and URL sets, equal H2 count, parser and MDX compilation, placeholder and executable-MDX rejection, client-name and credential scans, index uniqueness, and PNG signature, byte-size, and 1536x864 dimension checks.

The delivery gate additionally requires the exact eight-path set with mode `100644`, `git diff --check`, a clean committed worktree, and a second successful validator run at the immutable remote review SHA. Those checks are recorded by the delivery workflow rather than asserted from article content alone.
