# Sales Reporting Data Dictionary

**Fact:** `fact_sales` — transaction-level sales events.

**Dimensions:** `dim_customers`, `dim_products`, `dim_salespersons`, `dim_branches`, `dim_regions`, `dim_calendar`.

Key fact fields: Order_ID, Order_Date, Region, Branch_ID, Salesperson_ID, Customer_ID, Product_ID, Customer_Type, Quantity, Unit_Price, Discount_%, Net_Unit_Price, Sales_Amount, Currency, Payment_Method, Order_Status and Invoice_Number.

The public package anonymizes customer, salesperson and branch-manager contact information while preserving keys and analytical relationships.
