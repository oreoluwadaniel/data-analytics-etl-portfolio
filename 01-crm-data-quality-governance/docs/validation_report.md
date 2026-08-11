# Validation Report

## Run summary

| Field | Value |
|---|---|
| Run ID | RUN-0001 |
| Refresh date | Aug 6, 2026 |
| Run by | Data Analytics Team |
| Source system | CRM Export (CSV) |
| Data owner | RevOps / Data Analytics Team |
| Records processed | 5,130 |
| Records passed QC (score ≥ 80) | 3,575 |
| Records flagged to Exceptions | 1,555 |
| Run status | Completed, exceptions found |

## Key metrics

| Metric | Count | Rate |
|---|---|---|
| Complete profiles | 4,659 | 90.8% |
| Incomplete profiles | 471 | 9.2% |
| Valid emails | 4,920 | 95.9% |
| Invalid emails | 210 | 4.1% |
| Valid phones | 5,023 | 97.9% |
| Invalid phones | 107 | 2.1% |
| Potential duplicate records | 946 | 18.4% |
| Stale records (no contact 12+ months) | 1,600 | 31.2% |
| Exceptions with no owner assigned | 40 | 2.6% of total |
| Average Data Quality Score | n/a | 90.1 / 100 |

## Data quality by customer status

| Status | Customers | Avg Quality Score | % Complete | % Valid Email |
|---|---|---|---|---|
| Lead | 1,010 | 90.7 | 91.4% | 96.6% |
| Qualified | 804 | 90.3 | 90.7% | 95.0% |
| Opportunity | 327 | 89.6 | 90.5% | 95.4% |
| Prospect | 916 | 89.3 | 90.4% | 95.9% |
| Customer | 1,184 | 90.6 | 91.5% | 95.6% |
| Churned | 419 | 89.3 | 89.5% | 96.2% |
| Inactive | 470 | 89.5 | 90.4% | 96.8% |
| **Total** | **5,130** | **90.1** | **90.8%** | **95.9%** |

## Exceptions by customer status (revenue relevance)

| Status | Segment | Customers | Exceptions | % of segment |
|---|---|---|---|---|
| Customer | Active / Revenue | 1,184 | 339 | 28.6% |
| Opportunity | Active / Revenue | 327 | 102 | 31.2% |
| Qualified | Pre-Revenue | 804 | 240 | 29.9% |
| Prospect | Pre-Revenue | 916 | 292 | 31.9% |
| Lead | Pre-Revenue | 1,010 | 291 | 28.8% |
| Churned | Lost | 419 | 134 | 32.0% |
| Inactive | Lost | 470 | 157 | 33.4% |
| **Total** | | **5,130** | **1,555** | **30.3%** |

Worth flagging: exception rates are fairly evenly spread across the pipeline, including active revenue-generating accounts (Customer and Opportunity), not just cold or dead leads. That means data quality issues here aren't a "clean up old leads" problem, they're a live pipeline-reporting risk.

## Issue reasons triggered

| Issue reason | Records |
|---|---|
| Potential Duplicate (only) | 859 |
| Incomplete Profile (only) | 410 |
| Invalid Email (only) | 199 |
| Invalid Phone (only) | 92 |
| Incomplete Profile + Potential Duplicate | 61 |
| Invalid Phone + Potential Duplicate | 15 |
| Invalid Email + Potential Duplicate | 11 |

## Notes from this run

Full audit and rebuild: replaced hardcoded Email/Phone Status, Completeness, and Quality Score values with live formulas; fixed mislabeled invalid emails; added the Config sheet and Exceptions tracking.
