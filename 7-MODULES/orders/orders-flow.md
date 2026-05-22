# Orders Module — Flow

## End-to-End Order Flow

This document describes the complete journey of an order — from creation through production, procurement, dispatch, and completion — showing how the Orders module connects to every other part of the ERP.

---

## Full Order Lifecycle

```
                    ┌─────────────────────┐
                    │   Buyer places order │
                    │   (e.g., Zudio)      │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  Admin creates Order │
                    │  LEO-YYYY-NNN        │
                    │  Status: Draft       │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │  Fill order details  │
                    │  · Quantities        │
                    │  · Fabric & Trims    │
                    │  · CMT price         │
                    │  · Dates             │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │  Submit for Approval │
                    │  approval_status:    │
                    │  Draft → Pending     │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │  Approver reviews    │
                    │  (Approval Status    │
                    │   queue)             │
                    └──────┬──────┬───────┘
                           │      │
                      Approved  Rejected
                           │      │
                           │      └──► Creator edits & resubmits
                           ▼
                    ┌─────────────────────┐
                    │  Order: In Progress  │
                    │  approval: Approved  │
                    └──────────┬──────────┘
                               │
            ┌──────────────────┼──────────────────┐
            ▼                  ▼                  ▼
   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
   │  PO & Bill  │    │     DC      │    │    Tasks    │
   │  Management │    │  Management │    │   / Stages  │
   │             │    │             │    │             │
   │  Procure    │    │  Dispatch / │    │  Track each │
   │  yarn &     │    │  Return     │    │  production │
   │  fabric     │    │  fabric     │    │  milestone  │
   └──────┬──────┘    └──────┬──────┘    └──────┬──────┘
          │                  │                  │
          ▼                  ▼                  ▼
   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
   │ Due Payments│    │    Stock    │    │  All stages │
   │             │    │  Management │    │    Done     │
   │ Track bills │    │             │    │      │      │
   │ & supplier  │    │  Fabric     │    │      ▼      │
   │ payments    │    │  in/out     │    │  Order:     │
   └──────┬──────┘    └─────────────┘    │  Completed  │
          │                              └─────────────┘
          ▼
   ┌─────────────┐
   │ Profit &    │
   │    Loss     │
   │             │
   │  Revenue vs │
   │  actual cost│
   └─────────────┘
```

---

## Step-by-Step Flow

### Step 1 — Create the Order

- Admin clicks `+ Order` in the Orders module.
- Fills in: buyer, classification (Bulk/Sample), unit, style, CMT price, delivery date.
- System auto-generates order number (`LEO-YYYY-NNN`).
- Order is saved in **Draft** status.

---

### Step 2 — Fill Order Details

- Add size-wise quantities (Bulk and/or Sample).
- System calculates cutting quantities with tolerance (default 3%).
- Add fabric colours with yarn and fabric process costs.
- Add production trims and packing trims.
- Fill Other Prices (embroidery, logistics, testing, etc.).
- Enable Style Type & Print Panel if garment has print panels.

---

### Step 3 — Approval

- Admin submits order for approval.
- Order appears in **Approval Status** sidebar queue.
- Approver reviews and approves or rejects.
- On approval → `approval_status` becomes `Approved`.

---

### Step 4 — Procurement (PO & Bill Management)

- Procurement team raises a **Purchase Order** (`PO-YYYY-NNNN`) linked to this order.
- Supplier (e.g., SUREYA TRADERS) receives the PO document (printed PDF).
- Supplier delivers material in full or partial shipments.
- PO status: `Open` → `Partial` → `Closed` as deliveries arrive.
- Bills from supplier are recorded against the PO.

---

### Step 5 — Fabric Dispatch (DC Management)

- Fabric received from supplier is dispatched to a processing unit via a **Delivery Challan** (`DC-YYYY-NNNN`).
- DC is linked to the order (e.g., `LEO-2026-031`).
- If fabric is returned to supplier, a **Return Delivery Note** (`DC-YYYY-NNNN(R)`) is raised.
- DC carries: fabric details, lot number, lab card, weight, knitting specs, remarks.
- DC PDF is printed and travels with the fabric physically.
- DC status: `Partial` → `Closed` as fabric movements complete.

---

### Step 6 — Production Tracking (Stages & Tasks)

- Production moves through defined stages (Cutting → Stitching → Washing → Packing → Dispatch).
- Each stage is marked In Progress → Done as work is completed.
- Stage progress ring on the Order card fills up visually.
- Tasks module tracks granular action items within each stage.

---

### Step 7 — Completion & Analysis

- When all stages are marked Done → Order status moves to **Completed**.
- **Profit & Loss** module pulls cost data from the order and compares with actual PO bills.
- Revenue = CMT price × total quantity shipped.
- Net profit/loss is calculated per order.

---

## How Orders Connects to Each Module

|Module|Connection|Data Shared|
|---|---|---|
|PO & Bill Management|PO is raised against an order|`order_id`, buyer, quantities, fabric spec|
|DC Management|DC is created from an order (via Create DC button)|`order_id`, style, fabric details, recipient|
|Tasks|Tasks reference the order for stage tracking|`order_id`, stage progress|
|Stock Management|Stock consumed against the order|`order_id`, fabric type, weight|
|Due Payments|Bills from POs linked to the order|`order_id`, supplier, bill amount, due date|
|Profit & Loss|Costs and revenue rolled up by order|CMT price, all cost fields, quantities|
|Approval Status|Order submitted for approval|`order_id`, `approval_status`|
|Audits|All changes to the order are logged|`order_id`, user, action, timestamp|

---

## PDF Documents Generated from an Order

|Document|Trigger|Pages|Contents|
|---|---|---|---|
|Order Summary PDF|Print button on Order Detail|3|Full order snapshot — quantities, fabric, trims, pricing, audit fields|
|Purchase Order PDF|Print on a linked PO|1–2|Supplier address, line items, HSN, amounts, GST totals|
|Delivery Challan PDF|Print on a linked DC|1|Fabric details, lot/lab card, weight, process info, signatures|
|Return Delivery Note|Print on a DC(R)|1|Same as DC with return designation|

---

## Order Number to Document Chain

```
LEO-2026-036  (Order)
    │
    ├── PO-2026-0051  →  SUREYA TRADERS  (Yarn procurement)
    │
    ├── DC-2026-0028(R)  →  Harish  (Fabric return)
    │
    ├── DC-2026-0023  →  SHIVALAYA KNITS  (Fabric dispatch)
    │
    └── [Bills, Payments, P&L all trace back to LEO-2026-036]
```

Every PO and DC carries the originating Order number as a visible reference tag — creating a full paper trail from buyer order to supplier payment.