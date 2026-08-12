# HR Workforce ETL & Executive Analytics

**An Excel and Power Query workforce reporting system that brings payroll, attendance, leave and performance data into one controlled employee view, while exposing the HR records that still need attention.**

**Stack:** Excel, Power Query, Power Pivot, PivotTables  
**Employees:** 1,001  
**Source records:** 17,216 across four HR datasets

---

## The business problem

HR decisions are difficult when the underlying employee data is spread across separate files.

Payroll may contain duplicate employees. Attendance and leave records may reference people who are not in the employee master. Performance reviews may be missing. Some employees may have no assigned manager.

A dashboard can hide these problems. This project is designed to expose them before they affect workforce decisions.

The workflow is:

```text
Payroll ───────┐
Attendance ────┤
Leave ─────────┼──> Power Query ETL
Performance ───┘          ↓
                    Employee Master
                          ↓
                Quality Checks + KPIs
                          ↓
                  Executive Dashboard
