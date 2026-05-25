# Business Logic Overview — LEO Fashions

## Core Business Rules

### Rule 1 — Admin Approval Gates Everything

Nothing moves forward without admin approval. Every order, PO, and DC starts in a pending state and waits for admin action.

### Rule 2 — 3% Tolerance on All Orders

```
Order Quantity × 1.03 = Cutting Quantity
Example: 100 pcs ordered → 103 pcs cut
Reason: Covers cutting wastage and defects
```

### Rule 3 — Quantity Always Tracked in Three Numbers

```
Total Sent / Ordered
    − Received / Returned
    = Remaining
This applies to PO, DC, and all stages.
```

### Rule 4 — Processing Loss Is Normal

```
Sent to supplier = 20 Kg
Received back    = 19 Kg
Loss             = 1 Kg (acceptable)
Cause: Dyeing, knitting, washing shrinkage
```

### Rule 5 — Role-Based Data Visibility

```
Admin  → sees ALL records across all orders/users
User   → sees ONLY their own orders and data
```

### Rule 6 — Status Only Moves Forward

```
Open → Partial → Closed  (cannot reverse)
Draft → In Progress → Completed
```

### Rule 7 — Completion % Auto-Calculated

```
Stage Completion = (Completed Qty ÷ Total Qty) × 100
Order Completion = All 8 stages at 100%
```

### Rule 8 — Advance Deducted from Final Salary

```
Final Salary = Total Weekly Wages − Advance Given
```

---

## Key Calculations

|Calculation|Formula|
|---|---|
|Cutting Quantity|Order Qty × 1.03|
|PO Total|Qty × Rate × (1 + GST%)|
|DC Remaining|Total Sent − Total Received Back|
|Stage %|(Completed ÷ Total) × 100|
|Weekly Wage|Pieces × Rate per Piece|
|Net Salary|Total Wages − Advance|
|Processing Loss|Sent − Received|

---

## Approval Logic

```
Any new Order / PO / DC created
        ↓
Saved with approval_status = Pending
        ↓
Approval Status badge count increases
        ↓
Admin reviews and approves
        ↓
approval_status = Approved
        ↓
Record becomes active and usable
```

---

## Task Auto-Generation Logic

```
Order approved and stage starts
        ↓
System AUTO creates tasks
(prefix: [Auto])
        ↓
Tasks assigned to relevant staff
        ↓
Staff completes task
        ↓
Task status = Completed
```

Manual tasks can also be created by Admin directly.