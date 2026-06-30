# Architecture Patterns — Deep Dive
## Harveer Singh | Data Architecture Framework

---

## Data Hub Design

The Data Hub is about integration, not analytics. Organizations confuse the two
constantly, and it causes them to overload the hub with workloads it was never
designed to handle.

### Hub Types

**Operational Hub**
Designed for operational data sharing: source systems publish data to the hub,
consuming systems subscribe. Focus is on latency (near-real-time to real-time),
availability, and correctness.
- Typical data: master data, reference data, operational transactions
- Latency target: seconds to minutes
- Consumers: operational applications, downstream systems

**Analytical Hub**
Designed to consolidate data from multiple sources for reporting and analysis.
Less focus on real-time; more focus on completeness, consistency, and history.
- Typical data: enriched transactions, conformed dimensions, aggregated metrics
- Latency target: minutes to hours
- Consumers: BI tools, reporting platforms, data science environments

**Universal Hub (both)**
Attempts to serve both operational and analytical workloads. Works if the
architecture separates the two paths cleanly inside the hub. Often fails when
the separation is not maintained.

### Spoke Integration Patterns
- **Canonical model:** Define a hub-native data model. Spokes map to it.
  The hub does not adapt to each spoke's idiosyncrasies — spokes do the work.
  This is non-negotiable. Hubs without a canonical model become translators
  for every pair of systems, which is unmaintainable.
- **Publish-subscribe:** Source spokes publish events; consumer spokes
  subscribe. Decoupled. Resilient. Requires reliable message infrastructure.
- **Request-response:** Consumer requests data from the hub on demand.
  Simpler. Creates coupling. Works for low-volume, latency-tolerant use cases.
- **Batch extract:** Source spokes push batches to the hub on schedule.
  Simple. Not real-time. Acceptable for many integration use cases.

### Governance at the Hub
The hub is the right place to enforce data governance at the integration layer.
- **Data quality gates:** Data entering the hub is validated against quality
  rules. Failing records are quarantined, not passed through.
- **Canonical identity resolution:** Entity matching (customer, product,
  location) is resolved at the hub. Downstream consumers receive a single,
  resolved identity, not the source-system identifiers.
- **Access control:** The hub controls which consumers can see which data.
  Not every consumer should see everything.
- **Lineage:** Every record in the hub should be traceable to its source.
- **Data contracts:** Each spoke should operate under a formal data contract —
  schema, quality SLAs, latency guarantees. The hub enforces the contract.

---

## Data Fabric Design

Data Fabric is the most misunderstood of the six patterns. It is marketed as
an architecture. It is better understood as a capability layer — a metadata-
driven integration and discovery fabric that operates across your existing
architecture.

### The Metadata Layer
The Fabric is only as good as its metadata. This is not aspirational —
it is mechanistic. Without comprehensive, active metadata, a Data Fabric is
just a marketing term.

**Metadata types the fabric must cover:**
- **Technical metadata:** Schema, format, location, lineage, version
- **Business metadata:** Owner, definition, domain, sensitivity, usage
- **Operational metadata:** Quality scores, freshness, access logs, usage patterns
- **Social metadata:** Who uses this? Who rated it? Who knows it best?

### Active Metadata
Active metadata is metadata that drives automated action, not just documentation.
- Discovery triggers based on access patterns — the fabric learns what data
  is valuable and surfaces it automatically
- Quality monitoring that alerts owners when data degrades
- Lineage that updates in real-time as pipelines run
- Automated classification and tagging based on content analysis

### AI-Powered Discovery
The Fabric uses AI to augment human navigation of complex data estates.
- Semantic search across assets (find data by business concept, not technical name)
- Recommendation of related datasets
- Automated impact analysis when schemas change
- Natural language interfaces to data catalog

**Caution:** AI-powered discovery is only as useful as the metadata it runs on.
Organizations that treat metadata as an afterthought will get AI-powered
nonsense from their Fabric.

### When the Fabric Breaks
- Metadata coverage below ~70% of the estate: discovery doesn't work
- No active metadata — the fabric is a static catalog, not a living system
- Governance of the fabric itself is not defined — who owns the fabric?
  Who ensures metadata quality?
- The fabric is treated as a product, not a platform — it needs continuous
  investment and ownership

---

## Data Mesh Design

Data Mesh is an organizational architecture as much as it is a technical one.
Organizations that treat it as a technology choice miss the point entirely.

### Domain Decomposition
The first and most difficult decision in Data Mesh is how to decompose domains.
There is no universal answer. Principles:
- Domains should align with business capabilities, not organizational charts
  (charts change; capabilities are more stable)
- Each domain should be able to own its data end-to-end without depending on
  a central team for routine operations
- Domains should be sized so that a small, capable team (5–10 engineers) can
  manage the domain's data products sustainably
- Cross-domain data should be explicit: if Domain A needs data from Domain B,
  that relationship is formalized as a data product contract, not an informal
  pipeline

