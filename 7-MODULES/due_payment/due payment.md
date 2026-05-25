## What Is the Due Payments Module?

Due Payments is the **central dashboard for all pending financial obligations** — amounts Leo Fashion owes to suppliers, and credits owed to customers. It gives the admin a real-time picture of outstanding liabilities so nothing slips through the cracks.

---

## What Appears in Due Payments?

|Entry Type|Source|Direction|
|---|---|---|
|Approved supplier bill|PO Bill → `approved`|We owe supplier|
|Partial payment balance|PO Bill (partially paid)|Remaining we owe|
|Customer credit note|DC Return → `credited`|We owe customer|

---

## Due Payments Dashboard Layout

```
┌─────────────────────────────────────────────────┐
│  DUE PAYMENTS                    [Filter] [Search]│
├───────────────────┬─────────────────────────────┤
│  Total Outstanding│        ₹ 1,24,500            │
│  Supplier Bills   │        ₹ 1,08,000            │
│  Customer Credits │        ₹  16,500             │
├───────────────────┴─────────────────────────────┤
│  Reference   │ Party    │ Amount  │ Due Since │ Action│
│  INV-441     │ Sri Fab  │ ₹21,240 │ 3 days    │ [Pay] │
│  INV-442     │ Sri Fab  │ ₹14,160 │ 1 day     │ [Pay] │
│  CR-001      │ Rajan Co │ ₹16,500 │ 5 days    │ [Settle]│
└─────────────────────────────────────────────────┘
```

---

## Payment Actions

### Pay a Supplier Bill

1. Admin clicks **Pay** next to a bill
2. Enters:
    - Amount paid (full or partial)
    - Payment method (cash / NEFT / cheque / UPI)
    - Payment date
    - Reference number (transaction ID / cheque no.)
3. Confirms → Bill status updates to `paid` (or stays `approved` if partial)
4. Audit log records the transaction

### Settle a Customer Credit

1. Admin clicks **Settle** next to a credit note
2. Options:
    - **Adjust against next order** — credit carried forward
    - **Refund** — mark as refunded with payment details
3. Credit entry is cleared from Due Payments

---

## Filters & Sorting

|Filter|Options|
|---|---|
|Type|Supplier bills / Customer credits / All|
|Supplier|Select specific supplier|
|Date range|Due since (oldest first by default)|
|Amount range|Min / Max|
|Status|All due / Partially paid|

Sorting: by amount (highest first), by age (oldest first), by party name.

---

## Aging Analysis

The Due Payments module shows how long each item has been outstanding:

|Age Bucket|Highlight|
|---|---|
|0–7 days|Normal (white)|
|8–15 days|Caution (yellow)|
|16–30 days|Warning (orange)|
|30+ days|Critical (red)|

Admin can filter to see only critical overdue items.

---

## Business Rules

- An item appears in Due Payments **only when a bill is `approved`** — not before
- Partial payments reduce the due amount but do not remove the entry until fully paid
- Customer credit notes appear immediately when return status → `credited`
- Payments cannot be backdated beyond 30 days (configurable)
- Every payment requires a payment method — cash entries are flagged for cash book reconciliation
- Once paid, the entry is archived (not deleted) — visible in payment history

---

## Payment History

Admin can view all completed payments:

- Date | Party | Reference | Amount | Method | Paid By (admin user)
- Exportable as CSV for accounting/Tally entry

---

## Related Documents

- PO Bills — Where supplier bills come from
- Supplier Bills — Bill approval process
- DC Returns — Where customer credits come from
- Profit & Loss — How payments affect P&L
- DB Schema — payments