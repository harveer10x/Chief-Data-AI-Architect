# Data Architecture Framework
## Harveer Singh | 25 Years of CDO Experience

---

## The 5+1 Architecture Patterns

There are six dominant patterns in modern data architecture. Most organizations
need a combination. The mistake is picking a pattern because it's popular, not
because it fits the problem.

---

### 1. Data Warehouse (EDW)
**Core idea:** Structured, modeled, governed. Data is transformed and loaded
into a well-defined schema before analysis.

**When it's right:**
- Business intelligence is the primary workload
- Regulatory compliance demands structured, auditable data lineage
- The organization has a mature analytics team that writes SQL
- Data volumes are large but not extreme (petabyte-scale EDWs work; exabyte-
  scale starts to strain)
- Stability and consistency matter more than flexibility

**When it's wrong:**
- You need to explore data before you know what questions to ask
- Data scientists need raw, unmodeled data for feature engineering
- You're dealing with unstructured or semi-structured data at volume
- Schema changes are frequent and costly in your domain

**Signature strengths:** Query performance, governed access, auditability,
SQL literacy of users.

**Signature weaknesses:** Schema rigidity, ETL bottlenecks, cost at scale,
poor fit for ML workloads.

---

### 2. Data Lake
**Core idea:** Raw storage first, structure later. Ingest everything; figure
out what you need when you need it.

**When it's right:**
- Exploration is the primary use case — data scientists, not business analysts
- You have diverse, unstructured, or semi-structured data
- Cost of storage is a constraint (lakes are cheap)
- You're building for future use cases you can't fully define yet

**When it's wrong:**
- You think you can govern it "later" (you can't)
- Business users need reliable, consistent reports
- Data quality discipline is low — the lake becomes a swamp within 18 months

**Signature strengths:** Flexibility, cost efficiency, ML/AI workload support,
schema-on-read.

**Signature weaknesses:** Governance vacuum, query performance, data quality
erosion, "data swamp" failure mode.

---

### 3. Data Lakehouse
**Core idea:** Combine the flexibility of a lake with the reliability and
performance of a warehouse. One physical storage layer, multiple logical
consumption patterns.

**When it's right:**
- You need both BI and ML/AI workloads from the same platform
- You want to avoid data duplication between a lake and a warehouse
- Your team can manage table formats (Delta Lake, Apache Iceberg, Apache Hudi)
- You're building greenfield or have the capacity to modernize

**When it's wrong:**
- Your team doesn't have the engineering depth to manage table formats and
  compute separation
- You need a proven, commodity solution with low operational overhead
- Your workloads are clearly one type (pure BI or pure ML) — simpler patterns
  may serve you better

**Signature strengths:** Unified storage, ACID transactions on the lake,
time travel, schema evolution, one source of truth.

**Signature weaknesses:** Operational complexity, requires engineering
sophistication, governance tooling is still maturing.

---

### 4. Data Hub
**Core idea:** Integration-centric. A central hub receives data from spoke
systems, applies governance and transformation, and distributes to consumers.
Hub-and-spoke topology.

**When it's right:**
- Integration is the core problem, not analytics
- Multiple source systems need to share data with multiple consumers
- You need a canonical data model to resolve naming and definitional conflicts
  across systems
- Operational data sharing (not just analytics) is a primary use case

**When it's wrong:**
- The hub becomes a bottleneck — every integration goes through one team
- You're trying to do analytics at scale (the hub is for integration, not
  heavy analytics workloads)
- The governance model at the hub is immature — you'll distribute dirty data
  at scale

**Signature strengths:** Integration decoupling, canonical model enforcement,
centralized governance of shared data, operational data sharing.

**Signature weaknesses:** Hub bottleneck, single point of failure risk,
analytics workloads don't belong here.

---

### 5. Data Mesh
**Core idea:** Domain-oriented, federated data ownership. Each domain owns its
data as a product. Central governance sets standards; domains implement them.
Decentralized execution with centralized policy.

**When it's right:**
- You have multiple mature domains with capable engineering teams
- Centralized data ownership has become a bottleneck to the business
- Data is diverse enough that no single team can own it all well
- Your governance model can operate federally — standards without
  micromanagement

