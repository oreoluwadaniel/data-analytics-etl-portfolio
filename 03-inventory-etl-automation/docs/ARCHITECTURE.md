# Inventory ETL Architecture

## Source

Warehouse inventory export.

## Ingestion

VBA refresh automation loads the latest source into the structured `Inventory_Raw` table.

## Validation

The `Data_Quality` sheet runs 15 integrity checks.

## Analytics layer

`Dashboard_Data` calculates:

- stock-status distribution
- category inventory value
- warehouse inventory value
- supplier inventory concentration
- replenishment value at risk

## Presentation

### Dashboard

Executive-level inventory exposure and risk.

### Operations

Interactive reorder browser with slicers for:

- warehouse
- category
- stock status
- supplier

### Inventory Summary

Lightweight refresh/KPI panel supporting the desktop workflow.

## Refresh audit

`Refresh_Log` records:

- date
- time
- records loaded
- status

`Snapshot_History` is designed to support period-over-period tracking as additional refreshes accumulate.
