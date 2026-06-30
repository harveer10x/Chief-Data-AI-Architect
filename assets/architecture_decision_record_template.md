# Architecture Decision Record (ADR)
## Harveer Singh Data Architecture Framework

---

**ADR Number:** [Sequential — ADR-001, ADR-002, etc.]
**Title:** [Short noun phrase — "Primary Data Platform Pattern Selection", "Real-Time vs. Batch for Order Processing Domain"]
**Date:** [YYYY-MM-DD]
**Status:** [Proposed | Accepted | Superseded | Deprecated]
**Supersedes:** [ADR-XXX if this replaces a prior decision; blank if new]
**Superseded by:** [ADR-XXX if this has been replaced; blank if current]

---

## Context

*What is the situation that requires an architecture decision? Describe the business context, the technical landscape, and the constraints that shaped the decision space. Be specific. Vague context produces decisions that can't be re-evaluated later when circumstances change.*

**Business driver:**
[What business need or problem prompted this decision?]

**Current state:**
[What exists today? What is the gap or constraint?]

**Constraints:**
[Technical, organizational, regulatory, financial, timeline — list them all.
Constraints that are not documented here will be "forgotten" during
implementation and will come back as surprises.]

**Assumptions:**
[What did we assume to be true at the time of this decision? These are the
things most likely to invalidate the decision if they turn out to be wrong.
Document them explicitly so they can be reviewed.]

---

## Decision

*State the architecture decision in one clear sentence. Then explain it.*

**Decision statement:**
[We will / We will not / We have chosen to...]

**Explanation:**
[Why this decision? What alternatives were considered and why were they ruled
out? This section should be long enough that someone who wasn't in the room
can understand not just what was decided, but why.]

### Option A: [Name of chosen option]
**Description:** [What this option entails]
**Pros:**
- [Specific advantage — not generic]
- [Specific advantage]

**Cons:**
- [Specific cost or risk — not generic]
- [Specific cost or risk]

**Why chosen / not chosen:** [One paragraph explaining the weight of evidence
for or against this option]

### Option B: [Name of alternative]
**Description:** [What this option entails]
**Pros:**
- [Specific advantage]

**Cons:**
- [Specific cost or risk]

**Why not chosen:** [One paragraph]

### Option C: [Name of another alternative, if applicable]
[Same structure]

---

## Consequences

*What are the expected results of this decision? Be honest about both the
benefits and the costs. An ADR that only lists benefits was not reviewed
seriously.*

**Expected benefits:**
- [Specific, measurable where possible]
- [Specific, measurable where possible]

**Known costs and trade-offs:**
- [What we give up by making this choice]
- [What this decision makes harder or more expensive]

**Risks:**
- [What could go wrong]
- [What assumptions could turn out to be wrong]
- [Mitigation for each risk]

**Follow-on decisions required:**
[List any architecture decisions that this decision makes necessary or that
should be made next. This creates the chain of decisions that forms a complete
architecture.]

---

## Governance Implications

*Every architecture decision has governance implications. Document them here
so they don't get skipped.*

**Data ownership:** [Who owns the data managed by or produced by this
architecture component?]

**Access control:** [How will access to data in this architecture be managed?
What roles, what policies, what enforcement mechanism?]

**Data quality:** [What quality standards apply? Where are they enforced?
Who is responsible for monitoring?]

**Lineage:** [How will data lineage be captured and maintained for data
flowing through this architecture?]

**Regulatory considerations:** [What regulations apply to the data handled
by this architecture? How does this decision support compliance?]

---

## Implementation Notes

*High-level implementation guidance to ensure the intent of the decision is
carried through. Not a project plan — a set of principles and constraints
for the engineering team.*

**Critical implementation principles:**
- [Non-negotiable design requirement]
- [Non-negotiable design requirement]

**What must not be compromised:**
- [Hard constraints on implementation]

**Acceptable shortcuts during implementation:**
- [If there are tactical compromises acceptable in the short term, name them
  and set a deadline for resolving them]

**Architecture review points:**
[Define the checkpoints at which architecture review is required during
implementation — e.g., "before ingestion pipelines are built," "before
Gold layer is opened to business users"]

---

## Evaluation Criteria

*How will we know if this decision was the right one? Define this before
implementation, not after.*

**Success measures:**
- [Measurable outcome — "Query p95 latency under 30 seconds at 500 concurrent users"]
- [Measurable outcome]

**Review date:**
[When will this decision be formally reviewed against the success measures?
Recommended: 6 months after production go-live, and annually thereafter.]

**Conditions for revisiting:**
[What circumstances would cause this decision to be revisited before the
review date? e.g., "Volume exceeds 3x current baseline," "Regulatory
requirements change," "Acquiring a business unit that uses a different platform"]

---

## Approvals

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Data Architect | | | |
| CDO / Architecture Lead | | | |
| Business Owner (primary domain) | | | |
| Engineering Lead | | | |
| Governance / Compliance (if applicable) | | | |

---

## Change Log

| Date | Change | Author |
|------|--------|--------|
| [YYYY-MM-DD] | Initial draft | [Name] |
| | | |

---

*This template is part of the Harveer Singh Data Architecture Framework.
ADRs should be stored in version control alongside the architecture they
document. A decision that isn't documented isn't a decision — it's a rumor.*
