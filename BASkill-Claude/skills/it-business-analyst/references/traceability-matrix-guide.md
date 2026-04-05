# Requirements Traceability Matrix (RTM) Guide

The RTM is the connective tissue of a BA programme — it links business objectives to requirements to design to test cases to delivery. In regulated industries like insurance, traceability is not optional; it's how you demonstrate compliance and change governance.

## Table of Contents
1. [RTM Structure](#rtm-structure)
2. [Traceability Levels](#traceability-levels)
3. [Building the RTM](#building-the-rtm)
4. [RTM for Agile Delivery](#rtm-for-agile-delivery)
5. [Regulatory Traceability](#regulatory-traceability)
6. [Quality Checklist](#quality-checklist)

---

## RTM Structure

Produce the RTM as an `.xlsx` workbook with conditional formatting for status tracking.

### Core RTM sheet

| Column | Description |
|---|---|
| Req ID | Unique requirement identifier (BRD-001, FR-012, US-045) |
| Requirement title | Short descriptive name |
| Requirement type | Business / Functional / Non-Functional |
| Priority | MoSCoW or numeric |
| Business objective | Which strategic objective this traces to |
| BRD reference | Parent business requirement (for FRs and stories) |
| Epic / Theme | Agile backlog mapping |
| User story | Story ID(s) that implement this requirement |
| Design reference | Solution design document / section |
| Test case ID(s) | UAT / QA test cases that verify this requirement |
| Test status | Not started / In progress / Passed / Failed / Blocked |
| Sprint / Release | When it's scheduled for delivery |
| Delivery status | Backlog / In development / In QA / Done / Deferred / Descoped |
| Owner | BA or product owner responsible |
| Regulatory link | Regulation reference if compliance-driven |
| Source | Where the requirement originated (stakeholder, document, transcript) |
| Change history | Version and date of last change |
| Notes | Additional context, dependencies, risks |

### Summary dashboard sheet

Include pivot tables and charts showing:
- Requirements by status (how many done, in progress, not started, deferred)
- Requirements by priority (Must/Should/Could breakdown with delivery status)
- Test coverage (requirements with test cases vs without)
- Regulatory requirements coverage (all regulatory-linked requirements with test status)
- Sprint/release view (what's in each sprint, delivery confidence)

### Conditional formatting rules

Apply colour-coding to make the RTM scannable at a glance:

| Condition | Colour | Meaning |
|---|---|---|
| Delivery status = Done, Test status = Passed | Green | Complete and verified |
| Delivery status = Done, Test status = Failed | Red | Delivered but failing tests — action needed |
| Delivery status = In development | Blue | In progress |
| Delivery status = Deferred or Descoped | Grey | Parked — monitor |
| Test case ID = blank | Amber | No test coverage — gap |
| Regulatory link is not empty AND Test status ≠ Passed | Red border | Regulatory requirement not yet verified — risk |
| Priority = Must AND Delivery status = Backlog | Amber | Must-have not yet started — schedule risk |

---

## Traceability Levels

Traceability works in both directions — upstream (why does this exist?) and downstream (how is it implemented and verified?).

### Full traceability chain

```
Business Objective / Strategy
  ↓ traces to
Business Requirement (BRD-xxx)
  ↓ decomposes into
Functional Requirement (FR-xxx)
  ↓ implemented by
User Story (US-xxx) in Epic/Sprint
  ↓ designed in
Solution Design Document (section ref)
  ↓ verified by
Test Case (TC-xxx)
  ↓ evidenced by
Test Execution Result (Pass/Fail + evidence)
```

### Traceability types

| Type | Direction | Purpose |
|---|---|---|
| **Forward** | Objective → Requirement → Story → Test | Ensures every objective is implemented and tested |
| **Backward** | Test → Story → Requirement → Objective | Ensures nothing is built without a business justification |
| **Horizontal** | Requirement ↔ Requirement | Identifies dependencies between requirements |
| **Regulatory** | Regulation → Requirement → Test → Evidence | Demonstrates compliance — critical for audits |

### Coverage analysis

The RTM should answer these questions:
- Are there any business objectives with no requirements? (strategic gap)
- Are there any requirements with no user stories? (delivery gap)
- Are there any user stories with no test cases? (quality gap)
- Are there any requirements with no business objective? (scope creep — why does this exist?)
- Are there any regulatory requirements without verified test evidence? (compliance risk)

---

## Building the RTM

### When to start
Start the RTM at the same time as the BRD — not after. Add rows as requirements are written. This prevents the common anti-pattern of building the RTM retrospectively (which invariably results in gaps and invented traceability).

### Incremental build pattern

| Phase | What to add to the RTM |
|---|---|
| Requirements gathering | Req ID, title, type, priority, business objective, source |
| Backlog creation | Epic, user story, sprint/release |
| Design | Design reference |
| Test planning | Test case IDs |
| Execution | Test status, delivery status |
| Go-live | Final status, sign-off |

### Linking conventions

Use consistent ID formats so cross-references are unambiguous:
- Business requirements: `BRD-001`, `BRD-002`
- Functional requirements: `FR-001`, `FR-002`
- Non-functional requirements: `NFR-001`, `NFR-002`
- User stories: `US-001`, `US-002`
- Epics: `EP-001`, `EP-002`
- Test cases: `TC-001`, `TC-002`
- Design sections: `DES-§3.2`, `DES-§4.1`

A single FR may trace to multiple stories (decomposition), and a single story may satisfy parts of multiple FRs (aggregation). The RTM should capture many-to-many relationships — use comma-separated IDs or multiple rows.

---

## RTM for Agile Delivery

In agile programmes, the RTM needs to coexist with backlogs and sprint boards without creating overhead.

### Lightweight RTM approach

For agile teams that find a full RTM too heavyweight:
- Maintain the RTM at the **epic/feature level** rather than individual stories
- Use story-level acceptance criteria as the "test case" equivalent
- Update the RTM at sprint boundaries, not daily
- Automate where possible: if using Jira or Azure DevOps, the RTM can be a view/report rather than a separate spreadsheet

### RTM columns for agile

| Column | Agile equivalent |
|---|---|
| Req ID | Epic ID or Feature ID |
| User story | Jira/ADO story key |
| Test case | Acceptance criteria reference or test suite ID |
| Sprint / Release | Sprint number or PI (Programme Increment) |
| Delivery status | Story status from the board (To Do / In Progress / Done) |
| Test status | Sprint demo acceptance or QA sign-off |

### Maintaining traceability across sprints

Each sprint planning session should verify:
- Stories in the sprint trace back to a requirement in the RTM
- No "orphan" stories are created without a parent requirement (unless explicitly agreed as tech debt or spike)
- Deferred stories are updated in the RTM with the reason for deferral

---

## Regulatory Traceability

In insurance, certain requirements are driven directly by regulation. The RTM must make these visible and trackable separately.

### Regulatory traceability view

Create a filtered view or separate sheet showing only regulatory-linked requirements:

| Reg reference | Regulation | Requirement | Req ID | Test case | Test status | Evidence | Compliance risk |
|---|---|---|---|---|---|---|---|
| Solvency II Art. 258 | Solvency II | Underwriting policy must be documented and approved by board | BRD-007 | TC-015 | Passed | Board minutes 15-Mar-2025 | Low |
| IDD Art. 25 | Insurance Distribution Directive | Demands and needs assessment must be recorded for every sale | FR-023 | TC-042, TC-043 | In progress | — | Medium — UAT not complete |
| GDPR Art. 17 | General Data Protection Regulation | Right to erasure must be supported for policyholder data | FR-031 | TC-051 | Not started | — | High — not yet tested |
| FCA PRIN 12 | Consumer Duty | Fair value assessment for all products | BRD-012 | TC-060 | Not started | — | High — new requirement |

This view is what auditors and compliance teams will ask for. Having it ready and current saves significant programme time during regulatory reviews.

---

## Quality Checklist

- [ ] Every requirement has a unique, consistently formatted ID
- [ ] Forward traceability is complete: every objective → requirement → story → test
- [ ] Backward traceability is clean: no orphan stories without parent requirements
- [ ] Test coverage is assessed: requirements without test cases are flagged amber
- [ ] Regulatory requirements have a separate filtered view with compliance status
- [ ] Conditional formatting is applied for at-a-glance status
- [ ] Summary dashboard shows coverage, status distribution, and risk areas
- [ ] RTM is updated at sprint boundaries, not just at project milestones
- [ ] Deferred and descoped requirements are tracked with rationale
- [ ] Change history is maintained for every requirement modification
