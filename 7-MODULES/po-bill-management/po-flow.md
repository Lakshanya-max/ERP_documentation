# Purchase Order — End-to-End Flow

**Module:** PO & Bill Management **Sub-doc:** `po-flow.md` **System:** LEO Fashions ERP

---

## Overview

This document describes the complete lifecycle of a Purchase Order at LEO Fashions — from the moment a user raises it, through admin approval, goods receipt, payment, and final closure.

---

## 👤 User Guide — Your Journey Through a PO

### The Full Journey (Your Steps)

```
Step 1: You receive a production order from management
        e.g. "We need 1,000 Kg of yarn for LEO-2026-002"
                    │
                    ▼
Step 2: You create a PO in the ERP
        Supplier: SUREYA TRADERS
        Qty: 1,000 Kg @ ₹10/Kg
        Linked to: LEO-2026-002
                    │
                    ▼
Step 3: PO is saved — Status: Open | Approval: Pending
        Admin is notified in their Approval queue
                    │
                    ▼
Step 4: Admin reviews and approves the PO
        Status becomes: Open | ✓ Approved
                    │
                    ▼
Step 5: You (or someone at the delivery address)
        contacts SUREYA TRADERS with the PO PDF
                    │
                    ▼
Step 6: Goods arrive — you create a Bill in the ERP
        Received: 1,000 Kg on 25/05/2026
                    │
                    ▼
Step 7: PO status → Closed
        Stock → +1,000 Kg added automatically
        Due Payments → ₹10,500 added for SUREYA TRADERS
                    │
                    ▼
Step 8: Finance team records payment in Due Payments
        Entry marked → Paid ✓
```

---

### What You Need to Do at Each Step

|Step|Your Action|Where in the ERP|
|---|---|---|
|1|Receive instruction|(outside ERP)|
|2|Create PO|PO & Bill Management → + Purchase Order|
|3|Wait for approval|Nothing to do — admin handles this|
|5|Print and share PO|Click 🖨 on PO card|
|6|Create Bill when goods arrive|Open PO → Create Bill|
|8|Record payment (finance)|Due Payments module|

---

### Status You Will See at Each Stage

```
Just created:       Open  |  Pending
After approval:     Open  |  ✓ Approved
Partial delivery:   Partial  |  ✓ Approved
Full delivery:      Closed   |  ✓ Approved
Force closed:       Closed   |  ✓ Approved  (or Pending)
```

---

### What to Do If Something Goes Wrong

|Situation|What To Do|
|---|---|
|Made a mistake in the PO before approval|Edit the PO directly (pencil icon)|
|Made a mistake after admin approved|Tell admin — they will close it, then you raise a new PO|
|Goods arrived but PO still shows Pending|Wait for admin to approve, then create the bill|
|Wrong quantity billed|Tell admin — they will edit the bill|
|Supplier sent wrong goods|Do not create a bill — report to admin first|

---

## 🔐 Admin Guide — Your Actions in the Flow

### Where Admin Steps In

```
                              ┌────────────────────┐
User creates PO               │   ADMIN REQUIRED   │
       │                      └────────────────────┘
       ▼
  Pending approval ─────────► Admin reviews PO
                                      │
                         ┌────────────┴────────────┐
                         │                         │
                    Looks correct?           Error found?
                         │                         │
                         ▼                         ▼
                    Click APPROVE            Click DELETE
                         │                   User creates
                         ▼                   a corrected PO
                PO is now ✓ Approved
```

---

### Admin Approval Checklist

Before clicking **Approve**, verify:

- [ ] Correct supplier selected (name + GSTIN)
- [ ] Correct production order linked (e.g. `LEO-2026-002`)
- [ ] Material description is accurate
- [ ] Quantity and unit are correct
- [ ] Rate (₹ per unit) matches agreed pricing
- [ ] Delivery address is correct
- [ ] Grand Total looks right (Qty × Rate + 5% GST)

---

### What Admin Controls at Each Stage

|Stage|Admin Action|Effect|
|---|---|---|
|PO raised (Pending)|**Approve**|PO locked, becomes active for billing|
|PO raised (Pending)|**Delete**|PO permanently removed|
|PO approved (any status)|**Close PO**|Force-closes, no more billing|
|Bill created incorrectly|**Edit Bill**|Corrects qty/date, recalculates stock + payments|
|Bill created by mistake|**Delete Bill**|Reverses stock and payment entries|

---

### Handling a Rejected PO (No Reject Button — Use Delete)

The system does not have a "Reject" button. When a PO has an error:

1. Click **Delete** on the pending PO (admin only).
2. Inform the user of what was wrong.
3. User creates a new, corrected PO.
4. Admin approves the corrected one.

---

### Monitoring PO Health

Check these regularly:

|Signal|Where to Look|Action|
|---|---|---|
|High Pending badge count|Sidebar → Approval Status|Approve pending POs|
|Many Partial POs|PO list → filter Status: Partial|Follow up on deliveries|
|Old unpaid Due Payments|Due Payments module|Chase supplier payment|

---

## 🛠 Developer Guide — Technical Flow

### Complete State Machine

