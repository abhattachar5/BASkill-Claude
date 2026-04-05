# Data Dictionary & Data Mapping Guide

BAs spend significant time defining data — field-level specifications, source-to-target mappings, data transformation rules, and data quality requirements. This guide covers how to produce professional data deliverables for insurance/financial services programmes.

## Table of Contents
1. [Data Dictionary](#data-dictionary)
2. [Source-to-Target Mapping](#source-to-target-mapping)
3. [Data Transformation Rules](#data-transformation-rules)
4. [Insurance Domain Data Patterns](#insurance-domain-data-patterns)
5. [Quality Checklist](#quality-checklist)

---

## Data Dictionary

A data dictionary defines every data element in the system — its name, type, format, business meaning, validation rules, and ownership. Produce as an `.xlsx` workbook.

### Structure (Excel)

**Sheet 1: Field Catalogue**

| Column | Description | Example |
|---|---|---|
| Field ID | Unique identifier | FLD-001 |
| Entity | Parent entity/table | Applicant |
| Field name (logical) | Business-friendly name | Date of Birth |
| Field name (physical) | System/database name | applicant_dob |
| Data type | String, Integer, Date, Decimal, Boolean, Enum | Date |
| Format / mask | Expected format | YYYY-MM-DD |
| Length / precision | Max length or decimal places | 10 chars |
| Required? | Mandatory / Optional / Conditional | Mandatory |
| Conditional logic | If conditional, when is it required? | — |
| Default value | Default if not supplied | NULL |
| Allowed values / enum | Valid value set | — |
| Validation rules | Business rules for valid data | Must be in past; age 16-85 at application date |
| Business definition | Plain-English description of what this field means | The applicant's date of birth as stated on the application form |
| Source system | Where this data originates | E-Application Portal |
| Owner | Business owner of this data element | Underwriting Ops |
| PII flag | Is this personally identifiable information? | Yes |
| Regulatory flag | Regulatory requirement for capture/retention | GDPR Art.6 — legitimate interest |
| Notes | Additional context | Used for age-at-entry calculation and premium rating |

**Sheet 2: Enum / Reference Data**

| Enum name | Code | Display value | Description | Active? |
|---|---|---|---|---|
| SmokingStatus | NS | Non-Smoker | Never smoked or quit 12+ months ago | Yes |
| SmokingStatus | SM | Smoker | Current smoker or quit < 12 months ago | Yes |
| SmokingStatus | EX | Ex-Smoker | Quit 12+ months ago (some products distinguish) | Yes |
| SmokingStatus | UN | Unknown | Smoking status not declared | Yes |
| RiskDecision | STD | Standard | Accept at standard premium rates | Yes |
| RiskDecision | RTD | Rated | Accept with premium loading | Yes |
| RiskDecision | EXC | Exclusion | Accept with condition exclusion | Yes |
| RiskDecision | DEC | Declined | Application declined | Yes |
| RiskDecision | DEF | Deferred | Decision postponed pending further evidence | Yes |
| RiskDecision | PPD | Postponed | Cannot consider at present, re-apply later | Yes |

**Sheet 3: Entity Relationship Summary**

| Entity | Description | Key fields | Relationships |
|---|---|---|---|
| Applicant | Person applying for cover | applicant_id, name, dob, gender | Has many Applications |
| Application | Single application for a product | application_id, product_code, sum_assured | Belongs to Applicant; has one Risk Assessment |
| Risk Assessment | UW assessment of an application | assessment_id, decision, rating_pct | Belongs to Application; has many Evidence Items |
| Evidence Item | Supporting document or data point | evidence_id, type, source, confidence | Belongs to Risk Assessment |
| Policy | Issued policy | policy_id, effective_date, status | Created from Application |

### Tips for insurance data dictionaries
- Always include PII flags — insurance data is heavily personal (medical, financial, lifestyle)
- Distinguish between data captured at application vs data derived during underwriting vs data added post-issue
- Include data retention periods where known (regulatory minimums vary: typically 7 years post-policy-end for life, longer for claims)
- Reference ICD-10 codes for medical condition fields, ISO country/currency codes for territory/financial fields

---

## Source-to-Target Mapping

Source-to-target (S2T) mapping specifies how data moves from one system to another — field by field, with transformation rules. Produce as an `.xlsx` workbook.

### Structure (Excel)

**Sheet: Source-to-Target Mapping**

| Map ID | Source system | Source entity | Source field | Source type | Target system | Target entity | Target field | Target type | Transformation rule | Default / fallback | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| M-001 | Broker Portal | Submission | proposer_name | VARCHAR(200) | UW Engine | Applicant | full_name | VARCHAR(150) | Trim whitespace; truncate at 150 chars | — | Source allows 200, target 150 — data loss risk for very long names |
| M-002 | Broker Portal | Submission | dob | DD/MM/YYYY | UW Engine | Applicant | applicant_dob | YYYY-MM-DD | Reformat date; validate age 16-85 | Reject if invalid | Broker portal uses UK date format, target uses ISO |
| M-003 | Broker Portal | Submission | smoker_flag | Y/N | UW Engine | Applicant | smoking_status | ENUM | Y→SM, N→NS | UN (Unknown) if null | Source is binary; target has richer enum — default to simple mapping |
| M-004 | GP Report (OCR) | Extraction | condition_text | TEXT | UW Engine | MedicalCondition | icd10_code | VARCHAR(10) | NLP entity extraction → ICD-10 lookup | Flag for manual coding if no match | AI-assisted mapping with confidence scoring |
| M-005 | Legacy System | PolicyMaster | pol_stat | CHAR(1) | New Platform | Policy | status | ENUM | A→Active, L→Lapsed, C→Cancelled, X→Expired, S→Surrendered | Error if unmapped code | Legacy uses single-char codes |

### Mapping categories

| Category | Description | Example |
|---|---|---|
| **Direct** | 1:1 field mapping, no transformation | first_name → first_name |
| **Format** | Same data, different format | DD/MM/YYYY → YYYY-MM-DD |
| **Lookup** | Map codes/values via reference table | Y/N → Enum lookup |
| **Calculated** | Derive target from source fields | age = today - dob |
| **Concatenated** | Combine multiple source fields | full_name = first + ' ' + last |
| **Split** | Split one source into multiple targets | full_name → first_name + last_name |
| **Conditional** | Different mapping based on conditions | If product='Life' then map to life_table, else health_table |
| **Default** | No source — target gets a default | created_by = 'MIGRATION' |
| **Unmapped** | Source field has no target (document why) | legacy_ref — no longer needed |

### Data migration vs real-time integration

Distinguish between:
- **Migration mappings**: One-time data load from legacy to new system — include record counts, data cleansing rules, and rollback strategy
- **Integration mappings**: Ongoing real-time or batch data flow — include frequency, error handling, retry logic, and monitoring

---

## Data Transformation Rules

For complex transformations, document separately:

| Rule ID | Description | Input | Output | Logic | Error handling |
|---|---|---|---|---|---|
| TFM-001 | Age at entry calculation | applicant_dob, application_date | age_at_entry (INT) | FLOOR((application_date - applicant_dob) / 365.25) | Reject if age < 16 or > 85 |
| TFM-002 | BMI calculation | height_cm, weight_kg | bmi (DECIMAL 4,1) | weight_kg / (height_cm/100)² | NULL if either input missing |
| TFM-003 | Premium loading application | base_premium, rating_pct | loaded_premium (DECIMAL 12,2) | base_premium × (1 + rating_pct/100) | Use base_premium if rating_pct = 0 |
| TFM-004 | Smoking status normalisation | smoker_flag, cessation_date | smoking_status (ENUM) | If flag=N → NS; If flag=Y AND cessation_date > 12m ago → EX; If flag=Y AND (no cessation OR < 12m) → SM | Default UN if ambiguous |

---

## Insurance Domain Data Patterns

### Common entities in L&H insurance

| Entity | Key attributes | Notes |
|---|---|---|
| Applicant / Life Assured | Name, DOB, gender, address, occupation, smoking status, height, weight | PII-heavy — GDPR applies |
| Application | Product, sum assured, term, premium type, distribution channel | Links to applicant and policy |
| Medical History | Condition (ICD-10), onset date, severity, treatment, current status | Core underwriting data |
| Risk Assessment | Decision, rating %, exclusions, evidence trail, assessor | Audit-critical |
| Policy | Policy number, status, effective date, expiry, premium schedule | Post-issue lifecycle |
| Claim | Claim type, cause, date of event, reserve, payments, status | Links to policy and claimant |
| Reinsurance Cession | Treaty/fac, cession %, retention, reinsurer, bordereaux ref | Financial and reporting |

### Common reference data

- Product codes and product hierarchy
- Occupation codes (insurer-specific, often mapped to risk class)
- ICD-10 medical condition codes
- Country / territory codes (ISO 3166)
- Currency codes (ISO 4217)
- Distribution channel codes
- Underwriting decision codes
- Claim cause codes

---

## Quality Checklist

- [ ] Every field has a unique ID, business name, and technical name
- [ ] Data types and formats are specified precisely (not just "string" — include length)
- [ ] Validation rules are testable and specific
- [ ] PII fields are flagged with GDPR/data protection implications
- [ ] Enum/reference data tables are complete with all valid values
- [ ] Source-to-target mappings cover all fields (including "unmapped" with rationale)
- [ ] Transformation rules are documented with input, output, logic, and error handling
- [ ] Data ownership is assigned for every entity
- [ ] Migration vs integration mappings are distinguished
- [ ] Insurance-specific patterns are used (ICD-10, occupation codes, product hierarchy)
