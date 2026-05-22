# Purchase Order — Overview

**Module:** PO & Bill Management **Sub-doc:** `po-overview.md` **Route:** `/console/purchase-orders` **System:** LEO Fashions ERP

---

## What Is the PO Module?

The Purchase Order module manages the complete procurement process at LEO Fashions — from raising an order with a supplier, through admin approval, to receiving goods and closing the order. Every PO is linked to a production order and generates a printable PDF document sent to the supplier.

---

## Module Structure

```
📁 po-bill-management/
│
├── po-overview.md     ← You are here — what the module is, who uses it, key concepts
├── po-bills.md        ← Bills / GRN — receiving goods, creating bills, payments
└── po-flow.md         ← End-to-end lifecycle flow from creation to closure
```

---

## 👤 User Guide

### Who Uses This Module?

|Role|What They Do Here|
|---|---|
|**Staff / User**|Create POs, view PO list, print PDFs, create bills when goods arrive|
|**Admin**|Approve POs, delete incorrect POs, close POs, configure GST rates|

---

### Key Concepts You Need to Know

#### Purchase Order (PO)

A PO is a formal document you send to a supplier saying: _"Please supply us with these materials at this price."_ Once created, it needs admin approval before goods can be billed against it.

#### PO Number

Every PO gets a unique number automatically in the format `PO-YYYY-NNNN`.

|Part|Meaning|Example|
|---|---|---|
|`PO`|Fixed prefix|`PO`|
|`YYYY`|Year of creation|`2026`|
|`NNNN`|Auto-incremented number|`0051`|

Full example: **`PO-2026-0051`**

#### Linked Production Order

Every PO must be linked to a production order (`LEO-YYYY-NNN`). This tells the system _why_ the PO was raised and links procurement costs back to a specific job.

#### Supplier

The business you are buying from. Suppliers are maintained in the **Supplier Management** module and selected from a dropdown when creating a PO.

#### Delivery Address

Where the goods should be delivered — this can be different from the LEO Fashions factory address (e.g. directly to a job-work unit or customer).

---

### The PO List Screen

```
┌──────────────────────────────────────────────────────────┐
│  ←   Purchase Orders                       [📋] [🏠]    │
├──────────────────────────────────────────────────────────┤
│  [🔍 search...]               [By PO Number ▼]          │
│  [Supplier ▼]  [Status ▼]  [Material Category ▼] [Print]│
├──────────────────────────────────────────────────────────┤
│  PO-2026-0051   Open   ✓ Approved              [🔗] [🖨] │
│  SUREYA TRADERS | Yarn                                   │
│  Qty: 1,000 | Amount: ₹10,500                            │
│  LEO-2026-002                                            │
│  Modified: 7 hours ago                                   │
├──────────────────────────────────────────────────────────┤
│  PO-2026-0043   Partial   ✓ Approved           [🔗] [🖨] │
│  SUREYA TRADERS | Yarn                                   │
│  Qty: 1,000 | Amount: ₹10,500                            │
│  LEO-2026-029                                            │
│  Modified: 9 hours ago                                   │
└──────────────────────────────────────────────────────────┘
                                    [+ Purchase Order]  FAB
```

#### What Each Part of a PO Card Means

|Element|Description|
|---|---|
|`PO-2026-0051`|Unique PO number|
|`Open` (amber)|No goods received yet|
|`Partial` (blue)|Some goods received, rest still pending|
|`Closed` (gray)|Fully received and billed|
|`✓ Approved` (green)|Admin has approved this PO|
|`Pending` (yellow)|Waiting for admin approval|
|Supplier \| Category|Who you ordered from and what category|
|Qty / Amount|Total quantity ordered and total ₹ (including GST)|
|Teal chip (`LEO-2026-002`)|Linked production order|
|`Modified: X ago`|Last time this PO was updated|
|🔗|Copy shareable link|
|🖨|Download PO as PDF|

---

### Status Reference

#### Fulfilment Status

|Status|Color|Meaning|
|---|---|---|
|Open|Amber|PO raised, goods not yet received|
|Partial|Blue|Some goods received, bill raised for partial qty|
|Closed|Gray|All goods received and fully billed, or manually closed|

#### Approval Status

|Status|Color|Meaning|
|---|---|---|
|Pending|Yellow|Created, awaiting admin approval|
|✓ Approved|Green|Approved by admin — PO is active|

---

### Creating a Purchase Order

1. Click **+ Purchase Order** (bottom-right FAB).
2. Select **Supplier** from the dropdown.
3. Select the **Production Order** this PO is for.
4. **Material Category** auto-fills — change if needed.
5. Select or create a **Delivery Address**.
6. Add line items in the items table:

|Field|Required|Notes|
|---|---|---|
|Description|Yes|Material name|
|HSN Code|No|For GST classification|
|Quantity|Yes|Must be > 0|
|Unit|Yes|Kg / Pcs / Mtr|
|Rate (₹)|Yes|Per unit price|
|Amount|Auto|Quantity × Rate|

