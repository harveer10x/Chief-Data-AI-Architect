# Architecture Evolution Roadmap
## Harveer Singh | Data Architecture Framework

---

## The Core Principle: Evolve, Don't Replace

The most expensive data architecture mistake is the "rip and replace" program.
Organizations convince themselves that the existing architecture is so broken
that the only path forward is to start over. The new platform is designed in
isolation, data is migrated in a big-bang, and the existing system is shut down.

This fails more often than it succeeds. The legacy system contains business
logic accumulated over decades. Migration reveals edge cases that no one
documented. The timeline extends. The budget grows. The business loses
confidence.

The alternative is evolution — continuous, incremental modernization that
keeps the business running while the architecture improves beneath it.
This is harder to sell to leadership because it doesn't have a clean
completion date. It is far more likely to succeed.

---

## The Strangler Fig Pattern for Data Architecture

The Strangler Fig pattern takes its name from a plant that grows around an
existing tree, gradually taking its place. Applied to data architecture:

**How it works:**
1. Identify the most valuable data flows or domains in the legacy architecture
2. Build the new architecture alongside the old — don't shut the old one down
3. Migrate one domain or data flow at a time to the new architecture
4. As each migration is complete, decommission that piece of the legacy system
5. Repeat until the legacy system is fully replaced

**Why it works:**
- The business is never fully dependent on an untested new platform
- Migration is incremental — problems are contained, not catastrophic
- Learning from early migrations informs later ones
- Decommissioning is gradual — legacy costs reduce over time rather than all at once

**Prerequisites for the Strangler Fig to work:**
- The new architecture must be able to coexist with the old one (dual-running)
- Integration layer must support routing data flows to either the old or new
  system during transition
- Clear criteria for when a domain is "done" and the legacy component can be
  decommissioned
- Business stakeholders must accept that the legacy system will be running
  during the transition — this is not a failure state

### Applying it by Pattern

**Migrating to Lakehouse:**
- Start with one analytical domain (not the most critical one — learn on
  something important but not existential)
- Build the Medallion layers for that domain on the new platform
- Run the old and new in parallel for 30–90 days to validate parity
- Switch reporting to the new platform; keep the old as fallback
- Decommission the old after 30 days of production confidence
- Repeat domain by domain

**Migrating to Data Mesh:**
- Start with the domain that is most frustrated with central ownership —
  they have the motivation to take ownership
- Stand up the platform infrastructure that domains will share
- Pilot domain decomposition with one willing, capable domain
- Document what worked and what didn't; apply lessons to the next domain
- Avoid mandating a fixed timeline across all domains — readiness varies

**Migrating from Spaghetti Integration to Hub:**
- Do not attempt to migrate all integrations at once
- Identify the highest-value, highest-pain integrations first
- Build the hub and migrate those integrations
- Each migration reduces point-to-point connections; the value compounds
- Set a policy: all new integrations go through the hub; legacy P2P
  connections are retired as the hub proves itself

---

## Cloud Migration Considerations

Cloud migration is not an architecture migration. It is a deployment migration.
Organizations that conflate the two make one of two mistakes: (1) they lift and
shift bad architecture into the cloud and call it "modern," or (2) they try to
simultaneously redesign the architecture and migrate to cloud, creating a
program that is twice as complex and twice as likely to fail.

**Recommended approach:**
1. Separate the decisions. First decide what architecture you want. Then decide
   how to deploy it, and where.
2. Cloud is a deployment decision, not an architecture decision. The Medallion
   architecture runs in a data center or in the cloud. Data Mesh can be
   on-premises or cloud-native. The architecture is independent of the
   deployment target.

### Cloud Migration Sequence

**Phase 1: Assess and Classify**
- Inventory all data assets and classify by cloud readiness
  (sensitive data, regulatory constraints, latency requirements)
- Identify dependencies: which workloads depend on on-premises systems
  that won't be migrated?
- Identify quick wins: analytical workloads with no dependencies are
  typically the easiest to move first

**Phase 2: Build the Landing Zone**
- Establish cloud governance and security before migrating data
- Define the network architecture (how does cloud connect to on-premises?)
- Define identity and access management patterns in cloud
- Migrate a non-critical workload first to validate the landing zone

**Phase 3: Migrate Incrementally**
- Migrate workloads in priority order: highest value, lowest risk first
- Run dual environments during each migration
- Validate each migration before decommissioning on-premises

**Phase 4: Optimize**
- Once workloads are in cloud, optimize for cloud-native capabilities
  (managed services, auto-scaling, serverless where appropriate)
- Eliminate lift-and-shift antipatterns — cloud should change how you
  architect, not just where you run things

### Cloud Architecture Considerations

**Storage costs compound over time.** Design data lifecycle policies from
day one. Hot, warm, and cold storage tiers should be applied to all data.
Data that isn't accessed in 90 days should move to cold storage automatically.
Data that isn't accessed in 3 years should be evaluated for deletion.

**Egress costs are a trap.** Data that lives in the cloud costs money to
move out of it. Design your architecture to minimize cross-cloud and cloud-
to-on-premises data movement. Analytics should happen where the data lives.

**Managed services reduce operational burden.** Where managed services are
available for a capability you need, prefer them over self-managed
infrastructure. The operational overhead of self-managing databases, message
queues, and compute at scale is significant.

**Multi-cloud adds complexity.** Multi-cloud is a hedge against vendor lock-in.
It is also a significant architectural and operational complexity. Be honest
about whether the lock-in risk justifies the complexity. Most organizations
are better served by a primary cloud with a secondary cloud for specific
workloads (disaster recovery, regulatory requirements, specific managed services).

---

## Governance-First vs. Technology-First

