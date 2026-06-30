# Architecture Assessment Framework
## Harveer Singh | Data Architecture Framework

---

## 35-Question Assessment

Five dimensions. Seven questions each. Score each question 0–4:
- 0 = Not in place / doesn't exist
- 1 = Ad hoc / informal / exists in pockets
- 2 = Partially implemented / inconsistent
- 3 = Implemented / consistent with gaps
- 4 = Fully implemented / measured / continuously improved

Maximum dimension score: 28. Maximum total: 140.
**Scale to 0–20 for reporting** (divide by 1.4).
**Scale to 0–100 total** (divide by 1.4).

---

### Dimension 1: Current State (What Have We Got?)

**Q1. Data Inventory**
Can you produce a complete, current inventory of all data assets in production?
- 0: No inventory exists; discovery is tribal knowledge
- 1: Informal lists exist in spreadsheets or email; incomplete
- 2: A catalog exists for part of the estate; coverage is below 50%
- 3: A catalog covers most assets (50–80%); not always current
- 4: A managed catalog covers 80%+ of assets; updated automatically

**Q2. Architecture Documentation**
Is the current data architecture documented accurately?
- 0: No documentation exists or it's years out of date
- 1: Diagrams exist but are incomplete or inaccurate
- 2: Architecture is documented for major systems; not for all
- 3: Architecture documentation exists and is reviewed periodically
- 4: Architecture documentation is current, version-controlled, and
  reviewed quarterly

**Q3. Source System Knowledge**
Do you know what every source system produces, at what frequency, and at
what quality?
- 0: No. Source system behavior is discovered when something breaks.
- 1: Known for critical systems; unknown for many others
- 2: Most source systems are documented; some gaps
- 3: All major source systems documented; minor systems may have gaps
- 4: Complete source system catalog with schema, SLAs, quality profiles

**Q4. Data Volume and Growth**
Do you know current data volumes and growth trajectories?
- 0: Unknown
- 1: Known roughly; no growth projections
- 2: Known for primary systems; growth tracking informal
- 3: Volume tracked; growth projections exist for major systems
- 4: Volumes tracked, projected, and used to drive capacity planning

**Q5. Data Duplication**
Do you know how many copies of the same data exist, where, and why?
- 0: No idea; suspected to be significant
- 1: Known anecdotally; not formally measured
- 2: Partially mapped; known problem areas identified
- 3: Duplication mapped for primary domains; reduction in progress
- 4: Duplication is tracked and managed; single-source targets are enforced

**Q6. Technical Debt**
Do you have a documented, prioritized list of architecture technical debt?
- 0: Not documented; known to be significant
- 1: Informal awareness; no formal tracking
- 2: Some debt documented; prioritization informal
- 3: Debt tracked; prioritized; addressed opportunistically
- 4: Debt formally tracked, prioritized, resourced, and regularly reviewed

**Q7. Architecture Ownership**
Is there a named person or team accountable for data architecture decisions?
- 0: No clear ownership; decisions made ad hoc
- 1: Informal ownership; no formal accountability
- 2: Ownership exists for some systems; gaps elsewhere
- 3: Architecture ownership defined; decision process established
- 4: Architecture function is established, empowered, and consistently engaged

---

### Dimension 2: Governance (Who's in Charge of What?)

**Q8. Data Ownership**
Does every major dataset have a named business owner accountable for its
accuracy, completeness, and appropriate use?
- 0: No business ownership; data is "IT's problem"
- 1: Ownership exists for some high-profile datasets
- 2: Ownership defined for primary datasets; gaps in others
- 3: Ownership defined broadly; accountability is real in most cases
- 4: Ownership is comprehensive, documented, and enforced

**Q9. Data Definitions**
Are critical business terms (customer, revenue, product, etc.) defined in a
business glossary that everyone agrees on?
- 0: No glossary; multiple conflicting definitions in use
- 1: Informal definitions exist; not universally agreed
- 2: Glossary exists for some terms; not comprehensive
- 3: Business glossary covers primary domains; actively maintained
- 4: Comprehensive, governed glossary; new terms require formal definition

**Q10. Access Control**
Is access to data managed by a documented, enforced policy?
- 0: Ad hoc; access decisions made informally
- 1: Policies exist on paper; enforcement is inconsistent
- 2: Access control implemented for sensitive data; gaps elsewhere
- 3: Role-based access control in place broadly; periodic review occurs
- 4: Policy-driven, automated access control; access is certified regularly

**Q11. Data Quality Standards**
Are there defined, measured data quality standards for critical datasets?
- 0: No quality standards; quality is assumed
- 1: Quality concerns are known but not formally measured
- 2: Quality rules exist for some datasets; measurement is partial
- 3: Quality measured for primary datasets; results visible to owners
- 4: Comprehensive quality monitoring; SLAs defined; violations trigger action

