# Purchase Order — Bills & GRN

**Module:** PO & Bill Management **Sub-doc:** `po-bills.md` **Route:** `/console/purchase-orders/:id` → Create Bill **System:** LEO Fashions ERP

---

## What Is a Bill (GRN)?

A **Bill** — also called a **Goods Receipt Note (GRN)** — is created when the goods ordered in a Purchase Order physically arrive at the delivery address. It records:

- How much was actually received
- On which date
- The supplier's invoice reference

Creating a bill does three things automatically:

1. Updates the **PO status** (Open → Partial or Closed)
2. Adds the received quantity to **Stock Management**
3. Creates a payable entry in **Due Payments**

---

## 👤 User Guide

### When Do You Create a Bill?

Create a bill as soon as goods from a supplier arrive at your location. Do not wait — stock and payment records depend on this being done promptly.

**Prerequisite:** The PO must be `✓ Approved` before you can create a bill against it.

---

### How to Create a Bill

1. Open the PO detail screen for the relevant PO (e.g. `PO-2026-0051`).
2. Click **Create Bill** (shown when PO is `Approved` and not yet `Closed`).
3. Fill in the bill form:

|Field|Required|Description|
|---|---|---|
|Receipt Date|Yes|Date the goods physically arrived|
|Received Quantity|Yes|Actual quantity received (may be less than ordered)|
|Unit|Yes|Pre-filled from PO (Kg / Pcs / Mtr)|
|Supplier Invoice No|No|Supplier's own invoice or challan number|
|Notes|No|Any delivery notes, quality remarks, or discrepancies|

4. The **Bill Amount** is calculated automatically:

```
Bill Amount = Received Quantity × Rate (from PO)
Bill GST    = Bill Amount × GST Rate
Bill Total  = Bill Amount + Bill GST
```

5. Click **Save**.

---

### What Happens After You Save a Bill

|Impact Area|What Changes|
|---|---|
|**PO Status**|If received qty = ordered qty → `Closed`. If less → `Partial`|
|**Stock Management**|Received quantity is added as an inward stock entry|
|**Due Payments**|Bill total is added as a new payable to the supplier|
|**Bill record**|Visible in the PO detail screen under the Bills section|

---

### Partial Receipts

If the supplier delivers only part of the order (e.g. 600 Kg out of 1,000 Kg ordered):

- Create a bill for **600 Kg**.
- PO status → `Partial`.
- When the remaining 400 Kg arrives later, create another bill for **400 Kg**.
- PO status → `Closed` once total billed qty equals ordered qty.

---

### Viewing Bills on a PO

Open any PO detail screen. Below the PO information, you will see a **Bills** section:

```
┌──────────────────────────────────────────────────────┐
│  Bills                                               │
├──────────────────────────────────────────────────────┤
│  Bill #1 — 19/05/2026                                │
│  Received: 600 Kg | Amount: ₹6,300                   │
│  Inv No: SURE/2026/441 | Created by: admin           │
├──────────────────────────────────────────────────────┤
│  Bill #2 — 25/05/2026                                │
│  Received: 400 Kg | Amount: ₹4,200                   │
│  Inv No: SURE/2026/489 | Created by: admin           │
└──────────────────────────────────────────────────────┘
  Total billed: 1,000 Kg | ₹10,500   PO Status: Closed
```

---

### Bill Amount Calculation

```
Each bill:
  Bill Taxable  = Received Quantity × PO Rate
  Bill GST      = Bill Taxable × GST Rate (5% for Yarn)
  Bill Total    = Bill Taxable + Bill GST

Across all bills on a PO:
  Total Billed Qty    = Sum of all bill received quantities
  Total Billed Amount = Sum of all bill totals
```

---

### Due Payments After a Bill

Once you create a bill, go to **Due Payments** in the sidebar. You will see a new entry for the supplier with the bill amount. Record the payment there once the supplier is paid.

---

## 🔐 Admin Guide

### Approving Bills

Bills do **not** require separate admin approval — they take effect immediately when saved by any user. However, admin has exclusive rights to edit or delete a bill if it was created incorrectly.

---

### Editing a Bill

If a bill was saved with the wrong quantity or date:

1. Open the PO detail.
2. Find the bill in the Bills section.
3. Click **Edit** on the bill (admin only).
4. Correct the quantity, date, or invoice number.
5. Save.

The PO status, stock, and due payments recalculate automatically.

---

### Deleting a Bill

If a bill was created by mistake:

1. Open the PO detail → Bills section.
2. Click **Delete** on the bill (admin only).
3. Confirm.

Deletion reverses:

- The stock inward entry
- The due payment entry
- The PO status (recalculated from remaining bills)

---

### Closing a PO Without Full Billing

If a supplier can no longer deliver the remaining balance:

1. Open the PO detail.
2. Click **Close PO** (admin only).
3. PO status → `Closed`.

This does not create any stock or payment entries for the unbilled quantity.

---

### Admin Permission Matrix for Bills

|Action|User|Admin|
|---|---|---|
|Create bill (on approved PO)|✅|✅|
|View bills on a PO|✅|✅|
|Edit a bill|❌|✅|
|Delete a bill|❌|✅|
|Download bill as PDF|✅|✅|

---

### Impact on Due Payments — Admin View

Each bill creates one entry in Due Payments:

```
Supplier: SUREYA TRADERS
PO: PO-2026-0051  |  Bill Date: 19/05/2026
Amount Due: ₹10,500  |  Status: Unpaid
```

Admin can record payments from the **Due Payments** screen. Partial payments are supported — the remaining balance stays visible until fully settled.


### API Endpoints — Bills

|Method|Endpoint|Description|Auth|
|---|---|---|---|
|`POST`|`/api/purchase-orders/:id/bills`|Create a bill|User + Admin|
|`GET`|`/api/purchase-orders/:id/bills`|List all bills on a PO|User + Admin|
|`GET`|`/api/purchase-orders/:id/bills/:billId`|Get single bill detail|User + Admin|
|`PATCH`|`/api/purchase-orders/:id/bills/:billId`|Edit a bill|Admin only|
|`DELETE`|`/api/purchase-orders/:id/bills/:billId`|Delete a bill|Admin only|

---

### POST `/api/purchase-orders/:id/bills` — Request Body

```json
{
  "receipt_date": "2026-05-19",
  "received_quantity": 600,
  "unit": "Kg",
  "supplier_invoice_no": "SURE/2026/441",
  "notes": "First partial delivery"
}
```

**Success — `201 Created`:**

```json
{
  "id": "uuid",
  "bill_number": "BILL-2026-0031",
  "receipt_date": "2026-05-19",
  "received_quantity": 600,
  "unit": "Kg",
  "taxable_amount": 6000.00,
  "gst_amount": 300.00,
  "grand_total": 6300.00,
  "purchase_order_status": "Partial"
}
```

**Errors:**

```json
{ "error": "PO is not approved" }                    // 409
{ "error": "PO is already closed" }                  // 409
{ "error": "Received quantity exceeds ordered qty" }  // 422
```

---

### Bill Number Generation

```sql
-- Same pattern as PO numbers, separate sequence
bill_number = 'BILL-' || YEAR || '-' || LPAD(NEXTVAL('bill_seq_' || YEAR)::TEXT, 4, '0')
-- Example: BILL-2026-0031
```