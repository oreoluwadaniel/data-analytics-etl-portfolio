# Sales ETL — Business Case

## Challenge
Management receives multiple regional sales exports. Manual consolidation creates risks around duplicates, invalid dates, inconsistent attributes and KPI reconciliation.

## Solution
Power Query handles ingestion/transformation; the cleaned fact table is joined to customer, product, salesperson, branch, region and calendar dimensions; Power Pivot/Pivots and DAX provide reporting; VBA orchestrates desktop refresh.

## Business value
The solution creates a repeatable reporting layer for revenue, regional, branch, category, product and customer analysis while making source-data defects visible.

## Analytical discipline
The original narrative overstated customer retention. Transaction volume alone cannot establish repeat purchasing. A valid retention analysis would require cohort/repeat-order logic.

## Scope
Synthetic portfolio data; desktop Excel implementation. No claim of cloud deployment or measured client ROI.
