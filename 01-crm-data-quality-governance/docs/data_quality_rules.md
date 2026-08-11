# Data Quality Rules

All thresholds and weights below live in the `Config` sheet of the workbook. Nothing here is hardcoded into the scoring formulas, so any of these numbers can be changed without touching the engine's logic.

## Email validation

A record's email is marked **Invalid** if any of the following are true:
- The field is blank
- It doesn't contain exactly one `@`
- It starts with `@`
- It ends with a `.`
- It contains a space
- There's no valid extension after the domain (no `.` following the `@`)

Valid emails are standardized to lowercase and trimmed of leading/trailing whitespace on load.

## Phone validation

A record's phone is marked **Invalid** if any of the following are true:
- The field is blank
- It contains a `#` character
- It contains fewer than 7 digits (configurable minimum)
- It contains alphabetic characters (e.g. "080-CALL-NOW")

## Completeness

A record is **Complete** only if all 8 required fields are populated with a real value:

FirstName, LastName, Email, Phone, Company, JobTitle, Country, City

The following values are treated as blank, not as valid data, even though they're technically non-empty text: `Unknown`, `Not Available`, `Not Assigned`, `N/A`, `TBD`.

## Duplicate detection

A record is flagged **Potential Duplicate** if either of these is true:
- Its email (when valid) matches another record's email
- Its phone number (when valid) matches another record's phone number

This is exact matching, not fuzzy matching. Detection only; the engine does not auto-merge or delete duplicate records. Flagged records are routed to the Exceptions queue for a human to review and decide how to consolidate.

## Staleness

A record is flagged **Stale** if there's been no contact in 365+ days (configurable). This is tracked separately from the Data Quality Score, since staleness is a measure of commercial relevance, not data correctness. A record can be perfectly valid and complete while still being stale.

## Scoring

Every record starts at 100 points. Points are deducted for each issue detected:

| Issue | Penalty (points) |
|---|---|
| Invalid email | 30 |
| Invalid phone | 20 |
| Incomplete profile | 40 |
| Potential duplicate | 25 |

The score floor is 0 (a record can't score below zero even if every rule fires).

## Exception threshold

Records scoring below **80** are routed to the Exceptions queue for manual review, rather than remaining mixed into the clean dataset.