**Common decomposition mistakes:**
- Decomposing by source system instead of business capability (source systems
  come and go; business capabilities don't)
- Creating too many domains — each domain has coordination overhead
- Creating domains that don't have engineering capacity to own data products

### Data Product Thinking
In Data Mesh, data is treated as a product: it has owners, consumers, quality
SLAs, versioning, and a defined interface. This is a significant cultural shift
for most organizations.

**A data product has:**
- A discoverable interface (registered in the catalog)
- A defined schema and contract (consumers can rely on it)
- Quality guarantees (freshness, completeness, accuracy — quantified)
- Versioning (breaking changes are managed like API versions)
- An owner who is accountable for all of the above

**Signs your organization isn't ready for data products:**
- "Data quality is IT's problem, not mine" — product ownership requires
  business accountability
- No engineering capacity in business domains
- No catalog or metadata infrastructure to make products discoverable

### Federated Governance
The central governance function in Data Mesh does not own data. It owns
standards. The distinction is critical.

**Central platform provides:**
- The tooling infrastructure that domains use to publish data products
- The governance standards: quality thresholds, security classifications,
  metadata requirements, interoperability standards
- The catalog for discovery
- The policy enforcement layer (access control, compliance, auditing)

**Domains are responsible for:**
- Implementing governance standards within their domain
- Maintaining data product quality within their SLAs
- Responding to governance violations in their domain

**Where federated governance fails:**
- Central team tries to review every data product (bottleneck recreated)
- Domains ignore standards because there's no enforcement
- No interoperability standards — data products can't join across domains

---

## Lakehouse Design

### Table Formats
The Lakehouse depends on open table formats to provide warehouse-like
capabilities on top of object storage. Three dominate:

**Delta Lake**
- ACID transactions on object storage
- Time travel (query data as of a past point in time)
- Schema enforcement and evolution
- Optimized for the Spark ecosystem
- Strong in environments where Spark is the primary compute engine

**Apache Iceberg**
- Table format standard with broad engine support
- Strong partition evolution (change how data is partitioned without rewriting)
- Hidden partitioning (queries don't need to know the partition scheme)
- Strong for multi-engine environments where data is read by multiple compute
  engines

**Apache Hudi**
- Optimized for record-level upserts (change data capture use cases)
- Near-real-time ingestion patterns
- Strong in CDC-heavy architectures where row-level updates are frequent

**Choosing a table format:**
- If you're primarily on Spark and want simplicity: Delta Lake
- If you need multi-engine support or strong partition evolution: Iceberg
- If CDC and row-level upserts are your primary ingestion pattern: Hudi
- If you're uncertain: Iceberg has the broadest engine support and is the
  most format-neutral choice

### Compute Separation
The Lakehouse stores data in open formats on object storage. Compute engines
are separate and interchangeable. This is a design principle, not just an
implementation detail.

**Benefits of compute separation:**
- Scale compute independently from storage
- Use different compute engines for different workloads (SQL for BI,
  Spark for ML, streaming engine for real-time)
- Avoid vendor lock-in on the compute layer

**What compute separation requires:**
- Open table formats (see above)
- A metadata catalog that multiple engines can read
- Carefully managed concurrency — multiple writers on the same table
  need ACID guarantees

### Serving Layer
The Lakehouse serving layer is where data is made available to consumers.
Gold-layer datasets are typically served through:
- SQL query engines for BI and reporting
- DataFrame APIs for data science
- REST or GraphQL APIs for applications
- Export to operational systems as needed

**Common serving layer mistake:** Building Gold as one undifferentiated pool.
Gold should be domain-specific views or schemas. A single Gold schema that
everyone queries becomes a performance and governance nightmare.

---

## Integration Patterns

### Change Data Capture (CDC)
**What it is:** Capturing database changes (inserts, updates, deletes) as they
happen and streaming them to target systems.

**When to use it:**
- Source system databases support CDC (most modern databases do)
- You need near-real-time synchronization without full table reloads
- Row-level updates and deletes are frequent in your source data

**When not to use it:**
- Source systems can't support the log-based CDC overhead (older, fragile
  systems may not)
- Changes are infrequent — a nightly batch is simpler and equally effective
- You need point-in-time completeness, not ongoing delta streams

**Implementation considerations:**
- Log-based CDC (reading database transaction logs) is more reliable than
  trigger-based CDC, which can degrade source system performance
- CDC pipelines need to handle schema changes in the source — this is the
  most common failure point

### Event Streaming
**What it is:** Systems publish events to a durable, ordered event stream.
Consumers subscribe and process events in order or near-order.

**When to use it:**
- Decoupled, asynchronous integration between multiple producers and consumers
- Event-driven architectures where downstream systems react to events
- Real-time analytics on event streams
- The firehose pattern: capture everything, process for different purposes

**When not to use it:**
- Simple point-to-point integration — event streaming adds infrastructure
  overhead without benefit
- Consumers need complete, queryable datasets, not event streams
- Your team doesn't have streaming infrastructure expertise

**Common failure modes:**
- Schema evolution not managed: producers change event schemas, consumers break
- Consumer lag not monitored: consumers fall behind the stream and never catch up
- Event ordering assumptions: consumers assume strict ordering that the
  infrastructure doesn't guarantee

### API-First Integration
**What it is:** Systems expose data through APIs (REST, GraphQL, gRPC).
Consumers request data on demand.

**When to use it:**
- Operational data sharing where consumers need current data on request
- External partner integration where you don't control the consumer
- Microservice architectures where services need to share data
- When you need fine-grained access control on every request

**When not to use it:**
- High-volume analytical queries — APIs are expensive per-call at analytics scale
- Bulk data transfer — APIs are not designed for moving large volumes
- You need history, not just current state

### Batch ETL
**What it is:** Extract data from source, transform it, load it to target.
Scheduled, bounded, complete.

**When to use it:**
- Latency requirement is hours or days, not seconds
- Transformation logic is complex and benefits from full dataset context
  (aggregations, joins across large datasets)
- Source systems can only expose data in batch (file exports, scheduled reports)
- Operational reporting with daily close cycles

**When not to use it:**
- Decisions require real-time data — batch ETL introduces inherent lag
- Source systems are too slow or unreliable to sustain large batch extracts

---

## Anti-Patterns

These are the failure modes seen repeatedly across organizations at every scale.
Name them. They are preventable.

### The Data Swamp
**What it is:** A Data Lake with no governance, no metadata, no quality
standards. Data arrives, data accumulates, data is never found or trusted.

**Symptoms:**
- "We have the data somewhere but we can't find it"
- No catalog; discovery is by email or tribal knowledge
- Quality of data in the lake is unknown
- Data engineers spend more time answering "what's in the lake?" than building

**Why it happens:** Organizations invest in ingestion infrastructure but not
governance infrastructure. The lake gets data; governance gets "later."

**Fix:** Stop ingesting until metadata and quality standards are in place.
A lake with governance is worth 10x more than a lake without it.

### Spaghetti Integration
**What it is:** Point-to-point integration proliferates until every system
is connected to every other system by a direct, custom pipe. N systems
produce N*(N-1)/2 integrations, each owned by someone different.

**Symptoms:**
- More time spent maintaining integrations than building new capabilities
- No one knows what the authoritative source of any data is
- Schema changes in one system cause cascading failures across unrelated systems
- Integration diagrams look like a bowl of spaghetti

**Why it happens:** Each integration was the right local decision at the time.
No one owned the integration architecture.

**Fix:** Hub-and-spoke or event-driven integration. Canonical data model.
Retire point-to-point pipes as you introduce the hub.

### Governance Afterthought
**What it is:** Architecture is built; governance is bolted on afterward.
Access controls, data lineage, quality monitoring, and retention policies
are added as an afterthought — or not added at all.

**Symptoms:**
- "We'll handle governance once we're operational"
- No data lineage from source to consumption
- Access controls are managed by a spreadsheet
- Data quality issues are discovered by business users, not caught in pipelines

**Why it happens:** Governance takes time to design and adds friction to
ingestion. Under delivery pressure, it is deprioritized.

**Fix:** Governance is architectural. If it's not in the design, it will not
be in the implementation. Mandate governance primitives before opening
ingestion pipelines.

### The Monolithic Gold Layer
**What it is:** One shared Gold layer that all business users query.
Tables accumulate, nobody owns them, naming is inconsistent, deprecation
never happens.

**Symptoms:**
- Hundreds of Gold tables, most of which nobody can explain
- Business users creating their own copies of Gold data because they don't
  trust the shared layer
- Query performance degrades as more users and tables accumulate
- No formal deprecation process — tables are never retired

**Fix:** Domain-partitioned Gold layers. Each domain owns and maintains its
Gold. The catalog makes domains discoverable. Formal lifecycle management
for all Gold assets.

### The Architecture That Serves IT, Not the Business
**What it is:** Architecture optimized for technical elegance, not business
outcomes. Impressive to architects, opaque to stakeholders, irrelevant to
users.

**Symptoms:**
- Business stakeholders can't articulate why the architecture matters
- Architecture decisions are made without business input
- The architecture review board is all technical; no business representation
- "Business alignment" is a slide in the deck, not a design principle

**Fix:** Every architecture decision starts with the business problem it
solves. Every review includes business representation. Architecture is
evaluated by business outcomes, not technical criteria alone.

### The Premature Mesh
**What it is:** Adopting Data Mesh before the organizational conditions for it
exist. Domains don't have engineering capacity; governance maturity is low;
the central team hasn't failed yet — but Data Mesh is fashionable.

**Symptoms:**
- Domain teams are excited about ownership but don't have engineers to support it
- "Federated governance" means no governance in practice
- Data products are defined on paper but not maintained
- The central data team is still doing most of the work

**Fix:** Assess domain readiness before decomposing. Data Mesh is the right
answer when centralization has provably failed and domain teams are genuinely
capable. It is not the right answer because someone read a blog post about it.
