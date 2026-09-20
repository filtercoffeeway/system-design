# System Design Course

A **bottleneck-first** course in distributed system design. Instead of memorizing
50 architectures, you learn a small set of composable **primitives** (the levers),
how to **diagnose the dominant bottleneck** of any system, and the **consequence
chain** — every lever you pull creates a new bottleneck.

> A system is `(dominant bottleneck) + (the primitives you compose to relieve it)
> + (the secondary bottlenecks that composition creates)`.

**Read it live: https://filtercoffeeway.github.io/system-design/**

## Live site

Static HTML, no build step. Open `index.html` locally, or publish via **GitHub
Pages → deploy from branch `main`, folder `/ (root)`**. Served at
`https://filtercoffeeway.github.io/system-design/`.

## What's inside

Three layers, indexed in the order you actually work through a design:

1. **Part I — Bottleneck Catalog** (on `index.html`): symptom → candidate levers →
   the new bottleneck each one introduces. The diagnosis layer.
2. **Part II — 21 Primitives** (`primitives/p1…p21.html`): the composable building
   blocks. One page each — what it is, how it works, variants, the new bottleneck
   it hands you, a real-world example, and pitfalls.
3. **Part III — 22 Systems** (`systems/s1…s22.html`): case studies. Each leads with
   its **hard constraint** and tags the primitives it exercises.

Every page has a Mermaid diagram, a named real-world example (Datadog, Kafka,
Stripe, Facebook Memcache, Google, Netflix, Uber, …), cross-links, and further
reading.

### Primitives

P1 Batching / async buffering · P2 Partitioning / sharding · P3 Replication & the
consistency ladder · P4 Caching strategies · P5 Write-time vs read-time cost ·
P6 Inverted index · P7 Scatter-gather & partial aggregation · P8 Tiered & columnar
storage · P9 Idempotency & "exactly-once-ish" · P10 Consensus, leader election &
fencing · P11 CDN & edge caching · P12 Tail latency: hedging & load shedding ·
P13 Real-time connections & routing · P14 Saga & compensation · P15 Geospatial
indexing · P16 Backpressure / flow control · P17 Storage durability & write
internals · P18 Distributed sort & external merge (MapReduce) · P19 CRDTs ·
P20 Distributed tracing · P21 Streaming aggregation & windowing

### Systems

1 Rate Limiter · 2 Message Queue / Kafka · 3 Key-Value Store (Redis / DynamoDB-style) ·
4 Relational Database Internals + Scaling · 5 Object Store (S3-style) ·
6 Distributed Metrics Logging & Aggregation (Datadog) · 7 Search Engine
(Elasticsearch / Lucene) · 8 Distributed SQL Engine (Presto / BigQuery-style) ·
9 Social Feed · 10 Chat System · 11 Notification System · 12 Distributed Task
Scheduler · 13 Distributed Lock / Leader Election (ZooKeeper / etcd) ·
14 URL Shortener · 15 Ride-Sharing / Location System · 16 Video Streaming ·
17 Payment System · 18 Web Crawler · 19 Search Autocomplete / Typeahead ·
20 Authentication & Authorization · 21 Booking / Reservation System ·
22 Top-K Trending Topics

## Status

Every page has a full draft. A **depth pass** — worked numeric examples,
algorithm-level mechanics, and "escalation ladders" that derive each design decision
from the simplest option up to the complex one — has been applied to most pages and
is tracked in [`DEPTH-PASS.md`](DEPTH-PASS.md). Newer pages are still being deepened.

## Repository layout

```
.
├── index.html                  ← landing: catalog, grids, coverage matrix, sequence
├── assets/
│   ├── style.css               ← all styling
│   └── site.js                 ← builds the sidebar nav on every page
├── primitives/  p1.html … p21.html
├── systems/     s1.html … s22.html
├── system-design-curriculum.md ← the source outline (single-file reference)
├── CLAUDE.md                   ← conventions + page templates for contributors
├── CHECKLIST.md                ← per-page progress tracker
├── DEPTH-PASS.md               ← depth-pass standards and per-page tracker
└── LICENSE                     ← MIT
```

## Contributing / extending

`CLAUDE.md` documents the page anatomy, the deep-dive section template (separate
for primitives vs systems), the Mermaid snippet, and the requirement that every
page carry a verified real-world example. `CHECKLIST.md` tracks status per page.

## Note on accuracy

The Datadog/DDSketch and Kafka facts are web-verified. Other real-world examples
were written from well-established public sources (engineering blogs, papers) with
hedged figures — see each page's *Further reading*. Verify specifics against a
current primary source before relying on exact numbers.

## License

[MIT](LICENSE)

---

*Companion to the [Filter Coffee Way](https://filtercoffeeway.com) site
([source](https://github.com/filtercoffeeway/filtercoffeeway-website)) — this repo is
the structured course; that site holds the per-topic design write-ups.*
