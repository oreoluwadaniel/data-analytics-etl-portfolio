# Data Analytics & ETL Portfolio

**Four business-focused Excel and Power Query projects that turn messy operational exports into controlled, reviewable reporting systems.**

A spreadsheet can produce a polished dashboard and still be wrong.

A duplicate customer can inflate a CRM pipeline. A missing manager can distort a workforce report. Negative stock can hide an inventory problem. A future-dated sale can make revenue look stronger than it is.

These projects focus on the part that happens before the dashboard: **getting the data into a state where the numbers can actually be trusted.**

The common workflow is:

```text
Raw business data
      ↓
Profile & validate
      ↓
Identify data issues
      ↓
Route exceptions
      ↓
Transform & model
      ↓
Build reporting layer
      ↓
Decision-ready information
```

---

## The Four Projects

| #      | Project                                                          | Business Problem                                                                                       |                   Scale |
| ------ | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ----------------------: |
| **01** | [CRM Data Quality & Governance](01-crm-data-quality-governance/) | Identify unreliable customer records and route them for review before they affect sales reporting      |       **5,130 records** |
| **02** | [HR Workforce ETL](02-hr-workforce-etl/)                         | Combine payroll, attendance, leave and performance data without hiding missing employee information    |     **1,001 employees** |
| **03** | [Inventory ETL Automation](03-inventory-etl-automation/)         | Turn warehouse data into a controlled replenishment process and identify stock exposure                |          **3,400 SKUs** |
| **04** | [Sales Reporting ETL](04-sales-reporting-etl/)                   | Combine 13 branch datasets into one reporting model with validation before management sees the numbers | **75,000 transactions** |

Each project includes the source data, workbook, transformation logic, data-quality checks, documentation and operating instructions where required.

---

## What These Projects Solve

### CRM

**Problem:** Duplicate and incomplete customer records can distort pipeline and customer reporting.

**Solution:** Score records, identify exceptions and separate records requiring human review from records that can safely continue through the process.

**Result:** **30.3% of 5,130 records were routed for exception handling.**

---

### HR

**Problem:** Payroll, attendance, leave and performance information often sits in separate files, making it difficult to build one reliable employee view.

**Solution:** Combine the datasets into a controlled employee model while keeping missing information visible instead of replacing it with misleading values.

**Result:** **301 employees had no performance review and 464 had no recorded manager.**

Those are not zeros. They are management exceptions.

---

### Inventory

**Problem:** Warehouse reports can show stock levels without telling the business which products actually require action.

**Solution:** Transform inventory data into a replenishment view backed by **15 integrity checks**, including stock and master-data validation.

**Result:** **3,400 SKUs with N6.49B in replenishment exposure.**

The purpose is not simply to show inventory. It is to identify where purchasing attention is required.

---

### Sales

**Problem:** Branch-level sales files can contain inconsistent records, making consolidated reporting unreliable.

**Solution:** Standardize and combine **13 branches** into a single reporting model with validation checks before the data reaches management.

**Result:** **75,000 source transactions reduced to 74,598 valid reporting records after cleaning.**

Every excluded record has a reason.

---

## The Principle Behind the Work

I do not treat data cleaning as "make the spreadsheet look right."

A bad record should not quietly disappear.

A duplicate, missing owner, negative stock balance and future-dated transaction represent different business problems. They should be identified, classified and handled differently.

That is why these projects use:

* Data profiling and validation
* Exception queues
* Power Query transformations
* Power Pivot data models
* DAX measures
* VBA refresh and audit processes
* Data dictionaries and quality documentation
* Reconciliation checks before reporting

The objective is simple:

> **Know which numbers are safe to use, which need review, and why.**

---

## What This Portfolio Demonstrates

**Data quality:** Finding problems before they reach management reports.

**ETL:** Turning inconsistent business exports into repeatable reporting datasets.

**Data modeling:** Building structured models that support reliable analysis instead of repeated manual manipulation.

**Reporting:** Connecting cleaned data to meaningful business measures.

**Governance:** Keeping exceptions visible instead of silently changing or deleting questionable records.

**Automation:** Reducing repetitive refresh and validation work through Power Query and VBA.

---

## Repository Structure

```text
0X-project-name/
├── README.md
├── workbook.xlsm / workbook.xlsx
├── data/
└── docs/
    ├── ARCHITECTURE.md
    ├── CASE_STUDY.md
    ├── DATA_DICTIONARY.md
    ├── DATA_QUALITY_FINDINGS.md
    └── RUNBOOK.md
```

Start with each project README for the business problem and findings. Open the workbook to inspect the transformations, data model, DAX measures and automation.

---

## Data

All datasets are synthetic.

They are deliberately structured to resemble CRM, HR, inventory and sales exports, including the kinds of inconsistencies that require validation before reporting. No real customer, employee or company records are included.

---
