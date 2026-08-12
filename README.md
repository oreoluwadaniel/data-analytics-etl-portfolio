# Data Analytics & ETL Portfolio - Daniel Olatunji

Four Excel and Power Query ETL projects. Each starts with a messy business export and turns it into a reporting model with checks for bad records, missing links, and numbers that do not reconcile.

I'm a data analyst based in Lagos, Nigeria. I work mainly with Excel, Power Query, Power Pivot, DAX, SQL, and Python. The data here is synthetic, but the problems are common: duplicate records, broken keys, missing owners, and reports that look fine until you check the source row by row.

**Contact:** danolatunji25@gmail.com

## The four projects

| # | Project | What it deals with | Scale | Stack |
|---|---|---|---:|---|
| 01 | [CRM Data Quality & Governance](01-crm-data-quality-governance/) | Score customer records, flag records that need review, and avoid automatic merges | 5,130 records, 30.3% routed to exceptions | Excel, Power Query |
| 02 | [HR Workforce ETL](02-hr-workforce-etl/) | Bring payroll, attendance, leave, and performance into one employee view without hiding missing information | 1,001 employees, 301 without a review, 464 without a manager | Excel, Power Query, Power Pivot |
| 03 | [Inventory ETL Automation](03-inventory-etl-automation/) | Turn warehouse data into a replenishment list backed by 15 integrity checks | 3,400 SKUs, N6.49B replenishment exposure | Excel, Power Query, VBA |
| 04 | [Sales Reporting ETL](04-sales-reporting-etl/) | Combine 13 branches into a reporting model with checks before the numbers reach management | 75,000 transactions, 74,598 after cleaning | Excel, Power Query, Power Pivot, DAX, VBA |

Each folder has the workbook, source data, and documentation covering the model, data fields, quality checks, and operating steps where needed.

## What kept coming up

The same problem showed up in every department: **the numbers don't add up, and nobody knows why.**

CRM data can overstate a pipeline when duplicate leads are counted twice. HR reports become misleading when an employee without a review is treated as having a score of zero. Inventory reports become dangerous when negative stock is printed as if it were normal. Sales reports can include transactions that fall outside the reporting period.

The workflow I used is simple:

```text
Raw export -> profile -> validate -> score problems -> route exceptions -> build reporting layer
```

I don't silently overwrite records just because they look wrong. A duplicate contact, negative stock balance, and future-dated sale are different problems. Each one needs to be checked before someone decides what to do with it.

## What the projects show

- Data-quality rules and exception queues
- Star-schema and employee master data models
- Power Query transformations and DAX measures
- VBA refresh and audit steps
- Data dictionaries, architecture notes, and quality findings
- Clear documentation of cases where the first number was wrong or incomplete

The point is not to make every report look clean. It is to know which numbers can be trusted, which need review, and why.

## How each project is laid out

```text
0X-project-name/
|-- README.md
|-- workbook.xlsm/.xlsx
|-- data/
`-- docs/
    |-- ARCHITECTURE.md
    |-- CASE_STUDY.md
    |-- DATA_DICTIONARY.md
    |-- DATA_QUALITY_FINDINGS.md
    `-- RUNBOOK.md
```

Start with the project README, then open the workbook if you want to see the Power Query steps, DAX measures, or VBA refresh process.

## About the data

All datasets are synthetic. They are shaped like CRM, payroll, warehouse, and sales exports but contain no real customer, employee, or company records. The defects are intentional so the validation work can be tested.

## About me

I'm Daniel Olatunji, a data analyst working across Excel, Power Query, Power BI, SQL, and Python. My main focus is data quality, ETL, and reporting systems for business operations.

If you want to discuss any of these builds, including the parts I had to correct, reach me at **danolatunji25@gmail.com**.

See also: [Everdale Retail Analytics](https://github.com/oreoluwadaniel/everdale-retail-analytics) and [Kavora CRM Migration & Data Governance](https://github.com/oreoluwadaniel/kavora-crm-migration-data-governance).
