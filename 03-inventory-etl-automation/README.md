# Inventory ETL Automation & Replenishment Intelligence

**An Excel inventory system that turns a raw warehouse export into a validated, prioritized replenishment and stock-risk view for operations and procurement.**

**Stack:** Excel, Power Query, VBA  
**Dataset:** 3,400 SKUs  
**Quality controls:** 15 automated checks  
**Replenishment exposure:** ₦6.49B

---

## The business problem

Inventory data can look clean while hiding expensive problems.

Negative stock, missing reorder levels, expired items, supplier gaps, and excess inventory can all sit inside a warehouse export without stopping the report from running.

The business therefore needs two answers before acting:

1. **Can we trust the inventory data?**
2. **What needs attention first?**

This project handles both.

---

## How it works

```text
Warehouse CSV
     ↓
Power Query + VBA
     ↓
Data Validation
     ↓
Inventory Model
     ↓
Risk & Replenishment Analysis
     ↓
Dashboard + SKU-Level Operations View