This is one of the most consequential sequencing decisions in data architecture.
The wrong choice costs years.

### The Case for Governance-First

Build the governance model before you build the platform. Define ownership,
standards, quality requirements, access policies, and stewardship before
a single byte of data moves to the new architecture.

**Why this is right:**
- Governance retrofitted into a running platform is an order of magnitude
  harder than governance designed in from the start
- Data quality problems caught by governance design (e.g., "who owns this
  dataset?") surface requirements that affect the architecture itself
- Business stakeholders engage with governance design in ways they won't
  engage with technical architecture
- The first datasets governed well become the model for all subsequent datasets

**When governance-first is non-negotiable:**
- Regulated industries (finance, healthcare, government) where compliance
  is not optional
- Organizations with significant data quality problems — poor governance
  is usually the root cause
- Data Mesh programs — federated governance must be designed before domains
  decompose

### The Case for Technology-First

Build the platform, demonstrate value, then layer governance on top.

**Why this is sometimes right:**
- In greenfield programs where there is no existing data estate to govern
- When the business needs to see value from data before they'll invest in
  governance
- When governance takes so long to design that momentum is lost

**The risk:** Technology-first almost always becomes technology-only.
"We'll handle governance later" is a statement that has never, in the
history of data programs, been followed by a functioning governance program.
The governance layer gets added when a crisis forces it — a compliance failure,
a data quality incident that causes a bad business decision, a regulatory audit.

**Recommended approach:**
Neither pure governance-first nor pure technology-first. A parallel track:
1. Stand up the platform for a limited pilot scope (one domain, one use case)
2. Simultaneously design the governance model for that pilot scope
3. Apply governance to the pilot before expanding the platform
4. Expand the platform and governance together, domain by domain

This is slower than technology-first. It is faster than governance-first alone.
It produces better outcomes than either extreme.

---

## Investment and Timeline Estimates

These are order-of-magnitude estimates for planning purposes. Every
organization's context is different. Use these for initial scoping and
investment conversation, not for contractual commitments.

### Foundational Data Architecture Program
**What it includes:** Assessment, architecture design, governance foundation,
pilot implementation on one domain, Medallion architecture for pilot domain.

| Component | Duration | Team | Investment Range |
|-----------|----------|------|-----------------|
| Assessment and design | 2–3 months | 2–3 architects | $200K–$400K |
| Governance foundation | 2–4 months | 1 governance lead + 2 business owners | $150K–$300K |
| Platform setup | 1–3 months | 2–3 engineers | $100K–$250K |
| Pilot domain implementation | 3–4 months | 3–5 engineers | $300K–$600K |
| **Total** | **6–12 months** | **5–10 FTEs** | **$750K–$1.5M** |

### Lakehouse Migration (Mid-Size Organization)
**What it includes:** Migrating from legacy EDW + Data Lake to unified Lakehouse.
Assumes 10–50 domains, 1–5 petabytes of data.

| Phase | Duration | Investment Range |
|-------|----------|-----------------|
| Architecture design | 2–3 months | $200K–$400K |
| Platform setup and governance | 2–4 months | $300K–$600K |
| Domain migration (per domain) | 1–3 months each | $100K–$250K/domain |
| Testing and validation | Embedded | Included above |
| Legacy decommission | Ongoing | Offset by license savings |

**Rough total for 10-domain migration:** $2M–$5M over 18–36 months.

### Data Mesh Program (Large Organization)
**What it includes:** Decomposing a large, centralized data estate into domain-
owned data products. Assumes 20+ domains, significant engineering investment.

| Phase | Duration | Investment Range |
|-------|----------|-----------------|
| Architecture design and governance | 3–6 months | $500K–$1M |
| Platform infrastructure | 3–6 months | $1M–$3M |
| Pilot domain (1–2 domains) | 6–12 months | $500K–$1.5M |
| Rollout (per additional domain) | 3–6 months each | $200K–$500K/domain |

**Rough total for 20-domain mesh:** $5M–$15M over 3–5 years.

### What the Investment Buys (and Doesn't)

**Investment buys:**
- Architecture that scales with the business
- Governance that reduces compliance risk
- Data quality that makes analytics trustworthy
- Self-service capability that reduces dependency on IT
- A platform that can support AI/ML programs

**Investment doesn't buy:**
- Perfection — every architecture has trade-offs
- Done — data architecture is continuous investment, not a one-time project
- Agreement — organizational change is required; investment in technology
  without investment in people and process will underdeliver

### The Hidden Cost: Organizational Change
Technology investment is the smaller part of the program. The larger
investment is organizational: data ownership, stewardship roles, governance
processes, and training. Budget at least 30–40% of total investment for
the organizational dimension. Organizations that skip this budget the
technology at 100% and the organizational change at 0%, then wonder why
adoption is low.

---

## Phased Roadmap Template

### Phase 0: Foundation (Months 0–3)
- Architecture assessment (use the 35-question framework)
- Current state documentation
- Architecture decision: which pattern(s)?
- Governance model design
- Quick wins: low-hanging fruit that demonstrate value immediately

### Phase 1: Pilot (Months 3–9)
- Platform setup for pilot scope
- One domain on the new architecture, fully governed
- Medallion architecture implemented for pilot domain
- Integration patterns validated
- User acceptance: business stakeholders validated on pilot output

### Phase 2: Expand (Months 9–24)
- Apply lessons from pilot
- Expand to 5–10 domains
- Governance operating model running
- Self-service capability for business users
- Performance benchmarked and managed

### Phase 3: Scale (Months 24–48)
- Full domain coverage
- Advanced capabilities: AI/ML data readiness, real-time where required
- Legacy decommission complete or in final stages
- Architecture optimization for cost and performance
- Continuous improvement process established
