# Stakeholder Communications Guide

BAs draft a high volume of stakeholder communications — status updates, change request summaries, steering committee briefs, escalation emails, and workshop invitations. This guide covers templates and tone guidance for insurance/financial services programmes.

## Table of Contents
1. [Communication Types & Templates](#communication-types--templates)
2. [Audience-Specific Tone](#audience-specific-tone)
3. [Status Update Template](#status-update-template)
4. [Change Request Summary](#change-request-summary)
5. [Steering Committee Brief](#steering-committee-brief)
6. [Escalation Email](#escalation-email)
7. [Workshop Invitation & Follow-Up](#workshop-invitation--follow-up)
8. [Quality Checklist](#quality-checklist)

---

## Communication Types & Templates

| Communication | Audience | Frequency | Format | Tone |
|---|---|---|---|---|
| Sprint status update | Product Owner, Scrum Master, stakeholders | Every sprint (bi-weekly) | Email or Slack | Concise, factual, action-oriented |
| Change request summary | Steering committee, sponsors | Ad hoc | Email with attachment | Formal, structured, impact-focused |
| Steering committee brief | COO, CTO, programme sponsors | Monthly or bi-weekly | Email + slide deck | Executive, headline-first, decision-focused |
| Escalation email | Senior management, blockers' managers | Urgent | Email | Direct, factual, solution-proposed |
| Workshop invitation | SMEs, stakeholders | Ad hoc | Email / calendar invite | Professional, clear agenda, prep instructions |
| Workshop follow-up | Same as invitation | Within 48hrs of workshop | Email | Summary-first, action items with owners and dates |
| Requirements sign-off request | Business owner, compliance | At milestone | Email with document link | Formal, clear ask, deadline stated |
| Release / go-live communication | Broader stakeholder group | At release | Email | Clear, what's changing, what to expect, support contacts |

---

## Audience-Specific Tone

### C-suite / Steering Committee
- Lead with the headline — decision or outcome needed
- Maximum 3-5 bullet points before any detail
- Use business language, not technical jargon
- Quantify impact (£, %, days, FTEs)
- Always state what you need from them (decision, budget, escalation support)

### Technical teams
- Be precise and specific — they appreciate detail
- Reference system names, API endpoints, data fields
- Include technical constraints and assumptions
- Link to Jira/ADO tickets or design documents

### Business SMEs (underwriters, claims handlers, ops)
- Use their domain language (underwriting terms, claims terminology)
- Focus on process impact — what changes for their daily work
- Be respectful of their expertise — they know the domain better than you
- Ask specific questions, not open-ended ones

### Compliance / Legal
- Reference specific regulations by article/section
- Be precise about data handling, consent, and retention
- Flag risks clearly with likelihood and impact
- Provide enough detail for them to make a determination

---

## Status Update Template

**Subject:** [Programme/Project] — Sprint [N] Status | [dates]

```
Hi [team/stakeholders],

Sprint [N] summary:

COMPLETED
• [US-xxx] [Story title] — [one-line outcome]
• [US-xxx] [Story title] — [one-line outcome]

IN PROGRESS (carrying to Sprint [N+1])
• [US-xxx] [Story title] — [brief reason for carry-over]

BLOCKED / AT RISK
• [US-xxx] [Story title] — Blocked by [reason]. Action: [who] to [what] by [when].

KEY DECISIONS NEEDED
• [Decision description] — needed by [date] to avoid [impact]

METRICS
• Velocity: [X] points completed / [Y] planned
• STP rate (if applicable): [X]%
• Defect count: [X] open ([Y] critical)

NEXT SPRINT FOCUS
• [Top 2-3 priorities for next sprint]

Shout if any questions.

[Name]
```

---

## Change Request Summary

**Subject:** Change Request: [CR-xxx] — [Title] | Impact Assessment

```
CHANGE REQUEST SUMMARY

CR ID: [CR-xxx]
Title: [Descriptive title]
Requested by: [Name, Role]
Date raised: [Date]
Priority: [Critical / High / Medium / Low]

WHAT'S CHANGING
[2-3 sentences describing the change in business terms]

WHY
[Business rationale — regulatory driver, stakeholder request, defect, market change]

IMPACT ASSESSMENT

| Dimension       | Impact    | Detail                                      |
|-----------------|-----------|---------------------------------------------|
| Scope           | [H/M/L]  | [What's added/removed/changed]              |
| Timeline        | [H/M/L]  | [Sprint impact, delay risk]                 |
| Budget          | [H/M/L]  | [Additional cost estimate if known]         |
| Resources       | [H/M/L]  | [Additional effort, skills needed]          |
| Risk            | [H/M/L]  | [New risks introduced]                      |
| Regulatory      | [H/M/L]  | [Compliance implications]                   |
| Downstream      | [H/M/L]  | [Impact on other workstreams/releases]      |

RECOMMENDATION
[Accept / Reject / Defer to Phase N / Accept with conditions]

[If accept:] Estimated effort: [X story points / Y person-days]
Proposed sprint: [Sprint N]

DECISION REQUIRED BY: [Date]

Attached: [Full impact assessment document if applicable]
```

---

## Steering Committee Brief

**Subject:** [Programme] — Steering Committee Update | [Date]

```
PROGRAMME STATUS: [GREEN / AMBER / RED]

HEADLINE
[One sentence — the single most important thing the committee needs to know]

PROGRESS SINCE LAST MEETING
• [Milestone achieved or key delivery]
• [Milestone achieved or key delivery]
• [Metric improvement if applicable]

RISKS & ISSUES (action required)

| # | Risk/Issue              | Impact | Likelihood | Mitigation               | Owner    | Decision needed? |
|---|-------------------------|--------|------------|---------------------------|----------|-----------------|
| 1 | [Description]           | High   | Medium     | [Action being taken]      | [Name]   | Yes / No        |
| 2 | [Description]           | Medium | High       | [Action being taken]      | [Name]   | Yes / No        |

DECISIONS REQUESTED
1. [Decision description] — Recommendation: [X]. Impact if delayed: [Y].
2. [Decision description] — Options: [A] or [B]. BA recommendation: [A] because [reason].

BUDGET / FINANCIALS
• Spend to date: £[X] of £[Y] budget ([Z]%)
• Forecast: [On track / Overspend risk of £X — reason]

NEXT PERIOD PLAN
• [Key deliverable 1 — target date]
• [Key deliverable 2 — target date]
• [Key milestone — target date]

APPENDIX: Detailed sprint metrics, RTM status, test coverage
[Link to dashboard or attached document]
```

---

## Escalation Email

**Subject:** ESCALATION: [Issue title] — [Impact if not resolved by date]

```
Hi [Manager / Senior Stakeholder],

I'm escalating [issue] because [it's blocking / it will cause] [specific impact] 
if not resolved by [date].

SITUATION
[2-3 sentences — what's happening, what was expected, what actually occurred]

IMPACT
• [Delivery impact — sprint delay, milestone risk]
• [Business impact — SLA breach, client impact, regulatory risk]
• [Cost impact if applicable]

WHAT WE'VE TRIED
• [Action 1 — outcome]
• [Action 2 — outcome]

WHAT WE NEED
[Specific ask — decision, resource, access, prioritisation]
From: [Name / Team]
By: [Date]

Happy to discuss — available [times].

[Name]
```

Key rules for escalation emails:
- Be factual, not emotional
- Show that you've already tried to resolve it
- Make the ask specific and actionable
- State the deadline and consequence of missing it
- Copy the right people — the person who can unblock, plus your own manager

---

## Workshop Invitation & Follow-Up

### Invitation

**Subject:** Workshop: [Topic] | [Date, Time, Duration] | [Location/Teams link]

```
Hi [attendees],

I'd like to invite you to a [requirements / design / review] workshop on [topic].

PURPOSE
[What we're trying to achieve in this session]

AGENDA
1. [Item] — [duration] — [facilitator]
2. [Item] — [duration] — [facilitator]
3. [Item] — [duration] — [facilitator]

PREPARATION NEEDED
• Please review [document/link] before the session
• Come prepared to discuss [specific topic]
• [Any other pre-work]

ATTENDEES
• [Name — Role — why they're needed]
• [Name — Role — why they're needed]

Please confirm your attendance by [date]. If you can't attend, 
please nominate a delegate who can represent your area.

[Name]
```

### Follow-Up (within 48 hours)

**Subject:** Workshop Follow-Up: [Topic] | [Date] — Decisions & Actions

```
Hi all,

Thank you for [the workshop]. Here's a summary of what we covered.

DECISIONS MADE
1. [Decision] — Agreed by [names]
2. [Decision] — Agreed by [names]

ACTION ITEMS
| # | Action                          | Owner    | Due date   | Status |
|---|---------------------------------|----------|------------|--------|
| 1 | [Action description]            | [Name]   | [Date]     | Open   |
| 2 | [Action description]            | [Name]   | [Date]     | Open   |

OPEN QUESTIONS (to be resolved offline)
• [Question] — Owner: [Name] — Due: [Date]

KEY REQUIREMENTS CAPTURED
[Summary of requirements discussed — or link to updated requirements document]

NEXT STEPS
• [What happens next]
• Next workshop: [Date] — Topic: [X]

Please review and flag any corrections by [date]. Silence = agreement.

[Name]
```

---

## Quality Checklist

- [ ] Subject line is clear and scannable (includes project name, type, date)
- [ ] Lead with the headline — most important information first
- [ ] Tone matches the audience (executive vs technical vs business)
- [ ] Actions have owners and deadlines
- [ ] Decisions needed are explicitly called out with recommendation
- [ ] Impact is quantified where possible (£, %, days, FTEs)
- [ ] Email is concise — detail goes in attachments, not the email body
- [ ] Risk/issue language is factual, not alarmist
- [ ] Regulatory implications are flagged for compliance-sensitive topics
- [ ] Follow-up emails go out within 48 hours of workshops
