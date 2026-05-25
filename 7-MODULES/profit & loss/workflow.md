## How P&L Is Built in Real Time

Every financial action in Leo Fashion automatically feeds into the P&L. This document explains the complete flow — what triggers revenue entries, what triggers expense entries, and how the final profit figure is calculated.

---

## P&L Construction Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                    PROFIT & LOSS WORKFLOW                         │
└──────────────────────────────────────────────────────────────────┘

REVENUE SIDE
─────────────

  [Order → Completed]          [Manual Revenue Entry]
         │                              │
         ▼                              ▼
  Revenue += Order Total        Revenue += entered amount
  (qty × rate per piece)        (e.g. misc income)

  [Customer Credit Note Issued]
         │
         ▼
  Revenue -= Credit Amount
  (offsets order revenue)


EXPENSE SIDE
─────────────

  [PO Bill → Paid]       [Wage Record → Paid]     [Overhead Entry]
        │                        │                       │
        ▼                        ▼                       ▼
  Expense +=             Expense +=              Expense +=
  Bill Total Amount      Net Wage Paid           Overhead Amount
  (incl. GST)            (gross − advance)       (rent, electricity…)


CALCULATION
────────────

  GROSS PROFIT = Total Revenue − Total Expenses
  MARGIN %     = (Gross Profit ÷ Revenue) × 100

  (Overhead-adjusted Net Profit = Gross Profit − Overheads,
   if overheads are tracked separately)
```

---

## Revenue Recognition — Step by Step

### Step 1: Order is Completed

```
Admin marks order → completed
          │
          ▼
System records:
  Revenue Entry
  ├── Type: order_revenue
  ├── Reference: Order ID (ORD-2026-012)
  ├── Amount: qty × rate per piece
  ├── Date: order completion date
  └── Period: month of completion
```

### Step 2: Credit Note Reduces Revenue

```
DC Return → credited status
          │
          ▼
System records:
  Revenue Entry (negative)
  ├── Type: credit_note
  ├── Reference: DC Return ID
  ├── Amount: − (returned qty × order rate)
  └── Period: month credit is issued
```

---

## Expense Recognition — Step by Step

### Supplier Payment

```
Admin pays PO bill (bill → paid)
          │
          ▼
System records:
  Expense Entry
  ├── Type: supplier_payment
  ├── Reference: Bill ID + Supplier Name
  ├── Amount: total amount paid (including GST)
  ├── Payment method: cash / NEFT / cheque / UPI
  └── Period: month of payment
```

### Worker Wages

```
Admin marks wage record → paid
          │
          ▼
System records:
  Expense Entry
  ├── Type: wages
  ├── Reference: Wage Record ID + Worker Name
  ├── Amount: net amount paid (gross − advance deducted)
  └── Period: week's end month
```

### Overhead Entry (Manual)

```
Admin clicks [Add Overhead]
          │
          ▼
Fills in:
  ├── Category (Rent / Electricity / Transport / Misc)
  ├── Amount
  ├── Date
  └── Description
          │
          ▼
Expense Entry recorded immediately
Visible in P&L for that month
```

---

## P&L Aggregation by Period

The system aggregates all entries by period:

```
Monthly P&L (May 2026)
─────────────────────────────────────────────────

REVENUE
  Order Revenue (8 orders)         ₹ 3,45,000
  Credit Notes (1 return)        − ₹     6,000
  ─────────────────────────────────────────────
  Net Revenue                      ₹ 3,39,000

EXPENSES
  Supplier Payments (6 bills)      ₹ 1,42,000
  Worker Wages (4 weeks)           ₹    68,500
  Overheads                        ₹     8,000
  ─────────────────────────────────────────────
  Total Expenses                   ₹ 2,18,500

─────────────────────────────────────────────────
GROSS PROFIT                       ₹ 1,20,500
PROFIT MARGIN                          35.5%
─────────────────────────────────────────────────
```

---

## Order-Level Drill Down

Admin can click into any order to see its individual P&L:

```
Order: ORD-2026-012 — 300 Shirts for Rajan & Co.
─────────────────────────────────────────────────
Revenue:
  300 pcs × ₹150                  ₹ 45,000

Expenses:
  Fabric (PO-2026-008)            ₹ 18,000
  Thread + accessories            ₹  2,400
  Cutting task (60 pcs × ₹5)     ₹    300
  Stitching tasks (300 × ₹12)    ₹  3,600
  Finishing tasks (300 × ₹8)     ₹  2,400
  ─────────────────────────────────────────
  Total Expenses                  ₹ 26,700

─────────────────────────────────────────────────
Order Profit                      ₹ 18,300
Order Margin                          40.7%
─────────────────────────────────────────────────
```

Note: Order-level expense linking (which PO / which tasks) requires reference tracking in PO and task records.

---

## Period Comparison View

Admin can compare two periods side by side:

```
                    Apr 2026      May 2026     Change
Revenue             ₹2,80,000    ₹3,39,000    +21.1%
Expenses            ₹1,95,000    ₹2,18,500    +12.1%
Profit              ₹  85,000    ₹1,20,500    +41.8%
Margin                 30.4%        35.5%     +5.1pp
```

---

## Export & Reporting

|Export Type|Format|Use Case|
|---|---|---|
|Monthly P&L Summary|PDF|Owner/investor review|
|Detailed Expense List|CSV|Accountant / Tally entry|
|Order-level P&L|PDF|Profitability analysis|
|Year-to-Date Summary|PDF|Annual planning|

---

## Key Rules

|Rule|Detail|
|---|---|
|Revenue on completion|Orders recognized as revenue only when `completed`|
|Expense on payment|Expenses recorded only when bills/wages are `paid` (cash basis)|
|Period locking|Closed months can be locked — no entries allowed after lock|
|Read-only derived data|P&L figures cannot be manually edited — only overheads are manual|
|Advance wages excluded|Advance payments are not an expense — only deducted wages are|
|GST included in expenses|Bill payments include GST in expense total (no separation in current version)|

---

## Related Documents

- Profit & Loss Overview — Dashboard, fields, and filters
- Due Payments — Payments that create expense entries
- Weekly Wages — Wage expense source
- Orders Overview — Revenue source
- Future Enhancements — Accrual accounting, GST separation