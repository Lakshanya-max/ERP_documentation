# UI Screens — LEO Fashions

## Every Screen Reference

|#|Screen|Access|Purpose|
|---|---|---|---|
|1|Login|All|Authenticate|
|2|Dashboard|All|Overview|
|3|Orders List|All|View/filter orders|
|4|Order Detail|All|Full order info|
|5|Create Order|User/Admin|Place new order|
|6|Stage Detail|Staff/Admin|Update stage progress|
|7|Tasks List|All|View tasks|
|8|Task Detail|All|View task info|
|9|Create Task|Admin|Assign new task|
|10|Suppliers List|Admin|View suppliers|
|11|Supplier Detail|Admin|Full supplier info|
|12|Create Supplier|Admin|Add supplier|
|13|PO List|Admin|View purchase orders|
|14|PO Detail|Admin|Full PO info|
|15|Create PO|Admin|New purchase order|
|16|DC List|Admin|View delivery challans|
|17|DC Detail|Admin|Full DC info|
|18|Create DC|Admin|New DC|
|19|Return DC Form|Admin|Create return DC|
|20|Weekly Wages List|Admin|View wages by order|
|21|Wage Detail|Admin|Panel-wise breakdown|
|22|Approval Status|Admin|Approve pending items|
|23|Stock Management|Admin|View stock|
|24|Due Payments|Admin|View overdue bills|
|25|Profit & Loss|Admin|Financial report|
|26|Users|Admin|Manage user accounts|
|27|Audits|Admin|Activity log|
|28|FAQ|All|Help content|

---

## Screen Details

### Screen 3 — Orders List

- Filters: Search, Status, Classification, Unit
- Each card: Order ID, status badge, style, unit, time, progress ring
- Actions: Click card, Export, + Order

### Screen 4 — Order Detail

- Header: Order ID, status, print
- Tabs: Summary, Quantities, Fabric, Yarn, Trims, Other Prices, Stages
- Each stage expandable with qty table + completion %

### Screen 7 — Tasks List

- Tabs: My Tasks, Given Tasks, All
- Sub-filters: Completed, Pending
- Each card: Task name, assigned by → to, order link, date

### Screen 11 — Supplier Detail

- Tabs: Basic Details, Bills
- Basic: Name, contact, address, GST, PAN, types, bank info, verification
- Bills: List of all invoices with totals

### Screen 14 — PO Detail

- Summary: Total Qty, Received, Remaining, Amount
- Tabs: Basic Details, Inwards, Bills, Remaining Stocks
- Approval section: Approved by, Approved on

### Screen 17 — DC Detail

- Header: DC number, status badges (Partial, Approved, Inward: Partial, Bill: Open)
- Summary: Sent, Received Back, Remaining, Total Amount
- Tabs: Basic Details, DC Inwards, DC Bills, Remaining Stocks

### Screen 21 — Wage Detail

- Header: Order ID, name, style, week dates
- Panel-wise table: Department × Day (7 days) × Amount
- Grand Total across all panels
- Advance section if any