**Q12. Data Lineage**
Can you trace any critical data element from its source to its consumption?
- 0: No lineage; tracing requires manual investigation
- 1: Lineage exists for some critical paths; not systematic
- 2: Lineage partially implemented; coverage below 50%
- 3: Lineage covers most critical paths; gaps in some areas
- 4: End-to-end lineage automated; available on demand for all assets

**Q13. Regulatory and Compliance Governance**
Is your data governance model aligned with applicable regulations (privacy,
financial, industry-specific)?
- 0: Not formally aligned; compliance is reactive
- 1: Known requirements; alignment is informal
- 2: Compliance controls exist for primary regulations; gaps present
- 3: Formal compliance program in place; periodic audit occurs
- 4: Compliance is automated, continuously monitored, audit-ready

**Q14. Governance Operating Model**
Is there a functioning governance body (council, committee, or equivalent) that
makes and enforces data governance decisions?
- 0: No governance body
- 1: A governance group exists on paper; rarely meets or decides
- 2: Governance body meets; decisions are made but not always enforced
- 3: Governance body is active and effective for primary decisions
- 4: Governance body is authoritative, consistent, and cross-functional

---

### Dimension 3: Integration (How Does Data Move?)

**Q15. Integration Inventory**
Do you have a complete map of all integration points between systems?
- 0: No map; integrations are discovered when they break
- 1: Major integrations known; many undocumented
- 2: Integration inventory exists; below 70% coverage
- 3: Most integrations documented; maintained imperfectly
- 4: Complete, current integration map; maintained in architecture tooling

**Q16. Integration Standards**
Are integration patterns standardized (API, CDC, event stream, batch)?
- 0: Every integration is custom; no standards
- 1: Some preferred patterns; inconsistently applied
- 2: Standards exist; partially adopted
- 3: Standards broadly adopted; exceptions require justification
- 4: Consistent integration patterns enforced; non-standard integrations
  are rare and justified

**Q17. Data Contracts**
Do source systems operate under formal data contracts (schema, quality, SLA)?
- 0: No contracts; source systems change without notice
- 1: Informal agreements with some sources
- 2: Contracts in place for critical integrations
- 3: Contracts broadly adopted; violations are tracked
- 4: Formal data contracts for all production integrations; automated monitoring

**Q18. Integration Resilience**
Are integrations designed to handle source system failures without cascading
failure?
- 0: Failures cascade; integrations are fragile
- 1: Some error handling; many failure modes untested
- 2: Resilience built for critical integrations
- 3: Most integrations handle common failure modes
- 4: Resilience patterns applied consistently; failure scenarios tested

**Q19. Point-to-Point Integration**
Is point-to-point integration controlled and declining?
- 0: Proliferating; spaghetti integration is the primary model
- 1: Known problem; not being addressed
- 2: Reduction plan exists; partially implemented
- 3: Actively reducing; hub or event-based integration replacing P2P
- 4: P2P integration is rare, governed, and declining

**Q20. Real-Time Capability**
Do you have the capability to move data in real-time or near-real-time
where the business requires it?
- 0: No real-time capability; everything is batch
- 1: Informal real-time solutions exist; not managed
- 2: Real-time capability exists for some use cases
- 3: Real-time capability available and used where appropriate
- 4: Real-time and batch integration are both mature, managed, and
  appropriately allocated by use case

**Q21. Master Data Management**
Are critical entities (customer, product, location) managed with a single,
authoritative source of truth?
- 0: No MDM; each system has its own version of shared entities
- 1: MDM recognized as a problem; no formal program
- 2: MDM in place for one or two entities
- 3: MDM covers primary entities; golden record enforced in some domains
- 4: Comprehensive MDM; golden records enforced across the estate

---

### Dimension 4: Performance (Does It Work at Scale?)

**Q22. Query Performance**
Do business users get query results within acceptable timeframes?
- 0: Frequent complaints; hours-long queries common
- 1: Performance acceptable for some workloads; major issues elsewhere
- 2: Performance managed for critical workloads; secondary workloads lag
- 3: Most workloads within SLA; optimization is ongoing
- 4: SLAs defined, measured, and met; degradation triggers investigation

**Q23. Ingestion Performance**
Can you ingest data at the rate the business requires without backlog buildup?
- 0: Ingestion frequently backlogs; data is late routinely
- 1: Ingestion keeps up under normal conditions; degrades under load
- 2: Ingestion capacity is adequate with headroom for moderate growth
- 3: Ingestion capacity managed proactively; growth projected and planned
- 4: Ingestion at scale; auto-scaling or proactive capacity management

**Q24. Cost Management**
Is the cost of data infrastructure understood, tracked, and managed?
- 0: Costs unknown or untracked
- 1: Total costs known; not broken down by workload or domain
- 2: Cost visibility improving; some attribution in place
- 3: Cost tracked by domain or workload; optimization is active
- 4: Full cost attribution; optimization embedded in architecture decisions

