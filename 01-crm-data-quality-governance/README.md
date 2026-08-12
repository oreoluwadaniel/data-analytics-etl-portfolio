# CRM Data Quality & Governance Platform

**An Excel and Power Query data-quality system that turns a messy CRM export into a scored, validated and actionable customer database.**

**Stack:** Excel, Power Query, formula-driven quality engine  
**Records:** 5,130  
**Exception queue:** 1,555 records  
**Average quality score:** 90.1 / 100

---

## The business problem

CRM data problems do not stay inside the CRM.

A missing email can break an outreach workflow.  
A duplicate customer can inflate pipeline reporting.  
An incomplete record can weaken segmentation.  
A stale contact can waste sales time.

The problem is not simply finding bad records. The business needs to know **which records need attention, why they need it, and who should fix them.**

This project turns that into a repeatable workflow:

```text
CRM Export
    ↓
Power Query
    ↓
Standardize & Validate
    ↓
Duplicate Detection
    ↓
Quality Score
    ↓
┌───────────────┬────────────────┐
│ Score ≥ 80    │ Score < 80     │
│ Pass QC       │ Exception Queue│
└───────────────┴────────────────┘
                         ↓
                    Human Review
