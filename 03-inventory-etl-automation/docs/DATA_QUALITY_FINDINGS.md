# Data Quality Findings

## Current audit

The source contains 3,400 inventory records.

| Check | Affected |
|---|---:|
| Negative stock quantity | 51 |
| Reserved exceeds on-hand | 51 |
| Available quantity mismatch | 51 |
| Missing reorder level | 102 |
| Missing safety stock | 0 |
| Missing barcode | 102 |
| Unresolved supplier name | 0 |
| Unresolved bin location | 0 |
| Duplicate Product IDs | 0 |
| Expired but still active | 84 |
| Overstock beyond maximum | 278 |
| Discontinued but flagged for reorder | 38 |
| Missing warehouse assignment | 0 |
| Missing supplier name | 85 |
| Missing product category | 0 |

## Interpretation

The defects are intentionally retained in the synthetic source data so the quality-control layer can demonstrate what it detects.

The pipeline should not silently convert:

```text
negative stock → 0
```

or:

```text
missing field → fabricated value
```

Instead, the exception should remain visible and be resolved at source or through an approved business rule.

## Data quality score

The workbook's current score is a **check-weighted quality indicator**:

```text
1 − average(affected-record percentage across the 15 checks)
```

It should not be interpreted as a formal probability that the dataset is correct.

This wording is important because different checks have different operational severity.
