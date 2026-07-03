# CHECKLIST — deep-dive write-up progress

Read `CLAUDE.md` first. This file tracks which pages have a full write-up.
A page is **done** only when its `Full write-up` TODO card is replaced by a
complete deep dive following the template, with at least one verified real-world
example. Tick the box, update "Last touched", and add a changelog line.

**Status:** all 35 pages have a first full draft. **Depth pass in progress:**
the first drafts are too high-level — named concepts (e.g. "Gorilla for time
series") appear without mechanics. The depth pass adds, per page: worked
byte/bit examples with real records, numeric walkthroughs, algorithm-level
mechanics, and extra diagrams. **P8 done as the depth-pass template.**
**Next up:** roll the same treatment across the remaining pages (start with the
heaviest mechanics: P17, P5, P3, P6, S2, S6).

Legend: `[x]` done · `[~]` in progress · `[ ]` not started

---

## Primitives (Part II)  —  docs/primitives/pN.html

- [x] **P1**  Batching / async buffering        — *Datadog DogStatsD, Kafka producer*
- [x] **P2**  Partitioning / hot-key             — *Amazon Dynamo / Cassandra*
- [x] **P3**  Replication & consistency ladder   — *DynamoDB, Spanner TrueTime*
- [x] **P4**  Caching strategies                 — *Facebook Memcache (leases)*
- [x] **P5**  Write-time vs read-time (fan-out)  — *Twitter timelines*
- [x] **P6**  Inverted index                     — *Apache Lucene segments*
- [x] **P7**  Scatter-gather & partial agg       — *Elasticsearch query-then-fetch*
- [x] **P8**  Tiered & columnar storage          — *Dremel/BigQuery, Parquet, S3 classes*
- [x] **P9**  Idempotency & exactly-once-ish     — *Stripe idempotency keys*
- [x] **P10** Consensus, leader election, fencing — *Chubby / etcd, fencing tokens*
- [x] **P11** CDN & edge caching                 — *Netflix Open Connect*
- [x] **P12** Tail latency: hedging / shedding   — *Google "Tail at Scale"*
- [x] **P13** Real-time connections & routing    — *Slack / Discord gateway*
- [x] **P14** Saga & compensation                — *Uber Cadence / Temporal*
- [x] **P15** Geospatial indexing                — *Uber H3*
- [x] **P16** Backpressure / flow control        — *TCP, Netflix concurrency-limits*
- [x] **P17** Storage durability & write internals — *RocksDB / LevelDB LSM*

## Systems (Part III)  —  docs/systems/sN.html

- [x] **S1**  Rate limiter                        — *Stripe (layered limiters)*
- [x] **S2**  Message Queue / Kafka               — *LinkedIn / Kafka internals*
- [x] **S3**  Key-value store (Redis / DynamoDB)  — *Amazon Dynamo*
- [x] **S4**  RDBMS internals + scaling           — *YouTube / Vitess*
- [x] **S5**  Object store (S3-style)             — *Amazon S3 (erasure coding)*
- [x] **S6**  Distributed log + metrics (Datadog) — *Datadog Agent + DDSketch*
- [x] **S7**  Search engine (Elasticsearch)       — *Elasticsearch / Lucene*
- [x] **S8**  Distributed SQL engine              — *Presto/Trino, BigQuery*
- [x] **S9**  Social feed                         — *Twitter / Instagram*
- [x] **S10** Chat system                         — *WhatsApp (Erlang)*
- [x] **S11** Notification system                 — *Uber push platform*
- [x] **S12** Distributed task scheduler          — *SQS + Lambda, Cadence*
- [x] **S13** Distributed lock / leader election  — *Chubby, ZooKeeper, etcd*
- [x] **S14** URL shortener                       — *Bitly / TinyURL*
- [x] **S15** Ride-sharing / location (Uber)      — *Uber H3 + dispatch*
- [x] **S16** Video streaming                     — *Netflix Open Connect*
- [x] **S17** Payment system                      — *Stripe, Uber LedgerStore*
- [x] **S18** Web crawler                         — *Googlebot / Mercator*
- [x] **S19** Search autocomplete / Typeahead      — *Google Suggest, Elasticsearch completion suggester*
- [ ] **S20** Authentication & authorization       — *gap, not started (see DEPTH-PASS.md)*
- [ ] **S21** Booking / reservation system          — *gap, not started (see DEPTH-PASS.md)*
- [ ] **S22** Top-K / real-time leaderboard         — *gap, not started (see DEPTH-PASS.md)*

## New primitives (gap additions, not yet drafted)

- [ ] **P18** Distributed sort / external merge (MapReduce) — *gap, not started (see DEPTH-PASS.md)*
- [ ] **P19** CRDTs (conflict-free replicated data types)    — *gap, not started (see DEPTH-PASS.md)*
- [ ] **P20** Distributed tracing (spans, sampling, propagation) — *gap, not started (see DEPTH-PASS.md)*
- [x] **P21** Streaming aggregation & windowing — *Apache Flink (barrier snapshots), Google Dataflow/MillWheel (watermarks)*

Progress: **36 / 42** pages have a full write-up (P1–17, S1–19). The six rows
above (P18–20, S20–22) were added 2026-06-21 from a gap audit against the
"45 curated system design questions" list and have no draft yet.

---

## Per-page quality gate (applied to every page)

- [x] Follows the template sections for its type (primitive vs system).
- [x] Has a Mermaid diagram that renders.
- [x] Has ≥1 named real-world example with specifics.
- [x] Cross-links the primitives/systems it references.
- [x] "Further reading" has real source links.
- [x] Top matter + prev/next + scripts intact; no broken internal links.

## Remaining polish (optional, next sessions)

- [ ] Re-verify each real-world example's numbers/specifics against a current
      primary source (per CLAUDE.md, examples written from knowledge should be
      double-checked; the Datadog/DDSketch facts on P1/S6 are already web-verified).
- [ ] Consider a second diagram on the heavier system pages (S6, S2, S16).
- [ ] Optional: dark-mode CSS; a search box on the landing page.

---

## Changelog

- 2026-07-03 — Deepened **P3**: added §7 "Replicating read-only config: local
  evaluation & where 'serve stale' fails" — the control-plane/feature-flag
  replication pattern derived as a ladder (per-eval API → local replica + ~10s
  poll → bounded staleness), plus the two graceful-degradation holes (cold-start
  empty replica; authoritative-empty overwrite) with their replication-primitive
  fixes (bootstrap/seed a replica; explicit per-read defaults), a web-verified
  **Statsig** example (local eval, config-spec polling, data-adapter bootstrap,
  deleted-key → false), and a P11 proxy/CDN fan-in note. Renumbered §7–9 → §8–10.
- 2026-07-01 — Added a **caching** deep dive to **S6** as new §9 ("where reads
  get served from memory"), derived as a ladder: no cache → OS page cache (bytes,
  not results) → recent window in RAM → **result cache keyed on (query, closed
  time-bucket)**, safe because closed buckets are immutable so only the open
  bucket recomputes → hot/cold SSD-over-object-store tiering. New-bottleneck
  callout is cache invalidation from late/out-of-order points (watermark before
  sealing). Web-verified real example: **Datadog Husky** reader-service
  fragment-level result cache, ~80% hit rate, in-mem + persisted, immutable
  snapshots/shard-placements + time-bucketing. Renumbered old §9–§19 → §10–§20
  and bumped all inline §refs; fixed a stray "§16" that meant the P16
  backpressure primitive; added P4 to prims, a caching Q&A + talking point, and
  Husky further-reading links. All 20 headers sequential, links verified.

- 2026-07-01 — Added new primitive **P21 · Streaming aggregation & windowing**
  (~1.9k words): the Dataflow four-questions model, event- vs processing-time,
  windows/state/watermarks with a diagram, window-type + trigger + sketch
  variant tables (HLL/Count-Min/DDSketch), the new-bottleneck quad (state size,
  watermark completeness-vs-latency dial, late-data policy, exactly-once state),
  a checkpointing/barrier-snapshot subsection, and two web-verified examples
  (Apache Flink async barrier snapshotting + RocksDB state backend; Google
  MillWheel/Dataflow watermark model). Wired into site.js (primitives array +
  COMPLETE + legend → 21 primitives), index.html (tile + matrix row), and the
  prevnext chain (P20 → P21 → S1). Added a detailed **S2 failure-modes** section
  (§10): producer / broker / consumer / data-lifecycle / poison-DLQ / schema
  failure tables (silent reorder, unclean leader election, max.poll eviction,
  auto-commit, retention-expiry silent loss, DLQ traps, zombie fencing, schema
  breakage) + the "three silent killers" note; renumbered S2 §10–14 → §11–15,
  cross-linked to P21.
- 2026-07-01 — Deepened **P9**: added §5 high-throughput stream-dedup ladder
  (idempotent producer → EOS → external store+TTL → partition-aligned local
  state → Bloom) and §6 Bloom filters in depth (bit-array/k-hash mechanics, a
  worked m=16/k=3 false-positive, the FP math + optimal-k + bits/element table,
  a verified sizing example — 1B keys @1% ≈1.2GB vs 16GB exact, ~13×, computed
  in Python — the "false positive drops a real message" asymmetry, the
  Bloom-as-negative-cache pattern, and counting/scalable/cuckoo variants).
  Added a web-verified **Segment** example (partition-by-messageId + local
  RocksDB, 24h target window bounded by DB size ≈170d) tying RocksDB's SSTable
  Bloom filters to Rung D. Renumbered tail sections 5–8 → 7–10; new further
  reading (Segment, Bloom/CACM 1970, RocksDB wiki, Confluent EOS). ~1.2k→2.5k
  words. Note: site lives at repo root, not `docs/` as CLAUDE.md states.
- 2026-06-21 — Added **S19** (already built to depth, was missing from this
  checklist) and six new gap rows — **P18** distributed sort/MapReduce, **P19**
  CRDTs, **P20** distributed tracing, **S20** auth, **S21** booking/reservation,
  **S22** top-K/leaderboard — found via a gap audit against the "45 curated
  system design questions" Reddit/SystemDesign.io list. See DEPTH-PASS.md for
  the per-page ladder sketch. Progress now 36/42 (was reported as a stale 35/35).
- 2026-06-20 — Scaffolded site; wrote CLAUDE.md + CHECKLIST.md; deep-dive CSS +
  Mermaid. Completed **P1, S2, S6** by hand (web-verified Datadog/Kafka facts).
- 2026-06-20 — Completed the remaining **32** pages (P2–P17, S1, S3–S5, S7–S18)
  via batch generators (helpers.py + partA–D.py in the scratchpad), each with a
  diagram, a named real-world example, cross-links, and further reading. Removed
  all "interview" wording. Verified: 35/35 pages, 0 placeholders, 0 broken links.
- 2026-06-20 — Began **depth pass**. Rewrote **P8** from ~250 to ~1630 words:
  added the dictionary/RLE/delta/FoR encoding table with sample records, a full
  Gorilla worked example (delta-of-delta timestamp bits + XOR value bits with
  real IEEE-754 patterns, incl. window-reuse on v3), a raw-vs-Gorilla per-point
  budget, a second Mermaid diagram, a variants table, and a Facebook/Gorilla
  real-world example. Bit patterns computed in Python; Gorilla spec from the
  VLDB 2015 paper (web search was unavailable to re-verify, but the scheme is a
  fixed published spec). Note: the `Plan/docs` duplicate and `.bundle` are no
  longer in the workspace — `system-design-course` is the single source now.
