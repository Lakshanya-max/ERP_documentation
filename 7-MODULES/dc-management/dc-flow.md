# DC Management — Flow

## Overview

This document describes the complete data flow and lifecycle of a Delivery Challan — from creation through dispatch, approval, stock update, billing, and closure — and how the DC module connects to every other part of the LEO Fashions ERP.

---

## System Architecture Flow

```
┌──────────────────────────────┐
│    Dispatch / Warehouse      │
│         Users                │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        Frontend UI           │
│  /console/delivery-challans  │
│  · Create DC                 │
│  · Dispatch fabric           │
│  · Track inward              │
│  · Billing against DC        │
└──────────────┬───────────────┘
               │  REST API Calls
               ▼
┌──────────────────────────────┐
│         API Layer            │
│  · Create DC API             │
│  · Update Dispatch API       │
│  · DC Billing API            │
│  · Stock Movement API        │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│    Business Logic Layer      │
│  · Dispatch Validation       │
│  · Remaining Stock Calc      │
│  · DC Status Workflow        │
│  · Partial Dispatch Handling │
│  · Billing Quantity Check    │
└──────┬───────────┬───────────┘
       │           │           │
       ▼           ▼           ▼
  ┌─────────┐ ┌─────────┐ ┌──────────┐
  │ DC Table│ │Stock DB │ │ Bills DB │
  └─────────┘ └─────────┘ └──────────┘
       │
       ▼
┌──────────────────────────────┐
│      Related Modules         │
│  · Orders Management         │
│  · Inventory Management      │
│  · Billing System            │
│  · Warehouse Tracking        │
└──────────────────────────────┘
```

---

## End-to-End DC Lifecycle

### Standard Delivery Challan Flow

```
Step 1 — Order Reference
        │
        │  An approved production order (LEO-YYYY-NNN)
        │  requires fabric to be dispatched
        │
        ▼
Step 2 — DC Creation
        │
        │  Admin / Warehouse user creates DC
        │  · Selects supplier / recipient
        │  · Links to production order
        │  · Fills fabric details (colour, lot, weight)
        │  · Adds process details (gauge, dia, loop length)
        │  · Adds remarks if needed
        │  · System generates DC-YYYY-NNNN
        │
        ▼
Step 3 — Stock Validation
        │
        │  Business logic checks:
        │  · Available stock quantity ≥ dispatch quantity
        │  · No duplicate dispatch for same lot
        │  · Quantity does not exceed order requirement
        │
        ▼
Step 4 — Submit for Approval
        │
        │  DC appears in Approval Status queue
        │  Approver reviews and approves / rejects
        │
        ▼
Step 5 — Dispatch Processing
        │
        │  On approval:
        │  · Fabric physically dispatched with DC printout
        │  · Stock reduced by dispatched quantity
        │  · DC Status → Partial (if more to dispatch)
        │                 Closed  (if fully dispatched)
        │
        ▼
Step 6 — Billing Integration
        │
        │  Billing module reads DC quantity
        │  Invoice generated against dispatched fabric
        │  Billed qty tracked vs remaining qty
        │
        ▼
Step 7 — Closure
        │
        │  When all fabric is dispatched and billed:
        │  DC Status → Closed
```

---

### Return Delivery Note Flow

```
Step 1 — Return Trigger
        │
        │  Fabric rejected (quality / wrong spec / excess)
        │  or processed fabric returned from vendor
        │
        ▼
Step 2 — Return DC Creation
        │
        │  Admin raises DC with (R) suffix
        │  · DC-YYYY-NNNN(R) generated
        │  · Document titled RETURN DELIVERY NOTE
        │  · Same fields as standard DC
        │  · Remarks field used for return reason
        │
        ▼
Step 3 — Approval
        │
        │  Submitted to Approval Status queue
        │  Approved by authorised user
        │
        ▼
Step 4 — Return Processing
        │
        │  · Fabric physically returned to supplier
        │  · Stock quantity increased (fabric back in inventory)
        │  · Billing module adjusts: billed qty reduced
        │  · DC(R) Status → Closed
```

