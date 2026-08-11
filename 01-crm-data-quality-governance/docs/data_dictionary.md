# Data Dictionary

## Source fields (raw CRM export)

| Field | Type | Description |
|---|---|---|
| CustomerID | Text | Unique identifier for the customer record |
| FirstName | Text | Customer's first name |
| LastName | Text | Customer's last name |
| FullName | Text | Concatenated first and last name |
| Company | Text | Customer's employer / account name |
| Email | Text | Primary email address |
| Phone | Text | Primary phone number |
| Mobile | Text | Secondary/mobile phone number |
| JobTitle | Text | Customer's job title |
| Department | Text | Customer's department |
| Industry | Text | Company's industry |
| LeadSource | Text | Channel the lead originated from |
| CustomerStatus | Text | Lifecycle stage: Lead, Qualified, Opportunity, Prospect, Customer, Churned, Inactive |
| Country | Text | Customer's country |
| State | Text | Customer's state/region |
| City | Text | Customer's city |
| Address | Text | Street address |
| PostalCode | Text | Postal/ZIP code |
| DateCreated | Date | Date the record was created in the CRM |
| LastContactDate | Date | Date of the most recent contact with this customer |
| AssignedSalesRep | Text | Sales rep who owns the account |

## Fields added by the quality engine

| Field | Type | Description |
|---|---|---|
| Email Status | Text | `Valid` / `Invalid`, based on format validation rules |
| Phone Status | Text | `Valid` / `Invalid`, based on digit-count validation |
| Customer Completeness | Text | `Complete` / `Incomplete`, based on the 8 required fields |
| Data Quality Score | Number (0-100) | Composite score after email, phone, completeness, and duplicate penalties |
| Missing Required Fields | Number | Count of required fields that are blank or a placeholder value |
| Phone Digit Count | Number | Count of numeric digits in the phone field |
| Issue Reason | Text | Plain-English summary of every issue triggered on this record |
| Duplicate Email Count | Number | How many records in the file share this email |
| Duplicate Phone Count | Number | How many records in the file share this phone number |
| Potential Duplicate | Text | `Yes` / `No`, true if either duplicate count is greater than 1 |
| Days Since Last Contact | Number | Days elapsed since LastContactDate |
| Stale Record | Text | `Yes` / `No`, true if Days Since Last Contact exceeds the configured threshold |

## Required fields for completeness

A record is only marked `Complete` if all 8 of these fields are populated with a real value (placeholder values like "Unknown" or "N/A" don't count):

FirstName, LastName, Email, Phone, Company, JobTitle, Country, City
