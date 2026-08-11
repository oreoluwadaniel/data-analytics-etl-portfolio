# Enterprise Inventory ETL — Case Study

## Business challenge

Inventory reporting becomes unreliable when warehouse exports contain conflicting quantities, missing master-data fields, expired items, and inconsistent operational flags.

A useful inventory system therefore needs two layers:

1. **trust the data**
2. **prioritize the action**

This project addresses both.

## Solution

A VBA-driven Excel ETL workflow loads the inventory export into a structured table and feeds:

- automated data-quality checks
- inventory valuation
- replenishment prioritization
- supplier concentration
- warehouse analysis
- operational drill-down
- executive reporting

## Data-quality findings

The current synthetic dataset contains:

- 51 negative-stock records
- 51 reserved-quantity violations
- 51 available-quantity mismatches
- 102 missing reorder levels
- 102 missing barcodes
- 85 missing supplier names
- 84 expired-but-active records
- 278 overstock records
- 38 discontinued items still flagged for reorder

The important design choice is that these issues are **surfaced rather than silently corrected**.

## Decision-support layer

The system converts inventory data into a procurement-oriented view.

For example:

```text
Reorder shortfall
        ×
Unit cost
        =
Estimated replenishment cost
```

Across the current dataset, the estimated cost to restore available inventory to reorder levels is approximately:

**₦6.49B**

This metric should be interpreted as a replenishment-cost exposure, not lost-revenue prediction.

## Business value

The solution helps an inventory manager answer:

- What needs attention first?
- Where is stock risk concentrated?
- Which warehouse holds the most value?
- Which suppliers represent the largest exposure?
- How much procurement spend could be required to restore reorder levels?
- Which data-quality problems need source-system correction?

## Limitation

No sales/consumption history is available.

Therefore the solution deliberately does not claim to perform demand forecasting or inventory-turn optimization.

Adding historical consumption would allow:

- days of supply
- demand velocity
- safety-stock optimization
- reorder-point modeling
- stockout-risk analysis