**Q25. Monitoring and Observability**
Is the data platform monitored so that problems are caught before users
report them?
- 0: No monitoring; users are the detection mechanism
- 1: Basic infrastructure monitoring; data pipeline monitoring absent
- 2: Pipeline monitoring in place for critical paths
- 3: Comprehensive monitoring; alerts go to owners before users notice
- 4: Full observability; anomaly detection; SLA tracking automated

**Q26. Disaster Recovery and Continuity**
Is the data platform designed to recover from failure within an acceptable
timeframe?
- 0: No formal DR; recovery would take days to weeks
- 1: Backup exists; recovery process not tested
- 2: DR plan exists; tested intermittently
- 3: DR tested regularly; RTO/RPO defined and achievable
- 4: DR automated; RTO/RPO tested and met; business continuity assured

**Q27. Performance Scalability**
Can the platform scale to 10x current load without fundamental redesign?
- 0: At or near capacity; scaling would require rebuild
- 1: Some headroom; scaling beyond 2x would be difficult
- 2: Architecture can scale moderately; some components would need work
- 3: Clear scaling path exists; primary bottlenecks identified
- 4: Architecture designed for scale; horizontal scaling available where needed

**Q28. Data Freshness**
Is data available to consumers within the freshness window the business
requires?
- 0: Data is routinely late; freshness windows consistently missed
- 1: Freshness acceptable for some use cases; missed for others
- 2: Freshness managed for primary use cases; secondary use cases lag
- 3: Freshness SLAs defined for most use cases; met most of the time
- 4: Freshness SLAs defined, measured, and met; violations trigger action

---

### Dimension 5: Future Readiness (Can We Evolve?)

**Q29. Cloud Readiness**
Is the architecture designed to leverage cloud capabilities (elasticity,
managed services, global distribution)?
- 0: On-premises only; no cloud strategy
- 1: Cloud strategy exists; adoption is minimal
- 2: Cloud adoption underway; hybrid architecture in progress
- 3: Cloud-first for new workloads; legacy migration planned
- 4: Cloud-native architecture; on-premises is the exception

**Q30. AI and ML Readiness**
Is the data estate structured to support AI and ML workloads (training data,
feature stores, model serving)?
- 0: No consideration for AI/ML data requirements
- 1: AI/ML discussed; data infrastructure not prepared
- 2: Some AI/ML infrastructure in place; not systematically designed
- 3: AI/ML data requirements addressed in architecture; active programs
- 4: Architecture explicitly designed for AI/ML; feature store, training
  data management, model registry in place

**Q31. Self-Service Capability**
Can business users find, access, and use data without requiring IT involvement
for routine requests?
- 0: All data access requires IT; no self-service
- 1: Limited self-service for a small user population
- 2: Self-service available for standard reporting; custom access requires IT
- 3: Broad self-service capability; IT involvement limited to exceptions
- 4: Governed self-service at scale; users are empowered; access is audited

**Q32. Architecture Agility**
Can the architecture absorb new data sources, new use cases, and new
consumers without major rework?
- 0: Every new requirement requires significant architecture work
- 1: Architecture changes frequently required; not designed for change
- 2: New sources and use cases can be added; some structural constraints
- 3: Architecture designed for extensibility; most changes are routine
- 4: Highly extensible; new sources, use cases, and consumers added rapidly

**Q33. Data Democratization**
Is data accessible to the people who need it, not just the people with
technical access?
- 0: Data is accessible only to technical staff
- 1: Access is expanding but limited; many business users cannot get data
- 2: Business users have access to curated datasets; raw data inaccessible
- 3: Data is broadly accessible; literacy programs support usage
- 4: Data is genuinely democratized; literacy, access, and tools aligned

**Q34. Technology Currency**
Is the data platform on supported, current technology versions?
- 0: Multiple systems on end-of-life versions; significant upgrade debt
- 1: Some systems current; others significantly behind
- 2: Most systems current; a few legacy exceptions
- 3: Currency managed proactively; upgrade plan in place for exceptions
- 4: All systems current; upgrade cadence is managed as routine

**Q35. Architecture Roadmap**
Is there a documented, resourced architecture roadmap for the next 2–3 years?
- 0: No roadmap
- 1: High-level roadmap exists; not detailed or resourced
- 2: Roadmap exists; partially resourced; may not reflect current priorities
- 3: Active roadmap; resourced; reviewed and updated periodically
- 4: Comprehensive roadmap; resourced; quarterly review; aligned with business

---

## Scoring and Maturity Levels

### Score Calculation
1. Total raw score: sum all 35 questions (max 140)
2. Scale to 100: (raw score / 140) × 100
3. Dimension scores: sum 7 questions per dimension (max 28), scale to 20

