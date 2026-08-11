# HR Employee Master — Data Dictionary

| Field | Meaning | Source | Treatment |
|---|---|---|---|
| EmployeeID | Unique employee identifier | Payroll | Deduplicated |
| Employee Name | Employee name | Payroll | Anonymized in public package |
| Department | Employee department | Payroll | Standardized |
| Salary (NGN) | Salary amount | Payroll | Numeric |
| Bonus (NGN) | Bonus amount | Payroll | Numeric |
| PAYE Tax (NGN) | PAYE deduction | Payroll | Nulls retained/flagged |
| Total Attendance Records | Attendance record count | Attendance | Aggregated by employee |
| Total Hours Worked | Total recorded hours | Attendance | Aggregated |
| Attendance Rate | Attendance ratio | Attendance | Calculated |
| Total Leave Days | Total leave days | Leave | Aggregated |
| Number of Leave Requests | Leave request count | Leave | Counted |
| Performance Score | Latest review score | Performance | Not Reviewed if no review |
| Manager | Reporting manager | Performance | Anonymized in public package |
| Rating | Review category | Performance | Not Reviewed where no review exists |
