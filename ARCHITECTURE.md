# ETL Architecture

The repository contains four ETL case studies. Each follows the same operating pattern.

```text
Source files
    |
    v
Profile and validate
    |
    +--> completeness
    +--> uniqueness
    +--> data types
    +--> business-rule checks
    |
    v
Power Query transformations
    |
    +--> clean
    +--> standardize
    +--> derive
    +--> route exceptions
    |
    v
Power Pivot / analytical model
    |
    v
DAX measures and reporting
    |
    v
Business decision
```

## Case studies

- CRM data quality and governance
- HR workforce ETL
- Inventory ETL and automation
- Sales reporting ETL

The project treats exceptions as part of the data process. Records that fail a rule are identified and documented instead of being silently removed.

## Portfolio use

This repository is the main evidence for Excel, Power Query, Power Pivot, DAX, data quality, and ETL work in the account.