**When it's wrong:**
- Your domains don't have engineering capacity to own data products
- Governance maturity is low — federated governance will devolve to no
  governance
- You're a small organization — the coordination overhead exceeds the benefit
- You're doing this because it's fashionable, not because centralization has
  actually failed you

**Signature strengths:** Domain ownership, scalability of teams, data as a
product discipline, reduced central bottleneck.

**Signature weaknesses:** Coordination overhead, governance complexity,
interoperability challenges, requires high organizational maturity.

---

### 6. Data Fabric
**Core idea:** Metadata-driven, AI-augmented architecture. Active metadata
connects data across environments. Discovery, lineage, and access are driven
by the fabric layer, not by hand-crafted pipelines.

**When it's right:**
- You have data distributed across on-premises, cloud, and multi-cloud
- Manual integration at scale is breaking you — you need automation
- Your governance team needs to manage thousands of assets, not hundreds
- You're investing in AI-augmented data management for the long term

**When it's wrong:**
- You don't have a metadata foundation to build on — fabric without metadata
  is vapor
- Your data estate is manageable without it — don't add complexity for
  complexity's sake
- The market for Data Fabric tooling is still maturing; expect rough edges

**Signature strengths:** Works across heterogeneous environments, AI-powered
discovery and lineage, scales to complex, distributed estates.

**Signature weaknesses:** Tooling maturity, requires strong metadata
discipline, risk of over-engineering simpler problems.

---

## Decision Matrix

Use this to select the primary pattern. Most organizations end up with a
dominant pattern plus elements from others.

| Factor | EDW | Data Lake | Lakehouse | Data Hub | Data Mesh | Data Fabric |
|--------|-----|-----------|-----------|----------|-----------|-------------|
| Primary workload: BI/Reporting | ★★★ | ★ | ★★★ | ★★ | ★★ | ★★ |
| Primary workload: ML/AI | ★ | ★★★ | ★★★ | ★ | ★★ | ★★ |
| Primary workload: Integration | ★★ | ★ | ★★ | ★★★ | ★★ | ★★★ |
| Org size: Small (<500 employees) | ★★★ | ★★ | ★★ | ★★ | ★ | ★ |
| Org size: Mid (500–5,000) | ★★★ | ★★ | ★★★ | ★★★ | ★★ | ★★ |
| Org size: Large (5,000+) | ★★ | ★★ | ★★★ | ★★ | ★★★ | ★★★ |
| Governance maturity: Low | ★★★ | ★ | ★★ | ★★ | ★ | ★ |
| Governance maturity: High | ★★ | ★★ | ★★★ | ★★★ | ★★★ | ★★★ |
| Engineering depth: Low | ★★★ | ★★ | ★ | ★★ | ★ | ★ |
| Engineering depth: High | ★★ | ★★ | ★★★ | ★★ | ★★★ | ★★★ |
| Multi-cloud/hybrid environment | ★ | ★★ | ★★ | ★★ | ★★ | ★★★ |
| Speed to value: Fast | ★★★ | ★★ | ★★ | ★★★ | ★ | ★ |

★★★ Strong fit | ★★ Reasonable fit | ★ Poor fit

---

## The Medallion Architecture

The Medallion architecture is a data organization pattern, not a platform
pattern. It works inside a Lakehouse, a Data Lake, or alongside a Data Hub.
It is not a replacement for choosing the right architecture pattern — it is
a structural principle for organizing data within storage.

**Why it works:** It separates concerns. Raw data is never transformed in place.
Each layer has a clear contract. Quality compounds as data moves through layers.

### Bronze Layer (Raw)
- Data arrives exactly as it was sent by the source
- No transformation, no cleansing, no schema enforcement
- Append-only; raw records are never modified or deleted
- Includes metadata: ingestion timestamp, source system, batch ID, file name
- Schema: schema-on-read or loosely defined
- Retention: typically 90 days to 7 years depending on regulatory requirements
- Who uses it: Data engineers debugging pipelines; rarely, data scientists
  needing truly raw data

**Failure mode:** Treating Bronze as the serving layer. Raw data is not
for consumption.

### Silver Layer (Cleansed)
- Data is cleansed, validated, deduplicated, and conformed
- Referential integrity is enforced across joined datasets
- Business rules for data quality are applied here
- Schema is defined and enforced; schema evolution is managed
- Data lineage connects Silver records to Bronze source records
- Who uses it: Data engineers, data scientists, advanced analysts

