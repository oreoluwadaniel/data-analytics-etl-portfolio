# HR Workforce ETL — Case Study

## Problem

HR information was split across four operational workbooks:

- Payroll
- Attendance
- Leave
- Performance

A management team needs one employee-level view without manually reconciling the files each reporting cycle.

## Solution

I designed a Power Query ETL workflow that:

1. extracts the four sources;
2. standardizes fields;
3. removes duplicate payroll employee records;
4. aggregates attendance;
5. aggregates leave;
6. selects the latest performance review;
7. joins the datasets at employee level;
8. validates data-quality exceptions;
9. feeds an executive workforce dashboard.

## What the source data revealed

The source data contained:

- 1,016 payroll rows representing 1,001 unique employees;
- 15 duplicate payroll rows;
- 81 attendance rows with unknown employee IDs;
- 8 leave rows with unknown employee IDs;
- 39 missing PAYE Tax values;
- 28 missing payroll departments;
- 301 employees without performance reviews;
- 464 employees without assigned managers.

These are not cosmetic issues. They affect HR reporting accuracy and management accountability.

## Business output

The resulting employee master and dashboard provide:

- workforce size
- payroll cost
- bonus cost
- PAYE tax
- attendance performance
- leave utilization
- reviewed performance
- manager coverage
- department workforce structure
- data-quality action items

## Key design principle

The dashboard distinguishes between:

**missing data**

and

**negative business performance**.

For example, an employee without a performance review is:

> `Not Reviewed`

not:

> `Performance Score = 0`.

This keeps the KPI analytically defensible.

## Portfolio boundary

This is a synthetic portfolio case study and does not claim implementation at a real HR organization.
