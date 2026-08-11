# Inventory ETL Automation & Replenishment Intelligence

> **A VBA-driven Excel ETL system that loads warehouse inventory exports, runs 15 automated data-quality checks, and turns the results into a prioritized replenishment and risk view for operations and procurement.**

**Platform:** Microsoft Excel, Power Query, VBA
**Data:** Synthetic warehouse inventory export
**Records:** 3,400
**Status:** Portfolio Case Study

---

## 1. Business problem

Inventory reports fall apart in a specific, quiet way: the export loads fine, the numbers look plausible, and nobody notices that 51 SKUs are sitting on negative stock or that 278 items are overstocked until someone tries to act on the numbers and the decision doesn't hold up.

A useful inventory system needs to do two things at once. First, prove the data can be trusted before anyone reports on it. Second, tell operations what to act on first, not just what the totals are.

This project builds both layers on top of a single warehouse export, using VBA to automate the refresh and Excel's data model to carry the analysis.

---

## 2. What the workbook does

```text
Warehouse Export (CSV)
        ↓
VBA Refresh -> Inventory_Raw (structured table)
        ↓
Data_Quality: 15 automated integrity checks
        ↓
Dashboard_Data: valuation, risk, and concentration calculations
        ↓
   Dashboard | Operations | Inventory Summary | Refresh_Log
   (executive  (SKU-level    (lightweight KPI    (audit
    risk)       drill-down)   panel)              trail)
```

Every refresh logs its own date, time, record count, and status, so the workbook doubles as its own audit trail instead of relying on someone remembering when it last ran.

---

## 3. Data-quality findings

The source data keeps its defects on purpose, so the quality layer has something real to catch. Nothing gets silently zeroed out or overwritten with a guess. Every exception stays visible until it's resolved at the source or covered by an approved business rule.

| Check | Records affected |
|---|---:|
| Negative stock quantity | 51 |
| Reserved quantity exceeds on-hand | 51 |
| Available-quantity mismatch | 51 |
| Missing reorder level | 102 |
| Missing barcode | 102 |
| Missing supplier name | 85 |
| Expired but still marked active | 84 |
| Overstock beyond maximum level | 278 |
| Discontinued item still flagged for reorder | 38 |

The workbook's data-quality score is a check-weighted indicator: `1 − average(affected-record % across the 15 checks)`. It isn't a formal probability that the dataset is correct. Different checks carry different operational severity, and the score is meant to communicate that at a glance, not replace the detail behind it.

---

## 4. From data quality to decisions

The checklist isn't the point on its own. What matters is converting inventory records into a procurement-oriented view:

```text
Reorder shortfall × Unit cost = Estimated replenishment cost
```

Applied across the current dataset, the estimated cost to bring available inventory back up to reorder levels comes out to approximately **₦6.49B**. That figure is a replenishment-cost exposure, not a lost-revenue forecast. It tells procurement how much capital is tied up in closing the gap, and nothing more than that.

The workbook answers the questions an inventory manager actually asks day to day:

- What needs attention first?
- Where is stock risk concentrated, by warehouse, category, or supplier?
- Which warehouse is carrying the most inventory value?
- Which suppliers represent the largest exposure if something goes wrong?
- How much procurement spend would it take to restore reorder levels?
- Which problems are data issues versus real operational issues?

---

## 5. Presentation layer

**Dashboard.** Executive view of inventory exposure and risk, built for a five-minute read.

**Operations.** An interactive reorder browser with slicers for warehouse, category, stock status, and supplier, for anyone who needs to drill into specific SKUs.

**Inventory Summary.** A lightweight refresh and KPI panel that supports the day-to-day desktop workflow without opening the full dashboard.

---

## 6. Data dictionary (selected fields)

| Field | Business meaning |
|---|---|
| Product ID / SKU / Barcode | Product identification |
| Warehouse / Warehouse Code / Bin / Aisle / Shelf | Physical storage location |
| Quantity On Hand / Reserved / Available | Core stock position |
| Reorder Level / Safety Stock / Maximum Stock Level | Replenishment thresholds |
| Supplier ID / Name / Country / Lead Time | Procurement source and timing |
| Unit Cost / Selling Price / Inventory Value | Financial exposure |
| Stock Status / Reorder Required | Operational flags |
| Expiry Date / Last Restock Date | Shelf-life and movement tracking |

Full field list in [`docs/DATA_DICTIONARY.md`](docs/DATA_DICTIONARY.md).

---

## 7. How to use the workbook

1. Open `Inventory_ETL_Automation.xlsm` and enable macros when prompted.
2. Run the refresh button. VBA loads the source into `Inventory_Raw` and logs the run in `Refresh_Log`.
3. Check `Data_Quality` for affected-record counts and the overall check-weighted score.
4. Use `Dashboard` for management-level risk, or `Operations` to drill into individual SKUs.
5. Confirm the run in `Refresh_Log`: timestamp, records loaded, status.

Full steps in [`docs/RUNBOOK.md`](docs/RUNBOOK.md).

---

## 8. Limitations

There's no sales or consumption history in this dataset, so the workbook stops short of demand forecasting or inventory-turn optimization. Claiming otherwise without that data would be overreaching. Adding historical consumption would open up days-of-supply tracking, demand velocity, safety-stock optimization, reorder-point modeling, and stockout-risk analysis, but that's future work, not something this version pretends to do.

This is also a synthetic dataset built for portfolio purposes. The ₦6.49B exposure figure and the 15 quality findings describe this dataset's model output, not a real company's operations.

---

## 9. Repository structure

```text
03-inventory-etl-automation/
├── README.md
├── Inventory_ETL_Automation.xlsm
├── data/
│   └── warehouse_inventory.csv
└── docs/
    ├── ARCHITECTURE.md
    ├── CASE_STUDY.md
    ├── DATA_DICTIONARY.md
    ├── DATA_QUALITY_FINDINGS.md
    └── RUNBOOK.md
```

---

## What this project demonstrates

Turning a raw warehouse export into an operational decision tool: raw export, VBA-automated ingestion, a 15-point quality audit, valuation and risk modeling, an executive dashboard, operational drill-down, and a refresh audit trail.

The spreadsheet itself isn't the point. It's a repeatable mechanism that tells an inventory team what's wrong, what it's worth, and what to fix first.