---

## DC Status State Machine

```
         CREATE
            │
            ▼
       ┌─────────┐
       │  Draft  │  (DC created, not yet approved)
       └────┬────┘
            │  Submit for Approval
            ▼
       ┌─────────┐
       │ Pending │  (in Approval Status queue)
       └────┬────┘
       ┌────┴────┐
       ▼         ▼
  Approved     Rejected ──► Creator edits & resubmits
       │
       ▼
  ┌─────────┐
  │ Partial │  (some fabric dispatched; more pending)
  └────┬────┘
       │  All fabric dispatched / returned
       ▼
  ┌─────────┐
  │ Closed  │  (DC complete)
  └─────────┘
```

---

## How DC Connects to Each Module

### Orders Module

```
Order (LEO-2026-031)
       │
       │  "Create DC" button on Order Detail page
       ▼
DC pre-filled with:
  · order_id  → LEO-2026-031
  · Style No. → 1234
  · Buyer/Recipient details
  · Fabric colour and specification
```

One order can produce **multiple DCs** — for example:

- DC-2026-0023: 100 Kg dispatched to SHIVALAYA KNITS
- DC-2026-0028(R): 20 Kg returned from SHIVALAYA KNITS
- DC-2026-0032: 20 Kg dispatched to SHREE HARI TEXTILES All three linked to the same order `LEO-2026-031`.

---

### Stock Management

```
DC Dispatched (Closed)       →  Stock REDUCED  by dispatch qty
DC Return Closed (R)         →  Stock INCREASED by return qty
DC Partial                   →  Stock partially reduced (proportional to qty dispatched so far)
```

---

### PO & Bill Management

```
DC Quantity
      │
      ▼
Billing Module reads dispatched qty from DC
      │
      ▼
Invoice raised for supplier / vendor
      │
      ▼
Billed qty tracked — prevents double billing
Remaining qty = Total DC qty − Already billed qty
```

---

### Approval Status

```
DC submitted
      │
      ▼
Appears in Approval Status sidebar queue
(badge count increments — e.g., 31)
      │
      ▼
Approver acts → Approved / Rejected
      │
      ▼
DC approval_status updated
✓ Approved badge shown on DC card in list
```

---

### Supplier Management

Recipient details on the DC (name, address, phone, GSTIN) are pulled from the **Supplier Management** master. This ensures consistent, accurate supplier data on all dispatch documents.

---

## DC to Document Chain

```
Order: LEO-2026-031
    │
    ├── DC-2026-0023  (Closed, Approved)
    │   SHIVALAYA KNITS — 100 Kg dispatched
    │
    ├── DC-2026-0028(R)  (Partial, Approved)
    │   Harish — 20 Kg returned
    │
    └── DC-2026-0032  (Closed, Approved)
        SHREE HARI TEXTILES — 20 Kg dispatched
```

---

## PDF Document Generated

Every DC generates a single-page printable PDF:

|Section|Contents|
|---|---|
|Header|DC number, document type (DC or Return), date|
|Company block|LEO Fashions name, address, GST, mobile|
|Recipient block|Supplier name, address, GSTIN, linked order and style|
|Fabric table|Fabric details, lab card, lot, fin dia, bags/rolls, weight (Kg + g)|
|Summary row|Gross Total weight, Remarks|
|Process section|Knitting Gauge, Loop Length, Knitting Dia, Needle Drop|
|Footer|Receiver's signature space, Created by, Approved by, digital disclaimer|

The footer always reads:

```
*Digitally created — Requires no signature
```

---

## Performance & Database Considerations

|Concern|Approach|
|---|---|
|Fast DC lookup|DC numbers are indexed in the database|
|Large list performance|Pagination applied to DC list; lazy loading for large datasets|
|Stock query speed|Optimized stock queries with filtering by order and fabric type|
|Concurrent dispatch|Duplicate dispatch prevention enforced in business logic layer|
|Audit trail|All create / edit / approve actions logged to the Audits module|