```
                    POST /api/purchase-orders
                              │
                              ▼
                 ┌────────────────────────┐
                 │  purchase_orders       │
                 │  status = 'Open'       │
                 │  approval = 'Pending'  │
                 └────────────────────────┘
                        │           │
                        │           └──── DELETE (admin, no bills)
                        │                → Row deleted
                        │
              POST .../approve (admin)
                        │
                        ▼
                 ┌────────────────────────┐
                 │  status = 'Open'       │
                 │  approval = 'Approved' │
                 └────────────────────────┘
                        │           │
                        │           └──── POST .../close (admin)
                        │                → status = 'Closed'
                        │
              POST .../bills (any user)
              received_qty < total_qty
                        │
                        ▼
                 ┌────────────────────────┐
                 │  status = 'Partial'    │
                 │  approval = 'Approved' │
                 └────────────────────────┘
                        │           │
                        │           └──── POST .../close (admin)
                        │                → status = 'Closed'
                        │
              POST .../bills (any user)
              total_billed_qty >= total_qty
                        │
                        ▼
                 ┌────────────────────────┐
                 │  status = 'Closed'     │  (terminal state)
                 │  approval = 'Approved' │
                 └────────────────────────┘
```

---

### Side Effects Map

Every event in the PO lifecycle triggers side effects across modules:

```
Event                    │ Side Effects
─────────────────────────┼──────────────────────────────────────────────
PO Created               │ approval_status = 'Pending'
                         │ Audit: PO_CREATED
                         │ Approval badge count +1
─────────────────────────┼──────────────────────────────────────────────
PO Approved              │ approval_status = 'Approved'
                         │ Audit: PO_APPROVED
                         │ Approval badge count -1
─────────────────────────┼──────────────────────────────────────────────
PO Deleted               │ Row removed from purchase_orders
                         │ purchase_order_items cascade deleted
                         │ Audit: PO_DELETED
                         │ Approval badge count -1 (if was Pending)
─────────────────────────┼──────────────────────────────────────────────
Bill Created             │ PO status → Partial or Closed
                         │ stock_movements INSERT (inward)
                         │ due_payments INSERT (Unpaid)
                         │ Audit: BILL_CREATED
─────────────────────────┼──────────────────────────────────────────────
Bill Edited              │ PO status recalculated
                         │ stock_movements updated
                         │ due_payments amount updated
                         │ Audit: BILL_EDITED
─────────────────────────┼──────────────────────────────────────────────
Bill Deleted             │ PO status recalculated
                         │ stock_movements reversed
                         │ due_payments entry removed
                         │ Audit: BILL_DELETED
─────────────────────────┼──────────────────────────────────────────────
PO Force-Closed          │ status = 'Closed'
                         │ No stock or payment changes
                         │ Audit: PO_CLOSED
─────────────────────────┼──────────────────────────────────────────────
Payment Recorded         │ due_payments status → Partial or Paid
  (in Due Payments)      │ Audit: PAYMENT_RECORDED
```

---

### API Call Sequence — Full Lifecycle

```bash
# 1. Create PO
POST /api/purchase-orders
→ 201: { id, po_number, status: "Open", approval_status: "Pending" }

# 2. Admin approves
POST /api/purchase-orders/:id/approve
→ 200: { approval_status: "Approved" }

# 3. Create partial bill
POST /api/purchase-orders/:id/bills
{ receipt_date, received_quantity: 600, unit: "Kg" }
→ 201: { bill_number, grand_total, purchase_order_status: "Partial" }

# 4. Create final bill
POST /api/purchase-orders/:id/bills
{ receipt_date, received_quantity: 400, unit: "Kg" }
→ 201: { bill_number, grand_total, purchase_order_status: "Closed" }

# 5. Record payment (Due Payments module)
POST /api/due-payments/:id/record
{ amount_paid: 10500, payment_date, payment_mode: "Bank Transfer" }
→ 200: { status: "Paid" }
```

---

### Database State at Each Stage

|Stage|`status`|`approval_status`|`bills` count|`due_payments`|
|---|---|---|---|---|
|Just created|`Open`|`Pending`|0|None|
|Approved|`Open`|`Approved`|0|None|
|First partial bill|`Partial`|`Approved`|1|1 (Unpaid)|
|Final bill|`Closed`|`Approved`|2|2 (Unpaid)|
|Payment done|`Closed`|`Approved`|2|2 (Paid)|

---

### Error Scenarios and Handling

| Scenario                    | HTTP Status | Error Message                                          |
| --------------------------- | ----------- | ------------------------------------------------------ |
| Approve already approved PO | `409`       | `Purchase order is already approved`                   |
| Delete approved PO          | `409`       | `Cannot delete an approved purchase order`             |
| Delete PO with bills        | `409`       | `Cannot delete a PO with existing bills`               |
| Bill on unapproved PO       | `409`       | `PO is not approved`                                   |
| Bill on closed PO           | `409`       | `PO is already closed`                                 |
| Bill qty > remaining qty    | `422`       | `Received quantity exceeds remaining ordered quantity` |
| Edit PO after approval      | `409`       | `Cannot edit an approved or closed purchase order`     |
| Non-admin tries to approve  | `403`       | `Forbidden`                                            |
| Unauthenticated request     | `401`       | `Unauthorized`                                         |
