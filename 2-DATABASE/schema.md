# Database Overview — LEO Fashions

## How Data Flows Through the System

---

## Data Journey — Start to End

```
USER fills a form (Web / Mobile)
        ↓
Data sent to API server
        ↓
Server VALIDATES the data
        ↓
Server CALCULATES auto values
(Order ID, tolerance, totals, GST)
        ↓
Data STORED in database
        ↓
Status set (Draft / Open / Pending)
        ↓
Admin NOTIFIED for approval
        ↓
Admin APPROVES
        ↓
Status UPDATED
        ↓
Next process TRIGGERED
        ↓
Data RETRIEVED when user opens screen
        ↓
Displayed back to user
```

---

## Where Data Starts

|Source|Example|
|---|---|
|User fills form|Order details, quantities, fabric info|
|Admin creates record|PO, DC, supplier|
|System auto-generates|Order ID, PO ID, DC ID, timestamps|
|System calculates|Cutting qty, totals, remaining qty, % complete|

---

## How Data Is Retrieved

When any list or detail screen opens:

```
User opens screen (e.g. Orders List)
        ↓
App sends GET request to API
        ↓
API checks user role:
├── Admin  → fetch ALL records
└── User   → fetch OWN records only
        ↓
API applies filters (status, date, search)
        ↓
API applies pagination
        ↓
Data returned and displayed
```

---

## Key Database Relationships

```
USERS
  └── places ──────────► ORDERS
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
           STAGES            PO              DC
         (8 rows)       (materials)    (processing)
              │               │               │
              ▼               ▼               ▼
        STAGE_JOBS        PO_INWARDS      DC_INWARDS
        (work done)     (received qty)  (returned qty)
              │               │               │
              └───────────────┴───────────────┘
                              │
                              ▼
                           BILLS
                        (invoices)
                              │
                              ▼
                          PAYMENTS
                       (money paid)
```

---

## Auto-Calculated Values

|Field|Formula|
|---|---|
|Cutting Quantity|Order Qty × 1.03 (3% tolerance)|
|DC Remaining|Total Sent − Received Back|
|PO Remaining|Total Ordered − Total Received|
|Processing Loss|Sent Qty − Received Qty|
|PO Total Amount|Qty × Rate + GST|
|Stage Completion %|(Completed ÷ Total) × 100|
|Weekly Wage Total|Pieces × Rate per piece|
|Net Salary|Total Wages − Advance Given|

---

## Data Rules

|Rule|Detail|
|---|---|
|Every record has unique ID|Auto-generated on creation|
|Every record tracks creator|`created_by` always stored|
|Every record tracks changes|`updated_by` + `updated_on` always stored|
|Status moves forward only|Open → Partial → Closed (no reversal)|
|Admin approval required|Nothing proceeds without approval|
|Role-based data access|Users see only their own data|
|Soft relationships|All records linked by IDs (Order ID, Supplier ID etc.)|

---

## ID Formats

| Record           | Format          | Example         |
| ---------------- | --------------- | --------------- |
| Order            | LEO-YYYY-XXX    | LEO-2026-008    |
| Purchase Order   | PO-YYYY-XXXX    | PO-2026-0051    |
| Delivery Challan | DC-YYYY-XXXX(R) | DC-2026-0028(R) |
| Supplier         | SUP-XXXXXX      | SUP-000019      |
| Supplier Bill    | SUPBILL-XXXX    | SUPBILL-0001    |
| Task             | Auto # + Order  | #LEO-2026-019   |