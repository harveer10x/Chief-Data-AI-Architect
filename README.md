# Data & AI Architecture — Claude Skill

**Stop making architecture decisions based on what's fashionable. Start making them based on what works — for both your data platform and the AI you're building on top of it.**

By [Harveer Singh](https://www.linkedin.com/in/harveer/) | Author, *[When Data Moves](https://whendatamoves.com/)* | Fortune 500 Chief Data Officer

---

## The Problem

Most data architecture decisions are made by engineers optimizing for technical elegance, not by CDOs optimizing for business outcomes. The wrong pattern — chosen because it was trending, not because it fit — costs millions and takes years to unwind. By the time the organization realizes the architecture is wrong, it has already been built into the foundation of every system that runs on top of it.

This skill brings 25 years of CDO-level pattern recognition into Claude. Not theory. Not vendor pitches. The real calculus of what to build, when to build it, and what failure looks like when you get it wrong.

---

## What This Skill Does

Install this skill into Claude and it will:

- **Assess your existing architecture** across five dimensions — Current State, Governance, Integration, Performance, and Future Readiness — using a structured 35-question diagnostic and score it 0–100
- **Design a new data architecture** by applying a decision matrix across six dominant patterns to recommend the right fit for your organization's size, workload, and governance maturity
- **Design an AI architecture** across the full stack — from compute and foundation model selection through RAG design, agent architecture, AI observability, and AI security — connected back to your data architecture foundation
- **Review an existing proposal** against four core principles and a catalog of known anti-patterns — and deliver a direct verdict: Approve, Approve with Conditions, Revise, or Reject
- **Identify architecture debt** already compounding costs in your environment and prioritize what to fix first
- **Produce structured deliverables**: Architecture Assessment Reports, Architecture Design Packages with Medallion guidance and integration pattern recommendations, AI Architecture Design Packages, and full Architecture Decision Records (ADRs)
- **Name failure modes before you commit to them** — the Data Swamp, Spaghetti Integration, Governance Afterthought, Monolithic Gold Layer, Premature Mesh, ungoverned RAG corpus, agents with no audit trail, models with no monitoring, and others
- **Guide real-time vs. batch decisions** by connecting latency requirements to business decision cycles, not infrastructure enthusiasm
- **Navigate the RAG vs. fine-tuning decision** with a framework grounded in cost, use case fit, and governance implications — not vendor marketing

---

## The 5+1 Architecture Patterns

Six dominant patterns. Most organizations need a combination. The skill helps you choose the right dominant pattern and understand what you're trading away in each direction.

| Pattern | Core Idea | Best Fit | Watch Out For |
|---------|-----------|----------|---------------|
| **Data Warehouse (EDW)** | Structured, modeled, governed. Transform before you load. | BI-first, compliance-heavy, SQL-literate teams | Schema rigidity kills ML workloads; ETL bottlenecks at scale |
| **Data Lake** | Raw storage first, structure later. Ingest everything. | Exploration, data science, unstructured data, cost constraints | Becomes a data swamp within 18 months without governance discipline |
| **Data Lakehouse** | Warehouse reliability on lake economics. One physical layer, multiple consumption patterns. | Mixed BI + ML/AI workloads; avoiding data duplication | Requires engineering depth; table format management is non-trivial |
| **Data Hub** | Integration-centric. Central hub receives, governs, and distributes to consumers. | Multi-system integration, canonical model enforcement, operational data sharing | Hub bottleneck; analytics workloads don't belong here |
| **Data Mesh** | Domain-owned data products. Federated execution, centralized standards. | Large orgs with mature domain teams where centralization has provably failed | Premature Mesh is the most common architecture mistake right now |
| **Data Fabric** | Metadata-driven, AI-augmented. Active metadata connects data across environments. | Complex, distributed, multi-cloud estates at scale | Fabric without metadata is a marketing term, not an architecture |

---

---

## The AI Architecture Stack

The AI architecture sits on top of your data architecture. The quality of your AI systems is bounded by the quality and governance of the data beneath them. This skill covers the full AI stack and where it connects to the data platform.

| Layer | Components | Key Decisions | Most Common Mistake |
|-------|-----------|---------------|---------------------|
| **AI Infrastructure** | GPU clusters, inference endpoints, MLOps platform | Spot vs. reserved capacity; real-time vs. batch vs. edge inference | Training and inference infrastructure not separated — they compete in production |
| **Foundation Models** | API vs. self-hosted, model selection, version management | Data residency requirements; context window; cost at production volume | Treating model API like a stateless utility — model upgrades silently change application behavior |
| **AI Data Layer** | Training data pipelines, feature stores, vector databases, embedding architecture | Feature store: needed now or not yet? Vector DB access control | Ungoverned training data — can't answer "what data trained this model?" |
| **RAG Architecture** | Ingestion → chunking → embedding → vector store → retrieval → generation | Chunking strategy; retrieval corpus governance; who controls what's in the corpus | Pointing RAG at everything with no access control — users retrieve documents they'd never be granted direct access to |
| **Agent Architecture** | Orchestrator/worker patterns, agent memory, tool calling, escalation paths | Pipeline vs. hierarchical vs. peer-to-peer; tool permission scoping | Agents deployed with no audit trail and no escalation path — "the AI did it" is not accountability |
| **AI Observability** | Drift detection, performance monitoring, hallucination tracking, AI audit trail | What to log, at what granularity; fairness thresholds before deployment | Models deployed with no monitoring — they degrade silently until the business notices |
| **AI Security** | Prompt injection mitigations, data leakage controls, AI access control, supply chain | Least-privilege for AI system identities; input validation; output validation | AI systems inheriting admin credentials because it was convenient in development |

---

## The Data-AI Integration Matrix

How each data architecture pattern handles AI workloads — and what you'll need to add.

| Data Architecture | Native AI Fit | What You Need to Add | Biggest Gap |
|-------------------|--------------|---------------------|-------------|
| **EDW** | Poor for training; adequate for structured feature serving | Separate AI data layer (lake or lakehouse) | Schema rigidity; no unstructured data support |
| **Data Lake** | Good for training storage; poor for feature serving | Feature store; vector DB; MLOps platform | Training-serving skew; governance on training data |
| **Lakehouse** | Best native fit | Feature store; vector DB | These are additions, not rebuilds — you're in the best position |
| **Data Hub** | Limited | Separate AI data layer; don't run AI workloads through the hub | Hub adds latency and bottleneck to AI data access |
| **Data Mesh** | Strong for domain AI; complex for cross-domain | Explicit cross-domain data access policy for AI training | Cross-domain AI training needs governance that Mesh must explicitly enable |
| **Data Fabric** | Strong for AI-powered discovery and catalog | Separate training and inference infrastructure | Fabric is governance/discovery, not a training data layer |

---

## The 4 Principles Every Architecture Is Evaluated Against

1. **Simplicity** — The right architecture is the simplest one that solves the actual problem. If you can't draw it on a whiteboard in five minutes, reconsider.
2. **Scalability** — It must scale in multiple directions: data volume, variety, user concurrency, and team size. Where does this break, and at what scale?
3. **Governance-by-Design** — Access controls, lineage, quality monitoring, retention, and audit trails are architectural primitives. If governance isn't in the design, it will not be in the implementation.
4. **Business Alignment** — Name three business outcomes this architecture directly enables. If you can't, stop and reframe.

---

## Installation

### Option 1 — Install the .skill file

1. Download `data-architecture.skill` from the [Releases](../../releases) page
2. Claude Desktop or Cowork → Settings → Capabilities → Install Skill
3. Drop in the file

### Option 2 — Manual (Claude Code)

```bash
git clone https://github.com/harveer10x/data-architecture-skill
```

Then reference the skill in your Claude Code project configuration.

---

## Usage

Drop any of these into Claude after installing the skill:

**Data Architecture:**
```
"Walk me through an architecture assessment. We're a mid-size financial services firm running a 6-year-old EDW. We're evaluating whether to move to a lakehouse."

"We're building a new data platform from scratch. We have 300 engineers, 12 business domains, and our primary workloads are fraud detection and customer analytics. What architecture pattern fits us?"

"Here's our proposed architecture: [describe it]. Review it against your framework and tell me what we're getting wrong."

"Our data lake is two years old and nobody trusts it. Help me diagnose what went wrong and what to fix first."

"We keep hearing we should do Data Mesh. Should we?"
```

**AI Architecture:**
```
"We're building a RAG system on top of our Lakehouse. Walk me through the full architecture — chunking, embeddings, vector store, retrieval, governance — and tell me what we're most likely to get wrong."

"Our CISO is asking how we're governing access control on our vector database. We don't have a good answer. Help me design that."

"Should we fine-tune our LLM or use RAG? We have 50,000 internal policy documents that need to be searchable."

"We're deploying AI agents that can write to our CRM. What does the governance architecture need to look like?"

"What does an AI-ready data foundation look like on top of our existing Lakehouse? What do we need to add and in what order?"

"Help me design the AI policy framework — what models can be deployed, by whom, with what approval process."
```

The skill detects your intent and routes to the right mode automatically. If the intent is ambiguous, it asks one clarifying question.

---

## Repository Structure

```
data-architecture-skill/
├── SKILL.md                        # Skill definition and operating modes (v1.1)
├── references/
│   ├── framework.md                # 5+1 patterns, decision matrix, Medallion architecture,
│   │                               # real-time vs. batch, 4 principles
│   ├── patterns.md                 # Deep dives: Hub, Fabric, Mesh, Lakehouse,
│   │                               # integration patterns, anti-pattern catalog
│   ├── ai_architecture.md          # AI architecture components: infrastructure, foundation
│   │                               # models, feature stores, vector databases, RAG stack,
│   │                               # agent architecture, AI observability, AI security,
│   │                               # and data-AI integration points
│   ├── assessment.md               # 35-question diagnostic, scoring rubric,
│   │                               # architecture debt identification, smell catalog
│   └── roadmap.md                  # Migration approaches, strangler fig, cloud
│                                   # considerations, governance-first vs. tech-first,
│                                   # investment estimates
└── assets/
    └── architecture_decision_record_template.md   # ADR template for all design outputs
```

---

## License

**Framework IP:** © Harveer Singh. The architecture frameworks, decision matrices, assessment rubrics, anti-pattern catalog, and all original intellectual property in this repository are the exclusive property of Harveer Singh.

**Skill implementation:** MIT License. The scaffolding, templates, and SKILL.md structure are freely available for use and adaptation.

---

## About the Author

Harveer Singh is a Fortune 500 Chief Data Officer with 25 years of experience leading data transformation at scale — across industries, continents, and every variety of architecture decision gone right and gone wrong. He is the founder of [Rizz Wireless](https://rizzwireless.com) and author of *[When Data Moves](https://whendatamoves.com/)*, a practitioner's account of what actually happens when data decisions meet the real world.

[LinkedIn](https://www.linkedin.com/in/harveer/) | [Newsletter: When Data Moves](https://www.linkedin.com/in/harveer/) | [Book](https://www.amazon.com/When-Data-Moves-Harveer-Singh/dp/B0GLFTWZCR)
