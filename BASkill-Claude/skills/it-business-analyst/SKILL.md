---
name: it-business-analyst
description: "Use this skill for IT Business Analysis deliverables in insurance, reinsurance, or financial services. Triggers: writing BRDs, FRDs, user stories, epics, themes, acceptance criteria; creating process flows or swimlane diagrams; building RACI matrices or stakeholder maps; performing gap analysis or impact assessments; breaking features into epics and stories; creating traceability matrices or data dictionaries; source-to-target data mappings; ingesting existing specs, transcripts, wiki pages, or PRDs; estimating stories or epics; drafting stakeholder comms, status updates, or steering briefs; assessing regulatory impact; building glossaries. Trigger on any structured analysis deliverable even without 'BA'. Domain-aware for life & health, P&C, reinsurance, underwriting, claims, and policy admin."
---

# IT Business Analyst Skill
## Financial Services & Insurance Edition

> **Domain specificity:** This skill is purpose-built for Business Analysis in **insurance, reinsurance, and financial services**. All templates, glossaries, regulatory checklists, process patterns, and examples are tailored to this domain — including life & health, P&C, London Market, and reinsurance. While the frameworks (BRD structure, user story format, RACI, etc.) are transferable to other industries, the domain vocabulary, regulatory checklists (Solvency II, IDD, GDPR, FCA Consumer Duty, Lloyd's), data patterns (ICD-10 codes, policy lifecycle, bordereaux), and estimation multipliers are insurance-specific. If you need a general-purpose BA skill, strip the domain-specific references and regulatory checklists.

This skill helps produce professional-grade Business Analysis deliverables tailored to insurance and financial services. It covers the full BA toolkit: requirements documentation, process modelling, stakeholder management, gap analysis, agile backlog structuring, data mapping, traceability, estimation, stakeholder communications, regulatory impact assessment, and glossary management.

## When to read reference files

Before producing any deliverable, check the `references/` directory for the relevant guide:
- **Requirements docs** (BRD, FRD, user stories, epics) → read `references/requirements-guide.md`
- **Process diagrams** (BPMN, swimlanes, workflows) → read `templates/process-flow-template.html` for the interactive template, and `references/process-modelling-guide.md` for Mermaid patterns
- **Stakeholder & RACI** → read `references/stakeholder-guide.md`
- **Gap analysis & impact assessment** → read `references/gap-analysis-guide.md`
- **Source ingestion** (when user uploads existing docs, transcripts, wiki exports, or PRDs as input) → read `references/source-ingestion-guide.md`
- **Data dictionary & data mapping** (field specs, S2T mapping, transformation rules) → read `references/data-dictionary-guide.md`
- **Requirements traceability matrix** (RTM, coverage analysis, regulatory traceability) → read `references/traceability-matrix-guide.md`
- **Estimation** (story points, T-shirt sizing, complexity scoring) → read `references/estimation-guide.md`
- **Stakeholder communications** (status updates, change requests, steering briefs, escalations) → read `references/communications-guide.md`
- **Regulatory impact** (Solvency II, IDD, GDPR, FCA Consumer Duty, Lloyd's) → read `references/regulatory-checklists.md`
- **Glossary & acronyms** (auto-generate, maintain, insurance domain terms) → read `references/glossary-guide.md`

Always read the relevant reference file before starting work — it contains structure templates, insurance-domain examples, and quality checklists.

## General principles

These principles apply across all BA deliverables:

1. **Audience-awareness matters.** BA documents serve different readers — business sponsors want outcomes and impact, technical teams want specificity and constraints, compliance teams want regulatory traceability. Always ask (or infer) who the audience is and adjust depth and language accordingly.

2. **Insurance domain vocabulary.** Use correct industry terminology: cedant, retrocession, treaty, facultative, bordereaux, loss ratio, combined ratio, IBNR, substandard risk, rated/declined, moratorium, pre-existing condition, guaranteed issue, group scheme, STP (straight-through processing). Don't over-explain terms to an insurance audience, but do define them when the document may reach non-specialist readers.

3. **Traceability is non-negotiable.** Every requirement should be uniquely identified (e.g., BRD-001, FR-012, US-045) and traceable upstream to a business objective and downstream to acceptance criteria or test cases. Include a traceability section or matrix when producing requirements documents.

4. **Regulatory awareness.** Insurance and financial services operate under heavy regulation (Solvency II, IDD, GDPR, FCA conduct rules, Lloyd's standards, local insurance regulations). Flag where requirements intersect with regulatory obligations — even if the user doesn't ask.

5. **Assumptions and dependencies up front.** Every deliverable should explicitly state assumptions, dependencies, constraints, and exclusions. These are often the most valuable parts of a BA document because they surface hidden risks early.

6. **Version control metadata.** Include a document control section with version number, author, reviewer, approval status, and change history. This is standard practice in regulated industries.

## Output format selection

Choose the output format based on what the user needs:

| Deliverable | Default format | When to use alternatives |
|---|---|---|
| BRD, FRD, requirements spec | `.docx` (use the docx skill) | Markdown for quick drafts |
| User stories, epics, themes | Markdown in chat or `.xlsx` for backlogs | `.docx` if formal sign-off needed |
| Process flows / BPMN / swimlanes | **Interactive `.html`** (use `templates/process-flow-template.html`) | Mermaid for inline/markdown embedding |
| RACI matrix | `.xlsx` (use the xlsx skill) | Markdown table for small teams |
| Stakeholder map | Mermaid quadrant chart or `.xlsx` | |
| Gap analysis | `.xlsx` (use the xlsx skill) | `.docx` for narrative format |
| Impact assessment | `.docx` (use the docx skill) | `.xlsx` for tabular format |
| Traceability matrix (RTM) | `.xlsx` (use the xlsx skill) | Include conditional formatting for status tracking |
| Data dictionary | `.xlsx` (use the xlsx skill) | Separate sheets for field catalogue, enums, entity relationships |
| Source-to-target mapping | `.xlsx` (use the xlsx skill) | Include transformation rules sheet |
| Estimation (story/epic level) | `.xlsx` (use the xlsx skill) | Markdown table for quick estimates in chat |
| Stakeholder communications | Draft in chat using message_compose tool | `.docx` for formal steering committee packs |
| Regulatory impact assessment | `.xlsx` checklist + `.docx` narrative | Include cross-regulation summary matrix |
| Glossary | Embedded section in parent document | `.xlsx` for standalone master glossary |

When producing `.docx` files, read the docx skill first. When producing `.xlsx` files, read the xlsx skill first. These skills contain critical instructions for file creation.

## Process flow visualisation

When the user asks for a process flow, workflow, BPMN diagram, or swimlane, **always produce an interactive HTML file** as the primary output. This is the default — BAs can use these directly in presentations, stakeholder reviews, and documentation.

### How to generate the interactive process flow

1. Read the template at `templates/process-flow-template.html`
2. Build a JSON config object matching the template's `config` structure (see below)
3. Create a new HTML file by copying the template and replacing `{{FLOW_CONFIG_JSON}}` with your config, and replacing the `{{TITLE}}`, `{{SUBTITLE}}`, `{{BADGE_TEXT}}`, and `{{FOOTER}}` placeholders
4. Save as `.html` in the outputs directory

### Config structure

The config object has this shape:

```json
{
  "stats": [
    { "value": "60%+", "label": "Target STP Rate" },
    { "value": "< 3s", "label": "Auto-Decision Latency" }
  ],
  "phases": [
    {
      "label": "EP-001 · Evidence Extraction",
      "type": "extract",
      "nodes": [
        { "id": "docai", "type": "auto", "icon": "🔍", "title": "Rapid Doc AI", "sub": "OCR + NLP extraction" },
        { "id": "gate1", "type": "gate", "icon": "⚖️", "title": "Confidence ≥ 85%?", "sub": "Quality gate" }
      ],
      "branches": { "yes": "Yes → Next phase", "no": "No → Human review" }
    }
  ],
  "details": {
    "docai": {
      "epic": "EP-001 · Evidence Extraction",
      "epicColor": "var(--accent-cyan)",
      "title": "🔍 Rapid Doc AI",
      "desc": "Description of what this step does...",
      "sections": [
        { "title": "Capabilities", "items": ["Item 1", "Item 2"] },
        { "title": "Technology", "tags": ["Azure AI", "OCR"] }
      ]
    }
  }
}
```

### Node types and when to use them

| Type | Colour | Use for |
|---|---|---|
| `auto` | Green | Automated / deterministic steps (rules engines, system processing) |
| `ai` | Purple | AI / ML / probabilistic steps |
| `human` | Blue | Human-in-the-loop steps (manual review, overrides, approvals) |
| `gate` | Amber | Decision points / quality gates / routing logic |
| `output` | Cyan | Outputs, integrations, external-facing results |

### Phase types for label colouring

Use these `type` values on phases to get matching label colours: `extract`, `map`, `decide`, `orchestrate`, `output`, `entry`, `input`. If none fit, use `default`.

### Design principles for the flow

- Each phase should represent a logical stage (epic, workstream, or functional area)
- Include 2-4 nodes per phase — enough to show the key steps without clutter
- Always include decision gates where routing logic exists
- Add `branches` to any phase that has conditional routing (yes/no, pass/fail)
- Stats bar should show 3-5 key metrics relevant to the process
- Detail panel should include: description, capabilities/steps, technology stack, SLAs where relevant, and traceable user story references
- The flow should tell a story top-to-bottom — a stakeholder should be able to read it without explanation

### When to also include Mermaid

Mermaid diagrams are useful as a **secondary** output for embedding in markdown documents, BRDs, or chat responses. Use Mermaid for quick inline diagrams, but always produce the interactive HTML as the primary deliverable when the user asks for a process flow or workflow visualisation. See `references/process-modelling-guide.md` for Mermaid patterns.

## Source ingestion — working from existing materials

BAs rarely start from scratch. Most deliverables are built from existing documentation, stakeholder conversations, and organisational knowledge. When the user uploads or references source materials, always read `references/source-ingestion-guide.md` for the full extraction methodology.

### Recognising source ingestion scenarios

Trigger the ingestion workflow when:
- User uploads documents and says anything like "based on this...", "use this as input", "here's the existing spec", "create a BRD from these", "here are the meeting notes"
- User provides call transcripts, meeting recordings, or interview notes
- User references wiki pages, Confluence exports, or PRD documents
- User asks to "update" or "build on" an existing specification
- User provides multiple documents that need to be synthesised

### The five-step ingestion workflow

1. **Inventory and assess** — catalogue every source document: type, date, length, relevance, freshness. Present the inventory to the user before proceeding. Flag stale or missing documents.

2. **Deep read and extract** — read each source using the appropriate extraction pattern:
   - **Existing specs / design docs**: Extract business rules, functional requirements, integration points, data model elements, and prior assumptions. Classify each as carry-forward, changed, or retired.
   - **Call transcripts**: Extract requirements statements, pain points, decisions made, open questions, and contradictions between stakeholders. Translate informal language into requirements language.
   - **Wiki pages / PRDs**: Extract product vision, feature descriptions, user journeys, and success metrics. Decompose PRD features into epics and stories. Check page freshness and identify the canonical source when multiple pages cover the same topic.

3. **Synthesise and cross-reference** — when multiple sources are provided, produce a cross-reference matrix showing where sources agree, contradict, or leave gaps. This is one of the most valuable outputs a BA can produce.

4. **Produce the deliverable** — write the BRD, FRD, stories, or other output with full source traceability. Every requirement should reference where it came from.

5. **Flag gaps and questions** — always produce a Questions & Gaps Log at the end. This surfaces what the source material didn't answer and what needs stakeholder follow-up.

### Source traceability in outputs

Every requirement produced from source material must include a source reference:
- For existing docs: document name, version, section/page number
- For transcripts: speaker name/role, approximate timestamp or context
- For wiki/PRD: page title, last-modified date

Assign confidence levels: Confirmed (2+ sources agree), Likely (single authoritative source), Inferred (logically implied), Uncertain (contradictory or casual mention).

### Change delta documentation

When updating an existing specification, always document the delta clearly — what was the previous requirement, what is the proposed change, who requested it, and what's the rationale. The source ingestion guide has the format template for this.

## Cross-cutting behaviours

These behaviours apply automatically across all deliverables — you don't need the user to ask for them.

### Auto-generate glossary
When producing any document (BRD, FRD, impact assessment, etc.), automatically scan for acronyms and domain terms. Append a glossary section to the document. Read `references/glossary-guide.md` for the core insurance glossary — use standard definitions where they exist, and add project-specific terms as needed.

### Regulatory impact scan
When any deliverable involves a change to underwriting, claims, policy administration, data processing, distribution, or pricing, automatically scan against the regulatory checklists in `references/regulatory-checklists.md`. Flag applicable items in the deliverable — even if the user didn't ask for a regulatory assessment. Use the cross-regulation summary matrix to quickly identify which regulations are triggered by the change type.

### Traceability by default
Every requirement produced — whether in a BRD, FRD, or user story — should carry a unique ID and be traceable. When producing multiple related deliverables (e.g., BRD + user stories + RTM), maintain consistent IDs across them. Read `references/traceability-matrix-guide.md` when producing formal traceability artefacts.

### Estimation readiness
When producing user stories or epics, include a complexity indicator (using the dimensions from `references/estimation-guide.md`) to help the team estimate. This doesn't replace team estimation but gives them a starting point. Flag insurance-specific complexity factors (multi-territory, regulatory, reinsurance, legacy integration).

## Working with the user

- If the user gives a vague brief (e.g., "write user stories for a claims portal"), ask one focused clarifying question about scope or audience before producing output — don't generate 30 stories blind.
- If the user provides detailed context, proceed directly with output.
- For large deliverables (full BRD, comprehensive gap analysis), offer to start with an outline/structure for review before filling in detail.
- When the user uploads an existing document for review or enhancement, read it first, then provide a structured assessment before making changes.

## Test cases for self-validation

When producing any deliverable, mentally verify:
- [ ] Does every requirement have a unique ID?
- [ ] Are acceptance criteria testable and specific (not vague like "system should be fast")?
- [ ] Are assumptions, dependencies, and exclusions stated?
- [ ] Is the insurance/financial services context reflected in terminology and examples?
- [ ] Is the format appropriate for the audience?
- [ ] Would a senior BA at a reinsurer or insurer consider this professional-grade?