### Maturity Levels

| Score | Maturity Level | What It Means |
|-------|----------------|---------------|
| 0–20 | **Foundational** | Architecture is ad hoc. Significant investment needed before scaling is possible. Immediate risks to operations and compliance. |
| 21–40 | **Developing** | Progress visible in pockets. Architecture decisions are being made but not systematically. Governance gaps create daily operational friction. |
| 41–60 | **Established** | Core architecture is functional. Governance exists but is inconsistent. Scaling is possible but constrained by debt. |
| 61–80 | **Advanced** | Architecture is intentional and managed. Most dimensions are working. Optimization and future-readiness are the focus. |
| 81–100 | **Optimized** | Architecture is a genuine business asset. Continuously improved. Governance, performance, and agility are all strong. |

---

## Architecture Debt Identification

Architecture debt is the cumulative cost of architecture decisions that were
correct for their time but are now constraints. Unlike technical debt (code
quality), architecture debt is structural — it affects how data moves, where
it lives, and who can use it.

**High-priority debt (address in 0–6 months):**
- Any Q with score 0 in Governance or Compliance dimensions
- Any Q with score 0 in Performance that is causing active operational issues
- Integration patterns that are creating cascading failures

**Medium-priority debt (address in 6–18 months):**
- Consistent scores of 1–2 across an entire dimension
- Point-to-point integration proliferation (Q19 score below 2)
- No real-time capability where business uses cases require it (Q20 score 0)

**Long-term debt (address in 18+ months):**
- Legacy technology currency issues (Q34) that don't have immediate operational impact
- Self-service gaps (Q31) that limit but don't block business operations
- AI/ML readiness gaps (Q30) if AI programs are not yet active

---

## Architecture Smells

Architecture smells are signs that something is wrong — not conclusive proof,
but signals that warrant investigation.

### Smell 1: The Invisible Architecture
No one can draw the current architecture accurately on a whiteboard. Every
attempt reveals that people have different mental models of how data flows.
**Signal:** Q2 score below 2 or inconsistent answers about current state.
**Risk:** Decisions are being made based on an architecture that doesn't exist
as described.

### Smell 2: Data as IT Property
Business users refer to data as "IT's data" or "the IT team's problem."
Business ownership of data is theoretical.
**Signal:** Q8 score below 2. Business stakeholders can't name the owner of
datasets they use daily.
**Risk:** Quality problems are never resolved because the people who can fix
them have no accountability.

### Smell 3: The Discovery Gap
Finding data requires knowing who to ask. New team members spend months
learning where data lives.
**Signal:** Q1 score below 2. No catalog, or catalog coverage below 30%.
**Risk:** Duplicate datasets proliferate; analysis is built on the wrong data.

### Smell 4: Integration Archaeology
When a source system needs to change, it takes weeks to understand what
depends on it.
**Signal:** Q15 score below 2. Integration map is incomplete.
**Risk:** Changes in source systems cause unplanned downstream failures.

### Smell 5: Governance by Spreadsheet
Access requests, data definitions, and quality issues are tracked in
spreadsheets maintained by one or two people.
**Signal:** Q10, Q14 scores below 2.
**Risk:** Governance doesn't scale. The spreadsheet owners become bottlenecks
and single points of failure.

### Smell 6: The Infinite ETL Queue
The team is perpetually backlogged with data pipeline requests. New data
takes weeks or months to reach consumers.
**Signal:** Q23 score below 2. Ingestion pipeline is a constant constraint.
**Risk:** The data team becomes the bottleneck for all data-driven decisions.

### Smell 7: Everyone Has Their Own Copy
Business teams maintain their own copies of data in Excel files, local
databases, or personal workspaces because they don't trust the official source.
**Signal:** Q5 score below 2. Q11 score below 2. Q31 score below 2.
**Risk:** Inconsistent numbers in business decisions. Governance is impossible
when data is distributed across unmanaged copies.

### Smell 8: The Mystery Query
A query runs for hours and no one can explain why. Performance investigation
reveals architecture decisions made years ago that nobody remembers making.
**Signal:** Q22, Q25 scores below 2.
**Risk:** Platform performance degrades unpredictably; business users lose
confidence in the platform.

### Smell 9: Compliance by Heroics
Regulatory deadlines are met by individual heroic efforts rather than
systematic processes.
**Signal:** Q13 score below 2. Compliance activities spike before audits.
**Risk:** One person's departure or one missed deadline creates a compliance
crisis.

### Smell 10: The Architecture That Nobody Uses
A formal architecture review process exists, but teams bypass it because it's
slow, bureaucratic, or irrelevant.
**Signal:** Q7 score below 2. Architecture decisions are made in projects
without architecture involvement.
**Risk:** Architecture diverges from design; debt accumulates faster than
it can be documented.
