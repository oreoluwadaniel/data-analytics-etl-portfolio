# Power Query Refresh Runbook

## Source order

Load:

1. Payroll
2. Attendance
3. Leave
4. Performance

## Required transformations

### Payroll
- trim text
- standardize department names
- remove duplicate EmployeeID rows
- retain missing PAYE Tax as a quality exception
- validate EmployeeID

### Attendance
- parse mixed date formats
- validate EmployeeID
- aggregate records and hours by employee
- calculate attendance rate using the documented status rule

### Leave
- validate EmployeeID
- aggregate leave days and request count

### Performance
- sort by EmployeeID + Review Date
- keep latest review per employee
- identify employees with no review
- preserve missing Manager as an exception

### Merge

Use Payroll EmployeeID as the employee master key.

Merge the aggregated Attendance, Leave, and latest Performance tables onto the unique Payroll employee list.

## Quality gate

Do not publish the refresh until:

- EmployeeID is unique
- unknown attendance/leave IDs are reviewed
- department values are standardized
- PAYE Tax exceptions are understood
- Not Reviewed employees are correctly classified
- manager coverage is reconciled

## Dashboard validation

After refresh, reconcile:

- employee count
- total payroll
- bonus
- PAYE
- attendance
- leave
- reviewed performance
- manager coverage

against the Employee_Master table.
