# Source Ingestion & Synthesis Guide

BAs rarely start from a blank page. Requirements emerge from existing documentation, stakeholder conversations, and organisational knowledge. This guide covers how to ingest, analyse, and synthesise source materials into formal BA deliverables.

## Table of Contents
1. [Source Material Types](#source-material-types)
2. [Ingestion Workflow](#ingestion-workflow)
3. [Pattern 1: Existing Knowledge Base Documents](#pattern-1-existing-knowledge-base-documents)
4. [Pattern 2: Call Transcripts & Meeting Notes](#pattern-2-call-transcripts--meeting-notes)
5. [Pattern 3: Wiki Pages & Product Requirement Documents](#pattern-3-wiki-pages--product-requirement-documents)
6. [Cross-Referencing Multiple Sources](#cross-referencing-multiple-sources)
7. [Source Traceability](#source-traceability)
8. [Quality Checklist](#quality-checklist)

---

## Source Material Types

| Source type | Typical formats | What to extract | Common challenges |
|---|---|---|---|
| Functional specs / design docs | .docx, .pdf, PDF scans | Existing requirements, business rules, system behaviour, data models, interfaces | Outdated content, version ambiguity, undocumented changes since last update |
| Technical design documents | .docx, .pdf, wiki | Architecture decisions, integration points, API contracts, data flows | Technical jargon that needs translating to business language |
| Call transcripts | .txt, .docx, .pdf, audio transcription output | Stakeholder needs, pain points, process descriptions, decision rationale, action items | Rambling discussions, contradictory statements, implicit assumptions |
| Meeting / workshop notes | .docx, .txt, email, wiki | Decisions made, requirements discussed, open questions, agreed scope | Incomplete capture, missing context, varying levels of detail |
| Wiki pages (Confluence, SharePoint, Notion) | .html, .pdf, .docx exports, markdown | Product requirements, process documentation, architecture decisions, team agreements | Stale content, fragmented across pages, no clear ownership |
| PRDs (Product Requirements Documents) | .docx, .pdf, Google Docs export | Product vision, user personas, feature descriptions, success metrics, priorities | Product-level language that needs decomposing into functional requirements |
| Existing BRDs / FRDs from prior phases | .docx, .pdf | Baseline requirements, previously agreed scope, change history | Requirements that were specified but never implemented, or implemented differently |

---

## Ingestion Workflow

Every source ingestion follows this workflow regardless of source type:

### Step 1: Inventory and assess
Before extracting anything, catalogue what you've been given:

Produce a **Source Inventory Table** (in chat or as part of the output document):

| # | Document / Source | Type | Date / Version | Pages / Length | Relevance | Freshness | Notes |
|---|---|---|---|---|---|---|---|
| 1 | Claims Platform FSD v2.3 | Functional Spec | Mar 2024 | 48 pages | High — baseline for new requirements | 12 months old — verify currency | Covers claims FNOL and assessment |
| 2 | UW Transformation Workshop — 15 Jan call | Transcript | Jan 2025 | 45 min | High — stakeholder requirements | Current | Chief UW + Head of Ops present |
| 3 | Product Wiki — Group Life | Wiki export | Unknown | 12 pages | Medium — context only | Unknown — verify | May be outdated |

Flag: estimated staleness, missing version info, documents that contradict each other, and gaps (things you'd expect to see but haven't been provided).

### Step 2: Deep read and extract
Read each source and extract structured information. The extraction approach depends on the source type — see the patterns below.

### Step 3: Synthesise and cross-reference
Combine extractions across sources, resolve contradictions, and identify gaps. Produce a **Synthesis Summary** before writing the final deliverable.

### Step 4: Produce the deliverable
Write the BRD, FRD, user stories, or other output with full source traceability.

### Step 5: Flag gaps and questions
Always produce a **Questions & Gaps Log** — things that the source material didn't answer, contradictions that need stakeholder resolution, and assumptions you've made.

---

## Pattern 1: Existing Knowledge Base Documents

These are functional specifications, design documents, technical architecture docs, and prior BRDs/FRDs that represent the current "as-is" state or a previous phase's "to-be" that has since been implemented.

### What to extract

Read the document and extract into a structured table:

| Extract ID | Source doc | Section/Page | Category | Content | Status | Carry forward? |
|---|---|---|---|---|---|---|
| EXT-001 | Claims FSD v2.3 | §3.2, p14 | Business rule | "Claims under £5,000 are auto-approved if medical evidence is complete" | Implemented | Yes — baseline rule, verify current threshold |
| EXT-002 | Claims FSD v2.3 | §4.1, p22 | Integration | "FNOL data received via REST API from broker portal, batch file from legacy" | Implemented | Partially — REST yes, batch to be retired |
| EXT-003 | UW Design Doc v1.0 | §2.3, p8 | Data model | "Applicant entity holds 47 attributes including medical history array" | Implemented | Yes — extend for new fields |

### Categories to extract
- **Business rules**: If-then logic, thresholds, calculations, validation rules
- **Functional requirements**: System behaviours, screen flows, user interactions
- **Non-functional requirements**: Performance SLAs, security controls, availability targets
- **Integration points**: APIs, file feeds, upstream/downstream systems
- **Data model elements**: Key entities, attributes, relationships
- **Process steps**: Workflow stages, routing rules, exception handling
- **Assumptions from prior phase**: These may no longer hold — flag each for revalidation

### How to use in the new deliverable
- Existing requirements that still hold become the baseline — reference them by source doc and section, don't rewrite from scratch
- Changed requirements should show the delta: "Previously: [old], Now: [new], Reason: [why]"
- Retired requirements should be explicitly listed as out of scope with rationale
- New requirements should be clearly distinguished from carried-forward ones

### Change delta format
When a requirement is changing from a prior spec, document the delta clearly:

```
FR-045: Claims Auto-Approval Threshold
Source: Claims FSD v2.3, §3.2
Previous: Claims under £5,000 auto-approved if medical evidence complete
Proposed: Claims under £10,000 auto-approved if medical evidence complete 
          AND fraud score < 30
Rationale: Threshold increase approved by Claims Director (ref: Workshop 
           15-Jan-2025). Fraud score gate added per Compliance requirement.
Impact: Fraud detection integration required (new dependency)
```

---

## Pattern 2: Call Transcripts & Meeting Notes

Stakeholder interviews, workshops, discovery calls, and requirements elicitation sessions are the richest source of BA material — but also the most unstructured.

### What to extract

Process transcripts in a single pass and extract into these categories:

**a) Requirements statements** — things stakeholders said they need:
Look for phrases like "we need", "it should", "the system must", "I want to be able to", "currently we can't", "the problem is". These are candidate requirements.

| Req ID | Speaker / Role | Timestamp or context | Raw statement | Interpreted requirement | Confidence | Follow-up needed? |
|---|---|---|---|---|---|---|
| TR-001 | Sarah (Chief UW) | 12:34 | "We need to see the full medical history on one screen, not click through five tabs" | Consolidated medical history view in UW workbench | High | No — clear requirement |
| TR-002 | James (Ops Manager) | 23:15 | "It would be nice if we could automate the chasing" | Automated evidence chasing with configurable follow-up rules | Medium | Yes — clarify "chasing" scope: email only? phone? |
| TR-003 | Sarah (Chief UW) | 31:02 | "I don't want the AI making decisions I can't explain to the regulator" | All AI-assisted decisions must produce human-readable audit trail with regulatory-grade explainability | High | No — clear requirement + regulatory context |

**b) Pain points** — problems with the current state:
These inform the "current state" section of the BRD and the gap analysis.

| Pain point | Speaker | Impact | Implied requirement |
|---|---|---|---|
| "We spend 2 hours a day just reading GP reports" | UW Team Lead | Productivity loss, UW bottleneck | Automated evidence extraction |
| "Half the time the data from the broker is incomplete" | Ops Manager | Rework, delays, SLA breaches | Data validation at submission with mandatory field enforcement |

**c) Decisions made** — things that were agreed in the meeting:

| Decision | Made by | Context | Implications |
|---|---|---|---|
| "Let's go with Option B — real-time API, not batch" | CTO + Head of Ops | Integration approach for broker data | Real-time integration requirement, deprecate batch feed |

**d) Open questions and action items** — things that weren't resolved:

| Question | Raised by | Assigned to | Due | Status |
|---|---|---|---|---|
| "What's the regulatory position on auto-declining without human review?" | Compliance Officer | Legal team | 2 weeks | Open |
| "Can we get access to the GP Connect API?" | Tech Lead | Integration team | Next sprint | Open |

**e) Contradictions** — where stakeholders disagreed or said conflicting things:

| Contradiction | Stakeholder A | Stakeholder B | Resolution needed |
|---|---|---|---|
| Auto-decision scope | Chief UW: "Auto-accept only, never auto-decline" | Head of Ops: "We need auto-decline for clear-cut cases to hit STP targets" | Escalate to Steering Committee |

### Processing multiple transcripts

When multiple call transcripts are provided:
1. Process each independently first
2. Then cross-reference: look for requirements mentioned in multiple calls (stronger signal), contradictions between calls, and evolving positions (stakeholder changed their mind between calls)
3. Produce a consolidated extraction with source attribution to specific calls

### Tone and language translation

Stakeholders speak informally. Translate to requirements language:
- "It would be nice if..." → "Should" (desirable, not mandatory) — Could-have in MoSCoW
- "We absolutely need..." → "Shall" (mandatory) — Must-have in MoSCoW
- "I hate it when..." → Pain point → invert into a requirement
- "Can we just..." → Often hides complexity — flag for estimation
- "Obviously it should..." → Assumption — may not be obvious to everyone, document explicitly

---

## Pattern 3: Wiki Pages & Product Requirement Documents

Wiki exports (Confluence, SharePoint, Notion) and PRDs are semi-structured — they have headings and some organisation, but vary wildly in quality, currency, and completeness.

### What to extract

**From PRDs:**
PRDs typically operate at a higher level than BRDs — they describe product vision, user personas, and feature-level requirements. Extract and decompose:

| PRD element | What to extract | How it maps to BA deliverables |
|---|---|---|
| Product vision / objectives | Strategic goals, success metrics | BRD §1 Executive Summary, success criteria |
| User personas | Roles, needs, pain points | User story roles ("As a [persona]..."), stakeholder register |
| Feature descriptions | High-level capabilities | Epics and themes |
| User journeys / flows | Step-by-step interactions | Process flows, user stories |
| Success metrics / KPIs | Measurable outcomes | BRD §8 Success Criteria |
| Constraints / dependencies | Boundaries, external factors | BRD §6 Assumptions & Constraints |
| Priority / roadmap | Sequencing, MoSCoW | Backlog prioritisation |

**From wiki pages:**

Wiki pages are often fragmented across multiple pages with linking. Key challenges:
- Content may be outdated — check "last modified" dates and flag anything over 6 months old
- Multiple pages may cover the same topic with different (possibly contradictory) information
- Some pages are "living documents" that evolve, others are point-in-time snapshots

Extract approach:
1. Build a **page inventory** with titles, last-modified dates, and authors
2. Identify the "canonical" page for each topic (most recent, most authoritative)
3. Extract requirements, rules, and process descriptions from canonical pages
4. Cross-reference with other sources to validate currency

### Decomposition: PRD features → Epics → Stories

PRDs describe features at a level that's too high for development. Decompose systematically:

```
PRD Feature: "Intelligent Claims Triage"
  ↓ Decompose into...
Epic: EP-010 — Intelligent Claims Triage
  ↓ Break into stories...
  US-101: As a claims handler, I want incoming claims automatically 
          categorised by complexity, so that simple claims are fast-tracked.
  US-102: As a claims manager, I want to set and adjust triage rules, 
          so that categorisation reflects current business priorities.
  US-103: As a compliance officer, I want all triage decisions logged 
          with rationale, so that we can demonstrate fair treatment.
```

Each decomposition step should be traceable: Story → Epic → PRD Feature → Product Objective.

---

## Cross-Referencing Multiple Sources

When working with multiple source documents, produce a **Cross-Reference Matrix**:

| Requirement area | Knowledge base doc | Call transcript | Wiki / PRD | Consistent? | Notes |
|---|---|---|---|---|---|
| Claims auto-approval threshold | FSD v2.3: £5,000 | Workshop 15-Jan: £10,000 discussed | Wiki: £5,000 | No — threshold increase proposed | Use workshop figure, flag for formal approval |
| Evidence chasing process | FSD v2.3: Manual email | Workshop 15-Jan: "Automate chasing" | Wiki: Manual | Consistent on current state, change requested | New requirement for automation |
| Fraud detection | Not mentioned | Workshop 15-Jan: "Need fraud scoring" | PRD: "AI fraud detection" feature | Consistent — new capability | New requirement, no baseline |

This matrix is valuable because it surfaces:
- **Confirmed requirements**: Mentioned consistently across sources — high confidence
- **Contradictions**: Different sources say different things — needs resolution
- **Gaps**: Topics covered in some sources but not others — needs investigation
- **New vs changed vs carried forward**: Clear classification for the deliverable

---

## Source Traceability

Every requirement in the output deliverable should trace back to its source(s). Use a **Source Reference** field in every requirement:

```
FR-045: Claims Auto-Approval Threshold Update
Source(s): 
  - Baseline: Claims FSD v2.3, §3.2 (Mar 2024)
  - Change request: UW Workshop transcript, 15-Jan-2025, 23:15 (Sarah, Chief UW)
  - Validation: Confirmed in Steering Committee minutes, 22-Jan-2025
```

For requirements extracted from transcripts, include the speaker role and approximate timestamp or context — this allows stakeholders to verify that their input was correctly interpreted.

### Source confidence levels

Not all sources are equally reliable. Assign confidence:

| Confidence | Criteria | Action |
|---|---|---|
| **Confirmed** | Requirement stated in 2+ sources, or formally approved | Include as-is |
| **Likely** | Stated clearly by an authoritative stakeholder in one source | Include, flag for validation |
| **Inferred** | Not explicitly stated but logically implied by other requirements | Include as assumption, flag for confirmation |
| **Uncertain** | Contradictory sources, or mentioned casually without commitment | Add to Questions & Gaps Log, do not include as confirmed requirement |

---

## Quality Checklist

Before delivering any document produced from source ingestion:

- [ ] Source inventory table is included — every input document is catalogued
- [ ] Document freshness is assessed — stale documents flagged with last-known-good date
- [ ] Extractions are attributed to specific source, section, and page/timestamp
- [ ] Contradictions between sources are identified and flagged for resolution
- [ ] Gaps in source material are documented in a Questions & Gaps Log
- [ ] Requirements are classified as: carried forward, changed (with delta), new, or retired
- [ ] Stakeholder statements from transcripts are translated from informal language to requirements language
- [ ] Confidence levels are assigned to requirements based on source strength
- [ ] Cross-reference matrix is produced when 2+ sources are provided
- [ ] Assumptions made during synthesis are explicitly listed
- [ ] The output document clearly distinguishes between "from source" and "BA interpretation"
