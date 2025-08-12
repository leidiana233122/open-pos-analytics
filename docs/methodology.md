# Methodology

Scope: open POs, delivery performance, vendor aging.

Key definitions
- On Time: DeliveredDate on or before DueDate.
- Open PO value: RemainingQty × UnitPrice on rows where Status = Open.
- Age buckets: based on DueDate to today.

Assumptions
- If DeliveredDate is blank and Status = Open, row is excluded from on-time calc.
- Currency and time zone use the source system defaults.
