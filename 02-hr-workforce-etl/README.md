# HR Workforce ETL & Executive Analytics

> **An Excel/Power Query HR data-integration solution that consolidates payroll, attendance, leave, and performance data into a governed employee master table and an executive workforce dashboard.**

**Data:** Synthetic portfolio dataset  
**Primary stack:** Excel, Power Query, Power Pivot/PivotTables, Excel dashboarding

---

## 1. Business problem

HR data often arrives from separate operational processes:

- Payroll
- Attendance
- Leave
- Performance management

When these files are consolidated manually, HR leaders face:

- inconsistent employee identifiers
- duplicate payroll records
- inconsistent department labels
- missing manager ownership
- incomplete performance coverage
- missing payroll fields
- broken attendance/leave references

The project creates a repeatable ETL workflow:

```text
Payroll ─────┐
Attendance ──┤
Leave ───────┼──> Power Query ETL ──> Employee Master ──> Executive Dashboard
Performance ─┘
```

---

## 2. What the solution does

### Extract
Imports four HR source workbooks.

### Transform
- standardizes column names
- trims text
- standardizes departments
- normalizes dates
- deduplicates payroll employee records
- aggregates attendance
- aggregates leave
- selects the latest performance review
- creates an employee-level master table

### Validate
Checks:

- duplicate employee IDs
- missing departments
- missing PAYE tax
- unknown employee IDs
- missing performance reviews
- missing managers

### Present
Produces an executive dashboard covering:

- workforce size
- payroll
- bonus
- PAYE tax
- attendance
- leave
- performance
- manager coverage
- department distribution
- action items

---

## 3. Source data

| Source | Rows | Role |
|---|---:|---|
| Payroll | 1,016 | Employee/payroll master |
| Attendance | 15,000 | Attendance and hours |
| Leave | 500 | Leave requests/days |
| Performance | 700 | Review scores and managers |

The payroll source contains **1,016 rows but 1,001 unique EmployeeIDs**, meaning 15 duplicate payroll rows require deduplication.

---

## 4. Data-quality findings

The source data contains deliberate/realistic quality defects.

### Duplicate payroll rows

**15 duplicate EmployeeID rows** exist in the payroll source.

The corrected workflow reduces these to the 1,001 unique employee records used by the master table.

### Broken attendance references

**81 attendance rows** reference employee IDs absent from the payroll employee master.

These should be treated as source-data exceptions, not silently assigned to another employee.

### Broken leave references

**8 leave rows** reference employee IDs absent from payroll.

### Missing payroll fields

- **28** payroll records have missing Department values.
- **39** payroll records have missing PAYE Tax values.

### Performance coverage

There are **700 performance records for 1,001 employees**.

Therefore:

> **301 employees have no performance review record.**

They should be classified as **Not Reviewed**, not as performance score zero.

### Manager coverage

The final employee master identifies:

> **464 employees without an assigned manager.**

That is a governance/action item, not merely a dashboard statistic.

---

## 5. Key dashboard figures

The current reconciled employee master contains:

- **1,001 employees**
- **₦531.6M total salary**
- **₦46.1M total bonus**
- **₦56.2M PAYE tax**
- **3,869 leave days**
- **74.5% average attendance**
- **77.3 average performance among reviewed employees**
- **301 employees not reviewed**
- **464 employees without managers**
- **27 employees with unspecified departments**

The performance average is explicitly calculated only for reviewed employees.

---

## 6. Business value

The solution helps HR leadership answer:

### Workforce governance
Where are employee records incomplete?

### Performance management
How many employees have not yet received a review?

### Manager accountability
How many employees lack a reporting manager?

### Attendance
Which departments are below the attendance target?

### Compensation
Which departments carry the largest payroll cost?

### HR data quality
Which source systems require correction before downstream reporting?

The dashboard therefore functions as a **workforce-control view**, not simply a collection of charts.

---

## 7. Important modeling decision

The project does **not** treat missing performance as zero performance.

Instead:

```text
No review record
       ↓
Not Reviewed
       ↓
Excluded from reviewed-performance average
```

This prevents the common analytical error of treating missing observations as poor performance.

---

## 8. Portfolio evidence

The public repository should contain:

1. sanitized source workbooks
2. corrected employee master
3. public dashboard workbook
4. data dictionary
5. data-quality findings
6. architecture diagram
7. dashboard screenshots
8. Power Query screenshots
9. a short case study

---

## 9. Public-data boundary

All portfolio data is synthetic.

Direct employee names are anonymized in the public package.

Do not publish:

- real employee data
- personal emails
- phone numbers
- addresses
- payroll identifiers tied to real people
- private HR documents

---

## 10. Positioning

The strongest portfolio description is:

> **Built an Excel/Power Query HR ETL pipeline that integrated 1,001 employee records across payroll, attendance, leave, and performance sources, introduced data-quality controls, and produced an executive workforce dashboard for payroll, attendance, performance, and HR governance.**
