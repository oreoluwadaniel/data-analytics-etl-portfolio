# HR ETL Architecture

```text
Payroll ────────┐
                │
Attendance ─────┤
                │
Leave ──────────┼──> Power Query ──> Quality Checks
                │                         │
Performance ────┘                         ▼
                                  Employee Master
                                         │
                                         ▼
                                Executive Dashboard
```

## Data grain

The final Employee_Master table is:

> **one row per unique EmployeeID**

Attendance and leave are first aggregated to employee level.

Performance is reduced to the latest review per employee.

This prevents many-to-many duplication when the sources are merged.
