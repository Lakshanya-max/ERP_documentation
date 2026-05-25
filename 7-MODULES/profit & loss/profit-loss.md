## What Is the Profit & Loss Module?

The Profit & Loss (P&L) module gives the admin a real-time financial snapshot of Leo Fashion's performance — how much revenue has come in, how much has gone out in expenses, and what's left as profit (or loss).

This is not an accountant-grade balance sheet — it is an **operational P&L** built for a garment manufacturer to understand their business at a glance.

---

## How P&L Is Calculated

```
REVENUE
  └── All completed order amounts collected
        (or: orders in completed status with payment received)

EXPENSES
  ├── Supplier Payments (paid PO bills)
  ├── Worker Wages (paid wage records)
  └── Other Overheads (manual entries — rent, electricity, etc.)

─────────────────────────────
GROSS PROFIT = Revenue − Expenses
NET PROFIT   = Gross Profit − Overheads (if tracked)
```

---

## P&L Dashboard

```
┌─────────────────────────────────────────────────────┐
│  PROFIT & LOSS          [May 2026 ▾]  [This Month ▾]│
├──────────────────────────────────────────────────────┤
│                                                      │
│   💰 REVENUE                          ₹ 3,45,000    │
│   📤 EXPENSES                         ₹ 2,18,500    │
│   ─────────────────────────────────────────────      │
│   📈 NET PROFIT                       ₹ 1,26,500    │
│                                    (Margin: 36.7%)   │
│                                                      │
├──────────────────────────────────────────────────────┤
│  REVENUE BREAKDOWN                                   │
│  ├── Order Receipts         ₹ 3,45,000              │
│  └── (Credits / Returns)  − ₹       0               │
│                                                      │
│  EXPENSE BREAKDOWN                                   │
│  ├── Supplier Payments      ₹ 1,42,000              │
│  ├── Worker Wages           ₹  68,500               │
│  └── Overheads              ₹   8,000               │
└──────────────────────────────────────────────────────┘
```

---

## Revenue Sources

|Source|How It Enters P&L|
|---|---|
|Completed orders|Order `total_amount` added when order → `completed`|
|Customer credits|Deducted when credit note is issued (DC return)|
|Adjustments|Manual revenue entry by admin|

---

## Expense Sources

|Expense Type|How It Enters P&L|
|---|---|
|Supplier bill paid|Bill → `paid` → amount added to expenses|
|Worker wages paid|Wage record → `paid` → amount added to expenses|
|Overhead entry|Admin manually enters (rent, electricity, transport)|
|Advance wages|Not counted as expense until deducted from wages|

---

## Overhead Management

Admin can log recurring overheads manually:

|Field|Description|
|---|---|
|**Category**|Rent / Electricity / Transport / Misc|
|**Amount**|Expense amount|
|**Month/Period**|Which period this belongs to|
|**Notes**|Description|

These are simple entries — not linked to POs or wages.

---

## Date Filtering

Admin can view P&L for:

- **This month** — default view
- **Last month**
- **Custom date range** — pick start and end date
- **This financial year** (April–March for Indian businesses)

---

## Order-Level P&L

Admin can drill down into a single order's P&L:

```
Order: ORD-2026-012
  Revenue:          ₹ 45,000   (300 pcs × ₹150)
  Material Cost:  − ₹ 18,000   (PO bills for this order)
  Labour Cost:    − ₹  9,600   (tasks for this order)
  ─────────────────────────────
  Order Profit:     ₹ 17,400   (Margin: 38.7%)
```

This helps admin identify which orders are profitable and which are not.

---

## P&L Report Export

Admin can export:

- Monthly P&L summary as PDF or CSV
- Order-level P&L breakdown
- Expense detail (supplier + wages + overheads)

Useful for: accountant handoff, bank reporting, owner review.

---

## Business Rules

- Revenue is recognized when order status → `completed` (not on dispatch)
- Expenses are recognized when bill/wage is `paid` (cash basis)
- Customer credits reduce revenue in the period the credit is issued
- P&L data is read-only — it is always derived from actual records
- Manual overhead entries can be edited or deleted within the same month

---

## Limitations (Current Version)

- No accrual accounting — only cash basis
- No balance sheet or assets tracking
- Stock valuation not included in P&L (unless manually added as overhead)
- No multi-currency support
- Tax (GST) is recorded but not separated as a P&L line item

See Future Enhancements for planned improvements.

---

## Related Documents

- Due Payments — Payments that affect P&L
- Weekly Wages — Wage expense source
- Stock Overview — Inventory context
- Orders Overview — Revenue source