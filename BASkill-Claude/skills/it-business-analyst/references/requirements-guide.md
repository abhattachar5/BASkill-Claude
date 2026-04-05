# Requirements Documentation Guide

This reference covers BRDs, FRDs, user stories, epics, themes, and acceptance criteria for insurance/financial services.

## Table of Contents
1. [BRD Structure](#brd-structure)
2. [FRD Structure](#frd-structure)
3. [Epics, Themes & User Stories](#epics-themes--user-stories)
4. [Acceptance Criteria](#acceptance-criteria)
5. [Requirements Catalogue](#requirements-catalogue)
6. [Insurance Domain Examples](#insurance-domain-examples)
7. [Quality Checklist](#quality-checklist)

---

## BRD Structure

A Business Requirements Document captures WHAT the business needs and WHY, without prescribing HOW. Use this structure:

### Document control
- Version, date, author, reviewers, approval status
- Change history table

### 1. Executive Summary
- 2-3 paragraphs: business problem, proposed solution direction, expected benefits
- Key metrics / success criteria (quantified where possible)

### 2. Business Context
- Current state overview
- Business drivers (regulatory, competitive, operational, strategic)
- Alignment to corporate strategy / programme objectives
- For insurance: reference relevant product lines, distribution channels, territories

### 3. Scope
- **In scope**: Explicitly list what's covered
- **Out of scope**: Explicitly list what's excluded (this prevents scope creep)
- **Future scope**: Items deferred to later phases

### 4. Stakeholders
- Stakeholder register table: Name, Role, Interest, Influence, Engagement level
- Reference RACI if one exists

### 5. Business Requirements
Structure each requirement as:

| Field | Description |
|---|---|
| **ID** | Unique identifier, e.g., BRD-001 |
| **Title** | Short descriptive name |
| **Description** | Clear statement of the business need |
| **Rationale** | Why this requirement exists |
| **Priority** | MoSCoW (Must/Should/Could/Won't) or numeric |
| **Source** | Who requested it / which workshop |
| **Acceptance criteria** | How we'll know it's met |
| **Dependencies** | Other requirements or external factors |
| **Regulatory link** | If driven by regulation, cite the specific rule |

### 6. Assumptions & Constraints
- Assumptions: things believed true but not yet confirmed
- Constraints: fixed boundaries (budget, timeline, technology, regulatory)

### 7. Dependencies & Risks
- Internal and external dependencies
- Key risks with likelihood, impact, and mitigation

### 8. Success Criteria & KPIs
- Measurable outcomes (e.g., "reduce underwriting turnaround from 5 days to 2 days")
- How and when they'll be measured

### 9. Glossary
- Define all domain terms, acronyms, and abbreviations

### Appendices
- Supporting data, process maps, workshop notes

---

## FRD Structure

A Functional Requirements Document specifies HOW the system should behave. It bridges business requirements to technical design.

### Document control
Same as BRD.

### 1. Introduction
- Purpose, audience, relationship to BRD (reference BRD version and ID)
- System/application context

### 2. Functional Requirements
Structure each requirement as:

| Field | Description |
|---|---|
| **ID** | e.g., FR-001 |
| **BRD trace** | Maps to BRD-XXX |
| **Title** | Short name |
| **Description** | Detailed functional behaviour |
| **Business rules** | Specific logic (if-then, calculations, validations) |
| **User interface** | Screen/field requirements if relevant |
| **Data requirements** | Inputs, outputs, data sources |
| **Error handling** | Expected error conditions and responses |
| **Priority** | MoSCoW |
| **Acceptance criteria** | Testable conditions |

### 3. Non-Functional Requirements
- Performance (response times, throughput, concurrency)
- Security & access control (role-based access, encryption, audit trail)
- Availability & disaster recovery (SLA, RPO, RTO)
- Data retention & archival (regulatory minimums)
- Integration requirements (APIs, file feeds, real-time vs batch)
- Regulatory / compliance requirements

### 4. Interface Requirements
- System interfaces (upstream/downstream systems)
- User interfaces (accessibility, browser support)
- Data interfaces (file formats, protocols, frequencies)

### 5. Data Requirements
- Data model overview or key entities
- Data migration requirements
- Data quality rules and validation

### 6. Assumptions, Constraints & Dependencies

### 7. Traceability Matrix
Table mapping FR → BRD → Epic/Story → Test Case

---

## Epics, Themes & User Stories

### Hierarchy

```
Theme (strategic goal)
  └── Epic (large body of work, typically spans multiple sprints)
       └── User Story (smallest unit of deliverable value)
            └── Acceptance Criteria (testable conditions)
                 └── Sub-tasks (implementation work items)
```

### Theme format
```
Theme: [Name]
Description: [Strategic objective this supports]
Business value: [Why this matters]
Epics: [List of child epics]
```

**Example:**
```
Theme: Digital Underwriting Transformation
Description: Modernise the life underwriting journey to enable straight-through 
processing for standard risks while maintaining risk quality.
Business value: Reduce new business processing time by 60%, improve customer 
experience, and reduce operational cost per policy.
Epics: E-Application, Automated Risk Assessment, Evidence Management, 
Decision Engine Modernisation
```

### Epic format
```
Epic: [ID] - [Name]
Theme: [Parent theme]
Description: [What this epic delivers]
Business value: [Measurable outcome]
Acceptance criteria: [High-level, epic-level conditions for "done"]
Stories: [List of child stories]
Estimated size: [T-shirt size or story points]
```

**Example:**
```
Epic: EP-003 - Automated Risk Assessment
Theme: Digital Underwriting Transformation
Description: Implement rules-based and AI-assisted risk assessment for life 
and CI applications, enabling auto-decision for standard risks.
Business value: 70% of standard risk applications decided within 2 minutes 
without manual underwriter intervention.
Acceptance criteria:
- Standard risk applications receive auto-decision within SLA
- All auto-decisions are auditable with full decision trail
- Fallback to manual review works seamlessly for complex cases
- Decision accuracy meets or exceeds current manual benchmarks
```

### User story format

Use the standard template:
```
[ID] As a [role], I want to [action], so that [benefit].
```

Write stories that are INVEST-compliant:
- **I**ndependent: can be developed and delivered on its own
- **N**egotiable: details can be discussed
- **V**aluable: delivers value to the user or business
- **E**stimable: team can estimate the effort
- **S**mall: fits within a sprint
- **T**estable: has clear acceptance criteria

**Insurance-specific roles to use:**
- Underwriter, Senior Underwriter, Chief Underwriter
- Claims Handler, Claims Manager
- Actuarial Analyst, Pricing Actuary
- Broker, Cedant, Client Relationship Manager
- Policy Administrator, Operations Manager
- Compliance Officer, Risk Manager
- Applicant, Policyholder, Claimant
- Distribution Partner, IFA (Independent Financial Adviser)

**Example:**
```
US-012: As an underwriter, I want to see a consolidated risk summary 
for the applicant including medical history, lifestyle factors, and 
financial data, so that I can make an informed decision without 
switching between multiple screens.

Acceptance Criteria:
Given an application has been submitted with medical evidence
When the underwriter opens the case in the workbench
Then they see a single-page risk summary showing:
  - Applicant demographics and sum assured
  - Medical conditions with severity and recency
  - Lifestyle risk factors (smoking, BMI, alcohol, occupation)
  - Financial justification status
  - Recommended decision with confidence score (if auto-assessed)
  - Link to full evidence documents
```

---

## Acceptance Criteria

Write acceptance criteria in Given-When-Then (Gherkin) format for testability:

```
Given [precondition / context]
When [action / trigger]
Then [expected outcome]
And [additional outcome if needed]
```

Rules for good acceptance criteria:
- Each criterion must be independently testable
- Use specific values, not vague terms ("within 3 seconds" not "quickly")
- Cover the happy path, edge cases, and error scenarios
- For insurance: include regulatory boundary conditions (e.g., cooling-off period, disclosure requirements)
- Number them: AC-1, AC-2, etc. within each story

**Anti-patterns to avoid:**
- "System should be user-friendly" → not testable
- "Data should be accurate" → define what accuracy means
- "Performance should be acceptable" → specify SLAs

---

## Requirements Catalogue

For large programmes, maintain a requirements catalogue in Excel with these columns:

| Column | Description |
|---|---|
| Req ID | Unique identifier |
| Type | Business / Functional / Non-Functional |
| Title | Short name |
| Description | Full requirement text |
| Priority | MoSCoW or numeric |
| Status | Draft / In Review / Approved / Implemented / Verified |
| Source | Stakeholder or workshop |
| BRD Ref | Traceability to BRD |
| Epic/Story | Traceability to backlog |
| Sprint | When it's planned |
| Owner | Who's responsible |
| Regulatory flag | Y/N with regulation reference |
| Notes | Additional context |

---

## Insurance Domain Examples

### Life & Health underwriting requirements
- Medical evidence ordering and retrieval (GP reports, blood tests, specialist reports)
- Tele-underwriting / tele-interview question sets
- Risk classification (standard, substandard, rated, declined, deferred, postponed)
- Reinsurance auto-facultative referral rules
- STP (straight-through processing) rules and thresholds
- Non-disclosure and claims repudiation logic

### Claims requirements
- First notification of loss (FNOL) capture
- Claims assessment workflow (medical, legal, financial)
- Reserve calculation and IBNR estimation
- Fraud detection and referral rules
- Rehabilitation and return-to-work programmes
- Reinsurance claims recovery and bordereaux reporting

### Policy administration
- New business, renewals, mid-term adjustments, cancellations
- Premium calculation and billing cycles
- Commission and clawback processing
- Regulatory reporting (Solvency II, ORSA, conduct MI)

---

## Quality Checklist

Before delivering any requirements document, verify:

- [ ] Every requirement has a unique, traceable ID
- [ ] Requirements use "shall" (mandatory) vs "should" (desirable) consistently
- [ ] Acceptance criteria are specific and testable
- [ ] Assumptions and constraints are explicitly stated
- [ ] Dependencies are identified with owners
- [ ] Insurance/regulatory implications are flagged
- [ ] Glossary includes all domain-specific terms
- [ ] Document control section is complete
- [ ] MoSCoW or priority is assigned to every requirement
- [ ] No solution design is embedded in business requirements (BRD stays solution-agnostic)
