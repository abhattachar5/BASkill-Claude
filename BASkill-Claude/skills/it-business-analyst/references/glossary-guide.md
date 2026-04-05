# Glossary & Acronym Manager Guide

Every BA deliverable in insurance/financial services needs a glossary. Domain jargon, acronyms, and technical terms create barriers to understanding — especially when documents cross between business, technology, actuarial, and compliance audiences. This guide covers how to build, maintain, and auto-generate glossaries.

## Table of Contents
1. [Auto-Generating Glossaries from Documents](#auto-generating-glossaries-from-documents)
2. [Standard Glossary Format](#standard-glossary-format)
3. [Insurance & Reinsurance Core Glossary](#insurance--reinsurance-core-glossary)
4. [Technology & Architecture Glossary](#technology--architecture-glossary)
5. [Regulatory Glossary](#regulatory-glossary)
6. [Quality Checklist](#quality-checklist)

---

## Auto-Generating Glossaries from Documents

When the user uploads documents or provides content, automatically scan for terms that need defining. Follow this process:

### Step 1: Identify glossary candidates
Scan the document for:
- **Acronyms**: Any uppercase sequence of 2+ letters (e.g., STP, IBNR, FNOL, API)
- **Domain terms**: Insurance-specific terminology that non-specialists might not know
- **Technical terms**: System names, architecture patterns, tool names
- **Project-specific terms**: Programme names, workstream names, custom terminology
- **Ambiguous terms**: Words that have different meanings in different contexts (e.g., "cover" in insurance vs general English)

### Step 2: Check against the core glossaries below
If a term appears in the core glossaries in this guide, use the standard definition. If the document uses the term differently, note the project-specific usage alongside the standard definition.

### Step 3: Produce the glossary
Include in every deliverable — either as a section at the end of the document (for .docx) or as a separate sheet (for .xlsx).

### Step 4: Maintain across deliverables
When producing multiple documents for the same programme, maintain a single master glossary and reference it. Add new terms as they emerge. Flag terms that are used inconsistently across documents.

---

## Standard Glossary Format

| Term | Acronym | Definition | Context / Usage | Related terms |
|---|---|---|---|---|
| Straight-Through Processing | STP | Fully automated end-to-end processing of a transaction without manual intervention | Underwriting: application assessed and decided automatically | Auto-decision, rules engine |
| Incurred But Not Reported | IBNR | Estimate of claims that have occurred but have not yet been reported to the insurer | Reserving: actuarial provision for unknown claims | Reserve, RBNS, ultimate loss |

---

## Insurance & Reinsurance Core Glossary

### Underwriting

| Term | Acronym | Definition |
|---|---|---|
| Underwriting | UW | The process of assessing and pricing risk for insurance applications |
| Sum Assured | SA | The maximum amount payable under the policy on a valid claim |
| Free Cover Limit | FCL | The maximum sum assured that can be accepted without individual medical underwriting (typically for group schemes) |
| Standard Rate | — | Acceptance at normal premium rates with no additional loading or exclusions |
| Substandard / Rated | — | Acceptance with additional premium loading due to increased risk |
| Exclusion | — | A clause that removes cover for a specific condition or circumstance |
| Decline | — | Refusal to offer insurance cover |
| Defer / Postpone | — | Decision to delay underwriting assessment (e.g., pending medical treatment outcome) |
| Moratorium | — | Underwriting approach where pre-existing conditions are excluded for a set period without individual medical questions |
| Full Medical Underwriting | FMU | Individual risk assessment based on medical evidence and questionnaires |
| Tele-underwriting | Tele-UW | Underwriting interview conducted by telephone, often by a trained nurse interviewer |
| Evidence | — | Medical, financial, or lifestyle information gathered to support underwriting decisions |
| GP Report | GPR | Medical report obtained from the applicant's General Practitioner |
| Non-disclosure | — | Failure by the applicant to disclose material information relevant to the risk assessment |
| Guaranteed Issue | GI | Cover offered without individual underwriting (typically group schemes below FCL) |
| Risk Appetite | — | The types and levels of risk an insurer is willing to accept |
| Straight-Through Processing | STP | Fully automated processing without manual intervention |
| Auto-decision | — | A risk decision made entirely by automated rules or AI without human underwriter involvement |

### Reinsurance

| Term | Acronym | Definition |
|---|---|---|
| Cedant / Ceding Company | — | The primary insurer that transfers (cedes) risk to a reinsurer |
| Reinsurer | — | Company that accepts risk from a cedant |
| Treaty | — | Reinsurance agreement covering a defined portfolio of risks automatically |
| Facultative | Fac | Reinsurance arranged on an individual risk basis (case by case) |
| Retrocession | Retro | Reinsurance purchased by a reinsurer (reinsurance of reinsurance) |
| Cession | — | The portion of risk transferred to the reinsurer |
| Retention | — | The portion of risk retained by the cedant |
| Bordereaux | — | Periodic report from cedant to reinsurer listing individual risks or claims |
| Quota Share | QS | Treaty where cedant cedes a fixed percentage of every risk |
| Surplus | — | Treaty where cedant cedes the amount above their retention |
| Excess of Loss | XoL | Treaty where reinsurer pays claims above a specified threshold |
| Loss Ratio | LR | Claims paid as a percentage of premiums earned |
| Combined Ratio | CR | Loss ratio + expense ratio — below 100% indicates underwriting profit |

### Claims

| Term | Acronym | Definition |
|---|---|---|
| First Notification of Loss | FNOL | Initial report of a claim event to the insurer |
| Incurred But Not Reported | IBNR | Actuarial estimate of claims that have occurred but not yet been reported |
| Reported But Not Settled | RBNS | Claims reported but not yet fully settled |
| Reserve | — | Amount set aside for expected claim payments |
| Ex-gratia | — | Payment made without admission of liability, as a gesture of goodwill |
| Subrogation | — | Right of insurer to pursue third parties who caused the loss |
| Claimant | — | Person making the claim |

### Policy Administration

| Term | Acronym | Definition |
|---|---|---|
| Inception | — | Start date of the insurance policy |
| Mid-Term Adjustment | MTA | Change to policy terms during the policy period |
| Lapse | — | Policy termination due to non-payment of premium |
| Surrender | — | Voluntary termination of a policy by the policyholder (may have surrender value) |
| Cooling-off Period | — | Period after policy inception during which the customer can cancel without penalty (typically 30 days) |
| Premium | — | Amount paid by the policyholder for insurance cover |

---

## Technology & Architecture Glossary

| Term | Acronym | Definition |
|---|---|---|
| Application Programming Interface | API | Interface for system-to-system communication |
| Representational State Transfer | REST | Architectural style for web APIs using HTTP methods |
| Extract, Transform, Load | ETL | Data pipeline pattern for moving data between systems |
| Straight-Through Processing | STP | See underwriting glossary — same concept applied to technology |
| Optical Character Recognition | OCR | Technology to extract text from images or scanned documents |
| Natural Language Processing | NLP | AI techniques for understanding and processing human language |
| Large Language Model | LLM | AI model trained on large text corpora for language understanding and generation |
| Ontology | — | Structured representation of domain knowledge as entities, relationships, and rules |
| Decision Engine | — | Rules-based system that evaluates inputs against business rules to produce decisions |
| Orchestration | — | Coordination of multiple services or components to execute a workflow |
| Data Fabric | — | Architecture for unified data access across distributed sources |
| Service Level Agreement | SLA | Agreed performance targets (response time, availability, throughput) |
| Recovery Point Objective | RPO | Maximum acceptable data loss measured in time |
| Recovery Time Objective | RTO | Maximum acceptable downtime after a failure |

---

## Regulatory Glossary

| Term | Acronym | Definition |
|---|---|---|
| Solvency II | S2 | EU/UK regulatory framework for insurance capital requirements and risk management |
| Solvency Capital Requirement | SCR | Capital an insurer must hold to absorb significant unexpected losses |
| Minimum Capital Requirement | MCR | Minimum capital threshold below which regulatory intervention is triggered |
| Own Risk and Solvency Assessment | ORSA | Insurer's own assessment of its risk profile and capital adequacy |
| Insurance Distribution Directive | IDD | EU directive governing insurance distribution and sales practices |
| Insurance Product Information Document | IPID | Standardised pre-sale product summary required under IDD |
| Product Oversight and Governance | POG | IDD requirement for manufacturers and distributors to have product governance processes |
| General Data Protection Regulation | GDPR | EU/UK regulation governing personal data processing |
| Data Protection Impact Assessment | DPIA | Assessment required before processing personal data that poses high risk |
| Record of Processing Activities | ROPA | Register of all personal data processing activities (GDPR Art. 30) |
| Financial Conduct Authority | FCA | UK financial services regulator for conduct and consumer protection |
| Prudential Regulation Authority | PRA | UK regulator for financial soundness of insurers and banks |
| Consumer Duty | CD | FCA regulation requiring firms to deliver good outcomes for retail customers |
| Senior Managers and Certification Regime | SMCR | FCA/PRA regime for individual accountability in financial services |

---

## Quality Checklist

- [ ] Glossary covers all acronyms used in the document
- [ ] Definitions are written for the target audience (business-friendly, not overly technical)
- [ ] Insurance-specific terms are included (don't assume the reader knows "cedant" or "IBNR")
- [ ] Project-specific terms and system names are defined
- [ ] Terms are used consistently throughout the document (same term = same meaning everywhere)
- [ ] Ambiguous terms have context-specific clarification
- [ ] Regulatory acronyms include the full regulation name and brief scope
- [ ] Glossary is sorted alphabetically for easy reference
- [ ] Cross-references to related terms are included where helpful
