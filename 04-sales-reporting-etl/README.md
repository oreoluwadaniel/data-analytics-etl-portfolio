# Automated Sales ETL & Executive Reporting

**A controlled Excel reporting system that turns 75,000 multi-branch sales records into one validated dataset and a management-ready view of sales performance.**

## The business problem

When 13 branches send sales data in separate exports, consolidation quickly becomes a reporting problem.

Different formats, duplicate orders, invalid dates, missing fields and inconsistent values can all make their way into the final report. A dashboard built on that data may look professional while reporting the wrong numbers.

This project addresses the problem from the source: **validate the data first, then build the reporting layer.**

## What the solution does

```text
Branch CSVs
    ↓
Power Query
    ↓
Clean + Validate
    ↓
Fact & Dimension Model
    ↓
Power Pivot + DAX
    ↓
Executive Reporting
    ↓
VBA Refresh
```

The result is a repeatable reporting process rather than a workbook that has to be manually rebuilt every reporting cycle.

### Scale

* **75,000** source transactions
* **74,598** records in the cleaned reporting table
* **3,500** customers
* **60** products
* **13** branches

---

## Data quality comes before the dashboard

The source data contains deliberate issues that a real sales pipeline would need to catch:

* Duplicate Order IDs
* Future-dated transactions
* Invalid quantities
* Excessive discounts
* Missing dimension values
* Invalid regions and payment methods
* Whitespace inconsistencies
* Invalid currency codes

The pipeline applies **13 explicit validation rules** and records failures at rule level.

The rules are not simply added together because one transaction can fail more than one check.

That distinction matters when management is deciding whether a data problem is isolated or systemic.

---

## Two findings that change how the report should be used

**75,000 source rows do not mean 75,000 valid sales records.**

After cleaning and validation, the reporting table contains **74,598 rows**. Management KPIs therefore need to run from the cleaned reporting layer, not the raw exports.

**The reporting period also needs attention.**

The stated dataset period ends in March 2026, but **735 source transactions are dated after that period, with the latest reaching September 17, 2026.**

Those records should be treated as forward-dated test data unless the official reporting period is extended.

I would rather flag that issue than let a dashboard quietly mix historical sales with future-dated records.

---

## What the business gets

This is more than a sales dashboard.

It gives the business a controlled path from branch-level exports to management reporting:

**Finance** gets a consistent sales base.

**Sales leadership** gets comparable branch and product reporting.

**Operations** gets visibility into data exceptions before they affect decisions.

**Management** gets a refreshable reporting layer instead of manually consolidated spreadsheets.

---

## Important reporting boundary

A transaction count is not a customer retention metric.

Knowing how many transactions occurred does not tell management how many customers returned, how frequently they purchased, or whether retention improved.

Those questions require customer-level repeat-purchase and cohort analysis, which should be added as a separate analytical layer rather than inferred from transaction totals.

---

## Tools

**Excel | Power Query | Power Pivot | DAX | VBA**

Power Query handles ingestion and transformation. Power Pivot provides the reporting model. DAX drives business calculations, while VBA handles the refresh process.

---

## Portfolio value

> **Built an automated Excel sales reporting pipeline that consolidated 75K multi-branch transactions into a controlled reporting model, applied 13 data-quality checks, and delivered refreshable executive reporting through Power Query, Power Pivot, DAX and VBA.**
