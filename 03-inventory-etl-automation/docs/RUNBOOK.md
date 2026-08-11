# Inventory ETL Runbook

## 1. Prepare source data

Place the latest warehouse export in the configured raw-data location.

## 2. Open the public workbook

Use:

`Inventory_ETL_Automation_PUBLIC.xlsm`

Enable macros when prompted.

## 3. Run the refresh

Use the workbook's refresh button.

The VBA process loads the source into `Inventory_Raw` and records the run in `Refresh_Log`.

## 4. Review data quality

Open:

`Data_Quality`

Check:

- affected record counts
- status
- overall check-weighted score

## 5. Review decisions

Use:

`Dashboard`

for management-level risk.

Use:

`Operations`

for SKU-level operational investigation.

## 6. Review audit trail

Use:

`Refresh_Log`

to verify:

- refresh timestamp
- records loaded
- status

## 7. Snapshot history

`Snapshot_History` is designed to accumulate one row per refresh.

Do not fabricate historical values just to create a trend chart.