**Failure mode:** Pushing too much business logic into Silver. Silver should
be "good data," not "answer-specific data."

### Gold Layer (Business-Ready)
- Domain-aligned, business-ready datasets
- Aggregated, modeled, and optimized for consumption
- Named in business language, not technical language
- Access-controlled at the business domain level
- Who uses it: Business analysts, BI tools, dashboards, applications

**Failure mode:** One monolithic Gold layer shared by all domains.
Gold should be domain-specific. A Finance Gold is different from a
Supply Chain Gold.

### When to Add a Platinum Layer
Some organizations add a Platinum layer for highly curated, certified,
executive-facing datasets. This is appropriate when: (a) the Gold layer
is being used by mixed audiences and needs subdivision, or (b) regulatory
reporting requires a formally certified dataset distinct from general use.
It is not necessary for most organizations.

---

## Real-Time vs. Batch

The question is not "should we do real-time?" The question is "what decisions
require real-time data, and what is the cost of the latency we're removing?"

### When Batch is Right
- The decision cycle is daily, weekly, or monthly (financial reporting,
  supply chain planning, most management reporting)
- Data volumes are high and processing is CPU-intensive — real-time adds cost
  without value
- Source systems don't support streaming — forcing real-time on batch systems
  creates fragility
- The governance and quality requirements favor completeness over currency

**Rule of thumb:** If the human receiving the data will act on it in more than
an hour, batch is probably fine.

### When Real-Time is Right
- Fraud detection, anomaly detection, operational alerting
- Customer-facing experiences (personalization, recommendations at the moment)
- Operational monitoring (system health, supply chain exceptions)
- When the cost of delay exceeds the cost of real-time infrastructure

### Hybrid Approaches
Most mature organizations run both. The architecture choice is how to integrate
them without creating two separate systems that diverge.

**Lambda architecture:** Separate batch and speed layers that merge at the
serving layer. Works. Complex to maintain. Common in mature shops.

**Kappa architecture:** One streaming layer handles everything; batch is just
slow streaming. Simpler. Requires streaming infrastructure sophistication.

**Streaming-first with batch backfill:** Stream everything; use batch processes
to backfill gaps and reprocess for corrections. Increasingly common in modern
lakehouse architectures.

**Recommendation:** Unless you have a genuine, business-justified need for
sub-minute latency, start with batch and a near-real-time event trigger layer.
Real-time infrastructure is expensive to build, operate, and govern. Be
certain the latency reduction justifies the cost before committing.

---

## The 4 Principles of Good Data Architecture

These are not aspirational values. They are the criteria against which every
architecture decision should be evaluated.

### 1. Simplicity
The right architecture is the simplest one that solves the actual problem.
Complexity is a debt. Every layer you add is a layer someone has to maintain,
govern, monitor, and explain. If you cannot explain the architecture in two
minutes to a non-technical stakeholder, it is too complex — or you don't
understand it well enough.

**Test:** Can you draw it on a whiteboard in under five minutes? If not,
reconsider.

### 2. Scalability
The architecture must scale in multiple directions: data volume, data variety,
user concurrency, and team size. An architecture that works for 10 datasets
and 50 users should have a clear path to 10,000 datasets and 5,000 users
without a full rebuild.

**Test:** Where does this break, and at what scale? Is that scale realistic
for this organization?

### 3. Governance-by-Design
Governance is not a feature you add after the architecture is built. If it
is not in the design, it will not be in the implementation. Access controls,
data lineage, quality monitoring, retention policies, and audit trails should
be architectural primitives, not afterthoughts.

**Test:** Where does the governance live in this design? If the answer is
"we'll handle that separately," the architecture is incomplete.

### 4. Business Alignment
Data architecture exists to serve business outcomes, not to demonstrate
technical sophistication. The architecture should be evaluated against what
business decisions it enables, what operational processes it improves, and
what risks it reduces. If a business stakeholder cannot articulate why the
architecture matters to them, it is either wrong or it has not been explained
correctly.

**Test:** Name three business outcomes this architecture directly enables.
If you can't, stop and reframe.