7. Review the totals:

```
Taxable Value  =  Sum of all item amounts
GST (5%)       =  Taxable Value × 5%   (for Yarn)
Grand Total    =  Taxable Value + GST
```

8. Click **Save**.

The PO is created with status `Open` and approval `Pending`. Admin will receive it in their approval queue.

---

### Searching and Filtering

|Control|Purpose|
|---|---|
|🔍 Search bar|Search by PO number or supplier name|
|Supplier filter|Narrow to a specific supplier|
|Status filter|Open / Partial / Closed|
|Material Category|Filter by Yarn / Fabric / etc.|
|Sort dropdown|By PO Number / By Date / By Amount|

---

### Printing a PO

**From the list:** Click the 🖨 icon on the PO card. **From the detail screen:** Open a PO → click **Print / Download PDF**.

The PDF includes company letterhead, supplier details, delivery address, item table, GST breakdown, grand total in words, and digital approval signature.

---

## 🔐 Admin Guide

### Your Daily Checklist

1. Open **Approval Status** in the sidebar — check the badge count.
2. Review and approve pending POs.
3. Check for any **Partial** POs where delivery is overdue.
4. Review **Due Payments** for outstanding supplier amounts.

---

### Approving a PO

1. Open any PO showing `Pending` approval badge.
2. Verify: supplier, production order, item descriptions, quantities, rates, delivery address.
3. Click **Approve**.
4. Status changes to `✓ Approved`. The PO is now locked for editing.

> Once approved, a PO cannot be edited. If there is an error, you must close it and have the user raise a fresh one.

---

### Deleting a PO

Only available when:

- `approval_status = Pending` (not yet approved)
- No bills are linked to the PO

Steps:

1. Open the PO detail.
2. Click **Delete** (red — admin only).
3. Confirm the prompt.

---

### Force-Closing a PO

Use when a supplier can no longer fulfil an order:

1. Open the PO detail.
2. Click **Close PO** (admin only).
3. The status moves to `Closed` regardless of how much was received.

---

### Admin Permission Matrix

|Action|User|Admin|
|---|---|---|
|View PO list|✅|✅|
|View PO detail|✅|✅|
|Create PO|✅|✅|
|Edit PO (Pending only)|✅|✅|
|Print / Download PDF|✅|✅|
|Share PO link|✅|✅|
|Approve PO|❌|✅|
|Delete PO|❌|✅|
|Force-close PO|❌|✅|

---

### GST Configuration

Admin can update GST rates per material category: **⚙️ Settings → Tax Configuration**

|Category|Default Rate|
|---|---|
|Yarn|5%|
|Fabric|5%|
|Others|18%|

---

### Company Details on PDFs

Admin sets the company name, address, GST number, mobile, and logo used on all PO PDFs: **⚙️ Settings → Company Profile**

---

## 🛠 Developer Guide

### Tech Stack

|Layer|Technology|
|---|---|
|Frontend|React SPA — `/console/purchase-orders`|
|Backend|Node.js REST API|
|Database|PostgreSQL|
|PDF Engine|Puppeteer (headless Chromium)|
|Auth|`session` cookie — `HttpOnly`, `SameSite=Lax`, 7-day TTL|

### Core Database Tables

|Table|Purpose|
|---|---|
|`purchase_orders`|One row per PO — status, amounts, FKs|
|`purchase_order_items`|Line items — description, qty, rate, amount|
|`suppliers`|Supplier master|
|`delivery_addresses`|Reusable delivery address book|
|`production_orders`|Linked orders (managed by Orders module)|

### Core API Endpoints

|Method|Endpoint|Description|
|---|---|---|
|`GET`|`/api/purchase-orders`|List all POs (paginated, filterable)|
|`POST`|`/api/purchase-orders`|Create a new PO|
|`GET`|`/api/purchase-orders/:id`|Get full PO detail|
|`PATCH`|`/api/purchase-orders/:id`|Edit PO (Pending only)|
|`DELETE`|`/api/purchase-orders/:id`|Delete PO (admin, Pending only)|
|`POST`|`/api/purchase-orders/:id/approve`|Approve PO (admin only)|
|`POST`|`/api/purchase-orders/:id/close`|Close PO (admin only)|
|`GET`|`/api/purchase-orders/:id/pdf`|Download PO as PDF|

### PO Number Generation

```sql
-- Per-year sequence, resets Jan 1 via cron
po_number = 'PO-' || YEAR || '-' || LPAD(NEXTVAL('po_seq_' || YEAR)::TEXT, 4, '0')
-- Example: PO-2026-0051
```

### Amount Calculation

```javascript
item.amount    = item.quantity * item.rate;
taxableValue   = items.reduce((s, i) => s + i.amount, 0);
gstRate        = TAX_RATES[material_category] ?? 0.18;
gstAmount      = taxableValue * gstRate;
grandTotal     = taxableValue + gstAmount;
```

