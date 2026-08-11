# Sales Data Quality Findings

| Rule | Failed rows |
|---|---:|
| Duplicate Order ID | 22 |
| Null Order Date | 0 |
| Future Order Date | 735 |
| Zero/negative Quantity | 670 |
| Zero/negative Unit Price | 0 |
| Discount >50% | 760 |
| Missing Salesperson | 506 |
| Missing Customer Name | 538 |
| Missing Product Name | 473 |
| Invalid Region | 380 |
| Invalid Payment Method | 383 |
| Leading/trailing spaces | 2,235 |
| Invalid Currency | 1,233 |

Failures are not additive because one row can fail multiple rules.

The current cleaning workflow reduces 75,000 source rows to 74,598 reporting rows. Remaining defects should be classified as reject, quarantine, approved correction or documented exception rather than silently overwritten.

The source also contains 735 transactions after the stated March 2026 reporting period.
