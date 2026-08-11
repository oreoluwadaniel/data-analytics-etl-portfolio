# Automated Sales ETL & Executive Reporting

An Excel BI solution that consolidates multi-branch sales exports, applies data-quality controls, builds a star-schema reporting model, and delivers executive reporting through Power Query, Power Pivot, DAX and VBA.

**Source:** 75,000 transactions | **Clean reporting table:** 74,598 rows | **Customers:** 3,500 | **Products:** 60 | **Branches:** 13

## Business problem
Branch-level sales exports create repeated consolidation, validation and reporting work. The solution turns those feeds into a controlled reporting layer and refreshable management dashboard.

## Architecture
```text
Regional CSVs → Power Query → Cleaning/Validation → Fact + Dimensions
→ Power Pivot/Pivots → DAX/Calculations → Executive Dashboard → VBA Refresh
```

## Data-quality controls
The source contains intentional defects: duplicate Order IDs, future dates, invalid quantities, excessive discounts, missing dimensions, invalid regions/payment methods, whitespace issues and invalid currency codes.

The current scorecard reports 13 explicit rules. Failures are rule-level counts and are not additive.

## Important corrections
The raw source contains 75,000 rows; the cleaned reporting table contains 74,598. The dashboard should use the cleaned table for management KPIs.

The stated dataset period ends March 2026, but 735 source transactions occur after that period, through September 17, 2026. These are forward-dated test records unless the reporting period is formally extended.

Transaction count does not prove customer retention; retention requires customer-level repeat-purchase/cohort analysis.

## Portfolio positioning
> Built an automated Excel sales-reporting pipeline that consolidated 75K multi-branch transactions into a governed reporting model, applied 13 data-quality controls, and delivered executive sales intelligence through Power Query, Power Pivot, DAX and VBA.
