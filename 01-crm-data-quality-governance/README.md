# CRM Data Quality & Governance Platform

> **A configurable CRM data-quality engine that profiles customer records, validates critical fields, detects duplicate records, scores data health, and routes records requiring remediation into an operational exceptions queue.**

**Platform:** Microsoft Excel + Power Query + formula-driven quality engine  
**Data:** Synthetic CRM export  
**Records:** 5,130  
**Status:** Portfolio Case Study

---

## 1. Executive Summary

CRM data quality directly affects pipeline reporting, segmentation, sales automation, customer communication, and operational decision-making.

This project builds a repeatable **CRM Data Quality & Governance workflow** rather than relying on manual spreadsheet inspection.

A raw CRM export is processed through configurable quality rules covering:

- Completeness
- Email validity
- Phone validity
- Duplicate detection
- Standardization
- Staleness
- Composite data-quality scoring
- Exception routing
- Refresh logging

The result is an operational workflow:

```text
Raw CRM Export
      ↓
Power Query / Data Preparation
      ↓
Standardization
      ↓
Data Quality Rules
      ↓
Validation & Duplicate Detection
      ↓
Quality Scoring
      ↓
 ┌────┴─────────────┐
 ↓                  ↓
Pass QC          Exceptions
                 for Review
```

The important design choice is that questionable records are **flagged and routed for human remediation rather than silently deleted or automatically merged**.

---

# 2. Business Problem

CRM data problems are rarely isolated.

A missing email can break an outreach workflow.

A duplicate record can distort:

- Customer counts
- Pipeline reporting
- Segmentation
- Revenue attribution

Incomplete records weaken downstream analysis.

Stale records can cause sales teams to spend time on contacts that are no longer commercially relevant.

The business requirement is therefore broader than "clean the spreadsheet."

It is:

> **Create a repeatable process that identifies data-quality risk, makes the risk measurable, and gives an owner a clear remediation queue.**

---

# 3. Solution

The solution combines:

### Data preparation
Power Query is used as part of the data-loading and transformation workflow.

### Configurable rules
Quality thresholds and scoring weights are stored in the `Config` sheet rather than buried inside individual formulas.

### Quality scoring
Each customer record receives a score from 0–100.

### Duplicate detection
Exact matching is performed on valid email and phone values.

### Exception management
Records below the configured quality threshold are routed to the `Exceptions` sheet.

### Governance
The workbook records refresh information and exposes the rules used to determine quality.

---

# 4. Data

The source is a synthetic CRM customer export created to resemble a real operational CRM dataset.

**No real customer data is used.**

| Attribute | Value |
|---|---:|
| Customer records | 5,130 |
| Raw fields | 21 |
| Data type | Synthetic CRM export |
| Primary source | CSV |

The raw dataset contains fields covering:

- Customer identity
- Company
- Email
- Phone
- Job title
- Department
- Industry
- Lead source
- Customer status
- Geography
- Creation date
- Last-contact date
- Assigned sales representative

---

# 5. Data Quality Framework

The engine evaluates four primary data-quality dimensions.

```text
CRM Data Quality
│
├── Completeness
├── Validity
├── Uniqueness
└── Consistency
      ↓
Standardization applied during data preparation
```

## Completeness

A profile is complete when all eight required fields contain meaningful values:

- First Name
- Last Name
- Email
- Phone
- Company
- Job Title
- Country
- City

Placeholder values such as `Unknown`, `Not Available`, `Not Assigned`, `N/A`, and `TBD` are treated as missing for completeness purposes.

## Validity

Email and phone values are tested against explicit validation rules.

## Uniqueness

Potential duplicates are identified using exact matches on valid email and phone values.

## Consistency

Selected values are standardized during data preparation, including email casing and company-name formatting.

---

# 6. Scoring Model

Each record starts with 100 points.

| Issue | Penalty |
|---|---:|
| Invalid email | -30 |
| Invalid phone | -20 |
| Incomplete profile | -40 |
| Potential duplicate | -25 |

The minimum score is 0.

### Exception threshold

The configured minimum acceptable score is:

> **80 / 100**

Records scoring **below 80** are routed to the Exceptions queue.

This distinction matters: an invalid-phone-only record receives 80 points under the current weights and therefore is **not** routed to Exceptions, while records with a score of 79 or below are routed.

---

# 7. Current Run Results

**Run ID:** RUN-0001  
**Refresh date:** August 6, 2026  
**Records processed:** 5,130

| Metric | Result |
|---|---:|
| Complete profiles | 4,659 (90.8%) |
| Incomplete profiles | 471 (9.2%) |
| Valid emails | 4,920 (95.9%) |
| Invalid emails | 210 (4.1%) |
| Valid phones | 5,023 (97.9%) |
| Invalid phones | 107 (2.1%) |
| Potential duplicate records | 946 (18.4%) |
| Stale records | 1,600 (31.2%) |
| Records below threshold | 1,555 (30.3%) |
| Exceptions with no owner | 40 (2.6% of exception queue) |
| Average data-quality score | 90.1 / 100 |

### Important interpretation

The 1,555 exception records are **not the same as the total number of records with any quality issue**.

Under the current scoring model, **92 records with invalid phone numbers only score exactly 80 and therefore pass the "below 80" exception rule**.

This is why issue-condition counts can be greater than the 1,555 exception count.

---

# 8. Issue Conditions vs Exception Queue

The workbook distinguishes between:

### Quality conditions triggered

A record can trigger one or more rules.

| Issue combination | Records |
|---|---:|
| Potential Duplicate only | 859 |
| Incomplete Profile only | 410 |
| Invalid Email only | 199 |
| Invalid Phone only | 92 |
| Incomplete Profile + Potential Duplicate | 61 |
| Invalid Phone + Potential Duplicate | 15 |
| Invalid Email + Potential Duplicate | 11 |
| **Total records with listed issue conditions** | **1,647** |

