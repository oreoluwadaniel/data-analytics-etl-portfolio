# HR ETL — Data Quality Findings

## Findings from source inspection

| Issue | Count | Treatment |
|---|---:|---|
| Duplicate payroll EmployeeIDs | 15 rows | Deduplicate |
| Missing payroll Department | 28 | Repair/standardize source |
| Missing PAYE Tax | 39 | Verify payroll source |
| Attendance rows with unknown EmployeeID | 81 | Quarantine/resolve |
| Leave rows with unknown EmployeeID | 8 | Quarantine/resolve |
| Employees without performance review | 301 | Mark Not Reviewed |
| Employees without manager | 464 | Resolve ownership |
| Employees with unspecified department in master | 27 | Correct source data |

## Important analytical correction

Missing performance is **not** equivalent to a score of zero.

The dashboard therefore reports:

> `Not Reviewed`

separately and calculates the reviewed performance average only across employees with a review.

## Quality-gate recommendation

Before a production refresh:

1. Validate EmployeeID uniqueness.
2. Resolve unknown attendance/leave IDs.
3. Repair department values.
4. Verify PAYE Tax nulls.
5. Assign managers.
6. Confirm performance-review coverage.
7. Refresh the Employee Master.
8. Reconcile dashboard totals.

The portfolio should demonstrate this as:

```text
Source
 ↓
Quality checks
 ↓
Exceptions
 ↓
Correction
 ↓
Refresh
 ↓
Reconciliation
```
