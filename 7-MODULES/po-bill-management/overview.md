# PO & Bill Management — Overview

## What Is PO & Bill Management?

When the factory needs to **buy raw materials** (yarn, fabric, trims) from suppliers, a Purchase Order (PO) is created. This module tracks every purchase — what was ordered, from whom, how much was received, and what was paid.

---

## Material Categories

|Category|What It Is|
|---|---|
|Yarn|Raw thread/yarn for fabric making|
|Fabric|Ready-made fabric for cutting|
|Production Trim|Labels, buttons, zippers, threads|
|Packing Trim|Carton boxes, poly bags, stickers|

---

## PO Record — Full Details

```
PO Contains:
├── PO ID          → PO-2026-0051
├── Supplier       → SUREYA TRADERS
├── Material       → Yarn
├── Order Link     → LEO-2026-002
├── Total Qty      → 1,000 Kg
├── Received Qty   → 0 Kg
├── Remaining Qty  → 1,000 Kg
├── Rate           → ₹10 per Kg
├── GST            → 5%
├── Total Amount   → ₹10,500
├── Delivery Address → Factory address
├── PO Status      → Open / Partial / Closed
└── Approval Status→ Pending / Approved
```

---

## PO Tabs

|Tab|Purpose|
|---|---|
|Basic Details|Supplier info, yarn details, amounts|
|Inwards|Material receipt entries|
|Bills|Supplier invoices|
|Remaining Stocks|Pending delivery table|

---

## PO Status Flow

```
Open → Partial → Closed
```

|Status|Meaning|
|---|---|
|`Open`|Approved, no material received yet|
|`Partial`|Some material received|
|`Closed`|Fully received|
|`Approved`|Admin verified the PO|

---

## Key Calculations

|Calculation|Formula|
|---|---|
|Subtotal|Qty × Rate|
|GST Amount|Subtotal × GST%|
|Total Amount|Subtotal + GST|
|Remaining|Total Ordered − Received|

---

## Key Rules

- Only verified suppliers can be selected
- Only admin can create and approve POs
- PO must be linked to an order
- Every material receipt triggers a PO Inward entry
- PO auto-closes when remaining = 0