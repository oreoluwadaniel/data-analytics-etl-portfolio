# Data Analytics & ETL Portfolio - Daniel Olatunji

Four Excel/Power Query ETL builds. Each one takes a messy, real-world-shaped export (CRM, HR, warehouse inventory, multi-branch sales) and turns it into a governed reporting model with data-quality controls built in from the start, not bolted on afterward.

I'm a data analyst based in Lagos, Nigeria, working mostly in Excel, Power Query, Power Pivot, DAX, and VBA. The projects below use synthetic data, no real customer, employee, or company records, but the data-quality problems in them are ones I've actually run into on client and employer work: duplicate records, broken foreign keys, missing owners, numbers that don't reconcile until you track down the one row causing it.

**Contact:** oluwafikayore@gmail.com

---

## What's in here

| # | Project | Core problem | Scale | Stack |
|---|---|---|---:|---|
| 01 | [CRM Data Quality & Governance](01-crm-data-quality-governance/) | Score every customer record, flag the ones that need a human, don't auto-merge duplicates | 5,130 records, 30.3% routed to exceptions | Excel, Power Query, formula-driven scoring engine |
| 02 | [HR Workforce ETL](02-hr-workforce-etl/) | Consolidate payroll, attendance, leave, and performance into one employee master without hiding the gaps | 1,001 employees, 301 without a review, 464 without a manager | Excel, Power Query, Power Pivot |
| 03 | [Inventory ETL Automation](03-inventory-etl-automation/) | Turn a warehouse export into a prioritized replenishment view, backed by 15 automated integrity checks | 3,400 SKUs, N6.49B replenishment exposure identified | Excel, Power Query, VBA |
| 04 | [Sales Reporting ETL](04-sales-reporting-etl/) | Consolidate 13 branches into a star-schema model an exec dashboard can actually trust | 75,000 transactions, 74,598 after cleaning, 13 branches | Excel, Power Query, Power Pivot, DAX, VBA |

Each folder is a self-contained case study: the workbook, the source data, and a `docs/` folder with the architecture, the data dictionary, the data-quality findings, and (where relevant) a runbook for how to operate it.

---

## The thread connecting all four

Every one of these started from the same complaint, just in a different department: "the numbers don't add up and nobody's sure why."

CRM data breaks pipeline reporting when duplicate leads inflate the funnel. HR data breaks headcount reporting when 301 employees have no performance review and someone reports their score as zero instead of "not reviewed." Inventory data breaks procurement planning when 51 SKUs show negative stock and the report just prints the number instead of flagging it. Sales data breaks executive reporting when 735 transactions are dated after the reporting period closed and nobody catches it before the numbers go into a deck.

The fix takes the same shape every time, even though the domain changes:

```text
Raw export -> profiling -> validation rules -> quality scoring -> exception routing -> governed reporting layer
```

None of these four projects quietly "cleans" data by overwriting or deleting what looks wrong. Records that fail a rule get flagged, scored, and routed to a queue for a person to decide, because a duplicate CRM contact, a negative stock count, and a forward-dated sale all deserve a human decision, not a silent fix that might be wrong.

---

## What this demonstrates

- **Data-quality engineering:** configurable rule engines, composite scoring, exception queues, and refresh logging, applied consistently across four different domains
- **Data modeling:** star-schema design (facts/dimensions), employee master-record consolidation, foreign-key integrity checks
- **Power Query & DAX:** multi-source ingestion, transformation, deduplication, and calculated measures for executive reporting
- **VBA automation:** refresh orchestration and audit trails for the inventory and sales workbooks
- **Documenting the messy parts:** every case study covers its own limitations and edge cases, like why 92 CRM records sit exactly at the exception threshold and don't get flagged, or why 735 sales transactions fall outside the stated reporting period, instead of presenting clean-looking numbers that fall apart under a follow-up question

Anyone can build a dashboard that looks polished. Knowing where your own numbers might mislead someone, and writing that down before they ask, is the part that's harder to fake.

---

## How to explore a project

Every project folder follows the same layout:

```text
0X-project-name/
|-- README.md              (the case study: problem, solution, results, business value)
|-- workbook.xlsm/.xlsx    (the actual Excel/Power Query/VBA build)
|-- data/                  (sanitized source and/or processed data)
`-- docs/
    |-- ARCHITECTURE.md          (the pipeline, end to end)
    |-- CASE_STUDY.md            (business framing and findings)
    |-- DATA_DICTIONARY.md       (field-level definitions)
    |-- DATA_QUALITY_FINDINGS.md (what the quality checks actually caught)
    `-- RUNBOOK.md               (how to operate the workbook, where applicable)
```

Start with the project README for the story, then open the workbook if you want to see the Power Query steps, the DAX measures, or the VBA behind the refresh button.

---

## About the data

Every dataset in this repository is synthetic, built to resemble real operational exports (CRM, payroll, warehouse, point-of-sale) without containing any real customer, employee, or company information. Where the source data includes intentional defects (duplicate IDs, missing fields, invalid formats, forward-dated records), that's by design. It's what makes the data-quality layer worth building in the first place.

---

## About me

I'm Daniel Olatunji, a data analyst working across Excel, Power Query, Power BI, SQL, and Python, with a focus on data quality, ETL, and reporting automation for CRM, HR, inventory, and sales operations. If you're hiring for a data analyst, BI developer, or analytics engineer role and want to talk through any of these builds, including the parts that didn't work on the first try, reach me at **oluwafikayore@gmail.com**.