### Why 1,647 is not the exception count

The 92 records with **Invalid Phone only** receive:

```text
100 - 20 = 80
```

The exception rule is:

```text
Score < 80
```

Therefore those 92 records remain above the exception cutoff.

This distinction is documented intentionally so the validation report can be reconciled mathematically.

---

# 9. Duplicate Detection

The engine uses **exact matching**, not fuzzy matching.

A record is flagged when:

- Its valid email appears on another record, or
- Its valid phone appears on another record.

The engine does **not** automatically merge or delete duplicate records.

Instead:

```text
Detection
   ↓
Flag
   ↓
Route
   ↓
Human Review
   ↓
Business Decision
```

This is deliberate.

Automatically merging CRM records based only on exact-match signals can remove legitimate information or combine accounts incorrectly.

The system therefore treats duplicate resolution as a **data-owner decision**.

---

# 10. Staleness

A record is classified as stale when there has been no contact for **365+ days**, based on the configured threshold.

Staleness is intentionally tracked separately from data correctness.

A record can be:

- Complete
- Valid
- Unique

and still be commercially stale.

Therefore staleness is a **commercial relevance signal**, not automatically a data-quality failure.

---

# 11. Exceptions Queue

Records scoring below 80 are routed to the `Exceptions` sheet.

The queue exposes information needed for remediation, including:

- Customer ID
- Customer name
- Company
- Customer status
- Assigned owner
- Email
- Email status
- Phone
- Phone status
- Completeness
- Duplicate flag
- Quality score

This turns the analysis into an operational workflow:

> **Find the problem → explain the problem → identify the record owner → remediate the record.**

---

# 12. Configuration

The `Config` sheet contains the main quality parameters.

Current configuration includes:

- Email penalty
- Phone penalty
- Incomplete-profile penalty
- Minimum phone digit count
- Exception threshold
- Reference values used by the quality engine

Keeping these parameters outside the scoring formulas makes the model easier to maintain and adapt.

---

# 13. Refresh & Governance

The `Refresh_Log` sheet records the latest processing run.

The current run records:

- Run ID
- Refresh date
- Run owner
- Records processed
- Records passed QC
- Records flagged
- Whether quality calculations were rebuilt
- Refresh notes

This provides a basic audit trail for the data-quality process.

---

# 14. Validation

The current validation run confirms:

- 5,130 records processed
- 3,575 records passed the minimum score
- 1,555 records were routed to Exceptions
- Quality conditions were calculated
- Duplicate detection was applied
- Quality scoring was rebuilt using configurable rules

The full validation output is documented in:

`docs/validation_report.md`

---

# 15. Architecture

```text
                 CRM CSV Export
                       │
                       ▼
              Power Query / Load
                       │
                       ▼
                Standardization
                       │
                       ▼
               Quality Validation
              ┌────────┼─────────┐
              ▼        ▼         ▼
           Email     Phone   Completeness
              │        │         │
              └────────┼─────────┘
                       ▼
                Duplicate Checks
                       │
                       ▼
                 Quality Score
                       │
              ┌────────┴────────┐
              ▼                 ▼
           Score ≥ 80         Score < 80
              │                 │
              ▼                 ▼
          QC Passed         Exceptions
                                │
                                ▼
                          Human Review
```

---

# 16. Technical Notes

The workbook uses:

- Microsoft Excel
- Power Query
- Formula-driven data-quality calculations
- Configurable thresholds
- Excel tables
- Validation outputs
- Refresh logging

### Macro-enabled workbook note

The working solution is maintained as an Excel macro-enabled workbook (`.xlsm`) because the broader workflow uses VBA.

**Important:** the specific uploaded copy should be checked before publication to ensure the VBA project is actually embedded in the final file. The uploaded package inspected for this review contains the Power Query connection structures, but does not expose a standard `vbaProject.bin` component. Do not claim embedded VBA in the public repository unless the final published workbook contains the actual macro project.

---

# 17. Limitations

This project uses synthetic data.

Therefore:

- It does not represent a real company's CRM.
- The validation results are not production business outcomes.
- Exact-match duplicate detection will miss some fuzzy or indirect duplicates.
- Staleness does not prove that a customer is commercially inactive.
- Quality penalties are configurable business rules, not universal standards.
- A score of 80 is a policy threshold, not an objective definition of "good data."
- Production deployment would require ownership, governance, monitoring, and integration with the organization's CRM.

---

# 18. Future Extension

A separate operational dashboard could be built on top of the current engine.

Potential components:

- CRM Health Score
- Duplicate Rate
- Completeness
- Invalid-record rate
- Exception queue
- Quality by customer status
- Quality by owner
- Issue distribution
- Multi-run quality trend

This is an **optional next layer**, not a requirement for the current project.

The core solution is the quality engine and remediation workflow.

---

# 19. Repository Structure

```text
CRM-Data-Quality-Governance/
│
├── README.md
│
├── CRM_Data_Quality_ETL.xlsm
│
├── data/
│   └── raw/
│       └── crm_customers_dirty.csv
│
└── docs/
    ├── data_dictionary.md
    ├── data_quality_rules.md
    └── validation_report.md
```

---

## What This Project Demonstrates

This project demonstrates the ability to turn a messy CRM export into a governed data-quality workflow:

**Raw data**

→ **profiling**

→ **standardization**

→ **validation**

→ **scoring**

→ **duplicate detection**

→ **exception routing**

→ **human remediation**

→ **governance**

The value is not the spreadsheet itself.

The value is creating a **repeatable mechanism for making CRM data trustworthy enough to support reporting, segmentation, and automation.**
