# Estimation Support Guide

BAs are frequently involved in estimation — sizing user stories, scoring complexity for prioritisation, and providing T-shirt estimates for roadmap planning. This guide covers practical estimation frameworks for insurance/financial services IT programmes.

## Table of Contents
1. [Story Point Estimation](#story-point-estimation)
2. [T-Shirt Sizing](#t-shirt-sizing)
3. [Complexity Scoring](#complexity-scoring)
4. [Insurance-Specific Complexity Factors](#insurance-specific-complexity-factors)
5. [Estimation Output Formats](#estimation-output-formats)
6. [Quality Checklist](#quality-checklist)

---

## Story Point Estimation

Story points measure relative effort, not absolute time. They capture complexity, uncertainty, and volume of work.

### Modified Fibonacci scale

| Points | Relative effort | Typical characteristics |
|---|---|---|
| 1 | Trivial | Config change, text update, single-field addition |
| 2 | Small | Simple CRUD, straightforward UI change, single validation rule |
| 3 | Moderate | Multi-field form, simple business rule, single integration touchpoint |
| 5 | Medium | Complex business logic, multiple validation rules, UI with conditional behaviour |
| 8 | Large | Multi-system integration, complex business rules with edge cases, significant data transformation |
| 13 | Very large | Major feature with multiple integration points, complex data migration, new workflow engine |
| 21 | Epic-sized | Should be decomposed further — too large for a single sprint |

### Estimation dimensions

When estimating, consider all three dimensions — not just coding effort:

| Dimension | What to assess |
|---|---|
| **Complexity** | How intricate is the logic? How many business rules, edge cases, conditional paths? |
| **Uncertainty** | How well understood is the requirement? Are there unknowns or dependencies on external teams? |
| **Volume** | How much work is there even if it's straightforward? (e.g., mapping 200 fields is high volume but low complexity) |

### Reference stories

Establish reference stories that the team agrees on — anchor points for relative estimation:

| Reference story | Points | Why |
|---|---|---|
| "Add a new read-only field to the applicant summary screen" | 2 | Simple, well-understood, no business logic |
| "Implement smoking status validation with cessation date logic" | 5 | Moderate business logic, enum mapping, conditional validation |
| "Integrate with GP Connect API to retrieve medical records" | 8 | External API, error handling, data transformation, security |
| "Build the hybrid decisioning pipeline (deterministic → AI fallback)" | 21 | Multi-component, complex orchestration — needs decomposition |

---

## T-Shirt Sizing

T-shirt sizing is used for roadmap-level estimation when story points are too granular.

### Scale

| Size | Typical effort | Sprint equivalent | Characteristics |
|---|---|---|---|
| **XS** | < 1 person-day | Fraction of a sprint | Config, minor change, defect fix |
| **S** | 1-3 person-days | < half a sprint | Simple feature, single component, clear requirements |
| **M** | 3-8 person-days | Half to one sprint | Multi-component feature, some integration, moderate complexity |
| **L** | 8-20 person-days | 1-2 sprints | Cross-system feature, significant business logic, multiple stories |
| **XL** | 20-40 person-days | 2-4 sprints | Major capability, multiple integration points, data migration element |
| **XXL** | 40+ person-days | 4+ sprints | Programme-level initiative — decompose into L/XL chunks |

### T-shirt sizing for epics

When sizing epics for roadmap planning, use a structured assessment:

| Epic | Scope indicators | Integration complexity | Data complexity | UW/Business rule complexity | Uncertainty | Size |
|---|---|---|---|---|---|---|
| Evidence Extraction (Rapid Doc AI) | 3 document types, OCR + NLP | Azure AI services, evidence vault | Unstructured → structured, 6-primitive mapping | Extraction confidence rules | Medium — AI accuracy uncertain | XL |
| SLA Monitoring & Escalation | Timers, alerts, escalation rules | UCM Next, notification service | Minimal — config-driven | Escalation thresholds, working hours | Low — well-understood pattern | M |

---

## Complexity Scoring

For prioritisation and capacity planning, score requirements on multiple dimensions:

### Complexity scorecard

Rate each dimension 1-5 and sum for total complexity score:

| Dimension | 1 (Low) | 3 (Medium) | 5 (High) |
|---|---|---|---|
| **Business rules** | Simple, few rules | Moderate, conditional logic | Complex, multi-factor, edge cases |
| **Data** | Single entity, standard types | Multiple entities, transformations | Complex model, migration, data quality issues |
| **Integration** | None or single internal API | 2-3 systems, standard protocols | Multiple external systems, real-time + batch, security |
| **UI/UX** | No UI or simple display | Forms with validation | Complex workflow UI, conditional rendering, accessibility |
| **Regulatory** | No regulatory impact | Standard compliance (GDPR, data retention) | Direct regulatory requirement, audit evidence needed |
| **Testing** | Straightforward happy path | Multiple scenarios, edge cases | Complex test data setup, integration testing, performance |
| **Uncertainty** | Fully understood, done before | Some unknowns, new tech | Significant unknowns, R&D element, external dependencies |

**Score ranges:**
- 7-14: Low complexity → S/M sizing, straightforward delivery
- 15-24: Medium complexity → M/L sizing, needs careful planning
- 25-35: High complexity → L/XL sizing, consider decomposition or spike first

---

## Insurance-Specific Complexity Factors

Insurance programmes have complexity drivers that generic frameworks miss:

| Factor | Why it adds complexity | Impact on estimate |
|---|---|---|
| **Multi-territory** | Different regulations, products, and business rules per market | Multiply by number of territories (not linearly — usually 1.3-1.5x per additional territory) |
| **Reinsurance layer** | Treaty terms, cession calculations, bordereaux reporting | Add 30-50% for features that touch reinsurance |
| **Actuarial involvement** | Pricing models, experience analysis, reserve calculations | Add uncertainty buffer — actuarial sign-off can be slow |
| **Regulatory sign-off** | Compliance review, legal review, regulatory notification | Add 2-4 weeks elapsed time for regulatory features |
| **Legacy integration** | Mainframe systems, batch files, non-standard formats | Add 50-100% for legacy integration vs modern API |
| **Medical data** | ICD-10 coding, medical terminology, clinical validation | Requires SME review — add time for UW/medical review cycles |
| **Multi-product** | Life, CI, IP, health — each has different rules | Multiply by product count (usually 1.2-1.4x per additional product) |
| **Audit trail** | Immutable logging, decision provenance, regulatory evidence | Add 20-30% for features requiring full audit trail |

---

## Estimation Output Formats

### Story-level estimates (Excel)

| Story ID | Title | Complexity score | Story points | Confidence | Assumptions | Risks |
|---|---|---|---|---|---|---|
| US-007 | Deterministic rules engine assessment | 24 | 8 | Medium | Magnum API available by Sprint 3 | API delay = blocker |
| US-008 | AI probabilistic fallback routing | 28 | 13 | Low | AI model performance meets threshold | May need additional sprint for tuning |

### Epic-level estimates (Excel)

| Epic | T-shirt size | Estimated sprints | Story count | Total story points | Key risks | Dependencies |
|---|---|---|---|---|---|---|
| EP-001 Evidence Extraction | XL | 3-4 | 8 | 45 | AI extraction accuracy | Azure AI Foundry provisioning |
| EP-003 Hybrid Decisioning | XL | 3-4 | 10 | 55 | Rule coverage completeness | Magnum API, ontology codification |

### Estimation confidence levels

Always state your confidence — an estimate without a confidence level is misleading:

| Level | Meaning | Typical accuracy | When to use |
|---|---|---|---|
| **High** | Well-understood, done similar before, clear requirements | ±20% | Detailed stories with acceptance criteria |
| **Medium** | Generally understood, some unknowns remain | ±40% | Epics with outline scope, stories pre-refinement |
| **Low** | Significant unknowns, new technology, unclear requirements | ±60% or more | Roadmap-level estimates, early-stage features |

---

## Quality Checklist

- [ ] Estimation scale is defined and reference stories are established
- [ ] All dimensions are considered (complexity, uncertainty, volume) — not just "how long to code"
- [ ] Insurance-specific complexity factors are accounted for (regulatory, multi-territory, reinsurance, legacy)
- [ ] Confidence level is stated for every estimate
- [ ] Assumptions behind the estimate are documented
- [ ] Risks that could blow the estimate are identified
- [ ] Estimates for large items (13+ points or XL+) include a recommendation to decompose
- [ ] Estimation is relative to team's reference stories, not absolute time
