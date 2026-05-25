# Approval Status — Overall Workflow

## What Is the Approval Module?

The Approval module is Leo Fashion's **central review queue** where all items that require admin sign-off are collected in one place. Rather than hunting across modules, the admin can open the Approval Queue and action everything from one screen.

---

## What Goes Through Approval?

|Item|Submitted By|Approved By|Effect of Approval|
|---|---|---|---|
|Supplier bill|Admin (on behalf of supplier)|Admin|Bill → `approved`, enters Due Payments|
|PO (before sending)|Admin|Admin (senior)|PO → `sent` to supplier|
|Wage sheet (weekly)|System (auto-generated)|Admin|Wages → `approved`, ready for payout|
|Advance wage request|Worker|Admin|Advance → `approved`, cash given to worker|
|DC (before dispatch)|Admin|Admin (senior)|DC → `dispatched`|
|Stock write-off|Admin|Admin|Seconds → written off, P&L updated|

---

## Approval Queue — Overall Flow

```
┌───────────────────────────────────────────────────────────┐
│                    APPROVAL WORKFLOW                        │
└───────────────────────────────────────────────────────────┘

  Various modules submit items for approval
           │
           ▼
  ┌─────────────────────────┐
  │    APPROVAL QUEUE        │  ← Admin's daily action center
  │   (Pending items list)   │
  └─────────────────────────┘
           │
           ▼
  Admin opens each item
           │
     ┌─────┴──────────┐
     ▼                ▼
  APPROVE           REJECT
     │                │
     ▼                ▼
  Item status      Item status
  → approved       → rejected
     │                │
     ▼                ▼
  Effect applied   Rejection reason
  (see table       logged + party
   above)          notified
     │
     ▼
  Audit log records:
  • Who approved
  • When
  • Notes (if any)
```

---

## Approval Queue Screen

```
┌──────────────────────────────────────────────────────────┐
│  APPROVAL QUEUE                  Pending: 7  [Filter ▾]  │
├──────────────────────────────────────────────────────────┤
│  Type      │ Reference   │ Party      │ Amount  │ Age    │
│  🧾 Bill   │ INV-441     │ Sri Fab.   │ ₹21,240 │ 2 days │
│  🧾 Bill   │ INV-442     │ Sri Fab.   │ ₹14,160 │ 1 day  │
│  💰 Wages  │ Week 12–18  │ All Workers│ ₹9,170  │ Today  │
│  💵 Advance│ ADV-022     │ Murugan K. │ ₹   500 │ Today  │
│  📦 Write- │ WO-003      │ (Seconds)  │ 12 mtrs │ 3 days │
│    off     │             │            │         │        │
└──────────────────────────────────────────────────────────┘
  [Approve All Wages]  [Filter: Bills only]
```

---

## Approval Flow Per Item Type

### Supplier Bill Approval

```
Bill submitted (INV-441)
        │
        ▼
Appears in Approval Queue → type: Bill
        │
        ▼
Admin clicks → Bill detail opens
  Shows: PO reference, supplier, amount, GST, bill date
        │
        ▼
Admin reviews:
  ✓ Amount matches PO?
  ✓ Bill date reasonable?
  ✓ Materials actually received?
        │
   ┌────┴────┐
APPROVE    REJECT
   │          │
   ▼          ▼
Bill →      Bill → rejected
approved    Admin adds reason
Enters      Supplier notified
Due Payments (to resubmit)
```

---

### Weekly Wage Approval

```
System auto-generates wage draft (every Monday)
        │
        ▼
Draft appears in Approval Queue → type: Wages
        │
        ▼
Admin clicks → Wage sheet opens
  Shows: each worker, tasks, gross, advance, net
        │
        ▼
Admin reviews:
  ✓ Task quantities correct?
  ✓ Advances properly deducted?
  ✓ No missing workers?
        │
   ┌────┴────┐
APPROVE    ADJUST
   │          │
   ▼          ▼
Wages →    Admin edits
approved   specific amounts
Workers    (with reason)
can see    Re-reviews
their pay  Then approves
```

---

### Advance Wage Request Approval

```
Worker submits advance request
  OR Admin creates advance on behalf of worker
        │
        ▼
Appears in Approval Queue → type: Advance
  Shows: worker name, amount requested, reason
        │
        ▼
Admin decides:
  ✓ Worker has earned enough to justify advance?
  ✓ Previous advances cleared?
        │
   ┌────┴────┐
APPROVE    REJECT
   │          │
   ▼          ▼
Advance →   Advance →
approved    rejected
Cash given  Worker notified
to worker   of reason
Recorded
in wages
```

---

### Stock Write-Off Approval

```
Admin proposes write-off (seconds stock)
        │
        ▼
Appears in Approval Queue → type: Write-off
  Shows: item, quantity, reason, estimated loss value
        │
        ▼
Admin (senior) reviews:
  ✓ Quantity verified?
  ✓ Cannot be reworked?
        │
   ┌────┴────┐
APPROVE    REJECT
   │          │
   ▼          ▼
Seconds     Item stays in
qty removed seconds stock
P&L loss    (try rework?)
recorded
```

---

## Bulk Actions

Admin can bulk-action items of the same type:

|Bulk Action|Available For|
|---|---|
|Approve All|Wage sheets (if all reviewed)|
|Reject All|Not available (must review each)|
|Filter by Type|Bills / Wages / Advances / Write-offs|

---

## Rejection Handling

When an item is rejected:

1. Admin must enter a **rejection reason** (mandatory)
2. The item's status changes to `rejected`
3. The submitter is notified (in-app or note visible on record)
4. The item leaves the approval queue
5. Corrected item can be resubmitted as a new entry

---

## Approval History

Admin can view all past approvals (not just pending):

- Filter by type, date range, approved by, rejected/approved
- Each item shows: who approved, when, any notes
- Supports audit queries ("Who approved bill INV-441?")

---

## Business Rules

- Only users with `admin` role can approve items
- Approval reason is optional for approvals, mandatory for rejections
- Approved items cannot be un-approved (must be voided via the source module)
- Items older than 7 days in the queue are highlighted for urgency
- Wage approvals must be done before payout — system blocks pay action if not approved

---

## Related Documents

- Supplier Bills — Bills awaiting approval
- Weekly Wages — Wage sheets in approval
- Wage Advances — Advance requests
- Stock Overall Workflow — Write-off flow
- Admin Role — Who can approve
- Audits — Approval audit trail