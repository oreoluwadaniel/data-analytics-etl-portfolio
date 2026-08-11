# Sales ETL Architecture

```text
Regional CSV exports
        ↓
Power Query
        ↓
Cleaning + validation
        ↓
fct_Sales_Clean
        ↓
Dimensions
        ↓
Power Pivot / PivotTables
        ↓
DAX + calculations
        ↓
Executive Dashboard
        ↓
VBA refresh orchestration
```

The cleaned fact table is the reporting source. The raw fact export is a quality/audit source and should not drive management KPIs.
