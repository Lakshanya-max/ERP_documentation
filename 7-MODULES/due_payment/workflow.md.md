## End-to-End Flow

This document walks through the complete lifecycle of a due payment — from the moment a bill is approved to the final settlement and its impact on financial records.

---

## Workflow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    DUE PAYMENTS WORKFLOW                     │
└─────────────────────────────────────────────────────────────┘

  TRIGGER SOURCES
  ───────────────
  [Supplier Bill Approved]          [Customer Credit Note Issued]
           │                                     │
           ▼                                     ▼
  ┌─────────────────────────────────────────────────┐
  │              DUE PAYMENTS DASHBOARD              │
  │   All approved-but-unpaid obligations land here  │
  └─────────────────────────────────────────────────┘
           │
           ▼
  Admin Reviews Outstanding Items
  (sorted by age — oldest first)
           │
     ┌─────┴──────┐
     ▼            ▼
  Supplier      Customer
  Bill Due      Credit Due
     │            │
     ▼            ▼
  Admin        Admin
  Clicks Pay   Clicks Settle
     │            │
     ▼            ▼
  Enter Payment  Choose Resolution:
  Details:       ├── Adjust against next order
  • Amount       └── Refund (mark as refunded)
  • Method
  • Date
  • Ref No.
     │
     ▼
  ┌─────────────────────────┐
  │    Full Payment?         │
  └─────────────────────────┘
     │              │
    YES             NO
     │              │
     ▼              ▼
  Bill → PAID    Partial payment recorded
  Removed from   Remaining balance stays
  Due Payments   in Due Payments (aging
                 counter resets)
     │
     ▼
  Audit Log Updated
  P&L Expense Recorded
  Supplier Payment History Updated
```

---

## Step-by-Step Process

### Phase 1 — Entry into Due Payments

|Step|Action|Who|
|---|---|---|
|1|Supplier bill approved by admin|Admin|
|2|Bill automatically appears in Due Payments|System|
|3|Entry shows: party, amount, due since date|System|

OR

|Step|Action|Who|
|---|---|---|
|1|DC return inspected, credit note issued|Admin|
|2|Customer credit automatically appears|System|

---

### Phase 2 — Admin Reviews Dashboard

- Admin opens **Due Payments** from sidebar
- Sees all outstanding amounts sorted by age
- Color-coded aging: green (0–7 days) → yellow → orange → red (30+ days)
- Admin prioritises which to pay first (typically oldest or largest)

---

### Phase 3 — Making a Payment (Supplier)

```
Admin clicks [Pay] on a bill entry
        │
        ▼
Payment drawer/modal opens
        │
        ▼
Admin fills:
  • Payment amount (pre-filled with full amount, editable for partial)
  • Payment method: Cash / NEFT / IMPS / Cheque / UPI
  • Payment date (defaults to today)
  • Reference number (NEFT transaction ID / cheque no. / UPI ref)
  • Notes (optional)
        │
        ▼
Admin clicks [Confirm Payment]
        │
        ▼
System checks: Is amount = full bill amount?
        │
   YES  │  NO
        │
   Bill → paid     Partial payment logged
   Removed from    Balance = Bill total − Paid
   dashboard       Entry stays in dashboard
```

---

### Phase 4 — Settling a Customer Credit

```
Admin clicks [Settle] on a credit entry
        │
        ▼
Choose resolution type:
  ┌─────────────────────────────────────┐
  │ Option A: Adjust against next order │
  │   → Credit carried as balance       │
  │   → Applied when next order billed  │
  └─────────────────────────────────────┘
  ┌─────────────────────────────────────┐
  │ Option B: Cash Refund               │
  │   → Enter refund date + method      │
  │   → Mark as refunded                │
  └─────────────────────────────────────┘
        │
        ▼
Credit entry cleared from Due Payments
Audit log updated
```

---

### Phase 5 — After Payment

|What Updates|How|
|---|---|
|Bill status|`approved` → `paid`|
|Supplier ledger|Payment recorded in supplier history|
|P&L|Expense recorded in the payment's month|
|Audit log|Action, amount, method, user, timestamp|
|Due Payments|Entry removed (or reduced if partial)|

---

## Aging Rules

|Days Outstanding|Display|Action|
|---|---|---|
|0–7 days|White / Normal|—|
|8–15 days|Yellow badge|—|
|16–30 days|Orange badge|Admin notified|
|30+ days|Red badge|Flagged as overdue|

---

## Payment Methods Supported

|Method|Reference Field|
|---|---|
|Cash|No reference needed|
|NEFT / IMPS|Bank transaction reference|
|Cheque|Cheque number + bank name|
|UPI|UPI transaction ID|

---

## Key Rules

- Payment cannot be made before a bill is `approved`
- Payment date cannot be future-dated
- Once a bill is `paid`, the payment record is locked — no edits
- Partial payments can be made multiple times until bill is fully settled
- Every payment requires a payment method — open cash entries are flagged