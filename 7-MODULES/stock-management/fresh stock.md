# Fresh Stock — Leo Fashion

## What Is Fresh Stock?

Fresh Stock refers to **first-quality, defect-free inventory** — raw materials received in good condition from suppliers, and finished garments that have passed quality inspection and are ready for dispatch to customers.

This is the primary stock category in Leo Fashion. All normal production and dispatch operations use fresh stock.

---

## Fresh Stock Categories

### 1. Fresh Raw Materials

Materials received from suppliers that are:

- Undamaged and within spec
- Correct quantity matching PO
- Accepted after basic quality check on receipt

Examples:

|Item|Unit|Typical Source|
|---|---|---|
|Cotton fabric|metres|Fabric supplier|
|Lining material|metres|Fabric supplier|
|Thread (colours)|cones|Thread supplier|
|Buttons|pieces|Accessories supplier|
|Zippers|pieces|Accessories supplier|
|Elastic|metres|Accessories supplier|
|Packaging material|pieces|Packaging supplier|

### 2. Fresh Finished Goods

Completed garments that have:

- Passed quality check (stitching, sizing, finishing)
- No visible defects
- Ready to be dispatched via DC

---

## How Fresh Stock Enters the System

### Raw Material — Via PO Receipt

```
Supplier delivers materials
         │
         ▼
Admin marks PO as "received"
         │
         ▼
System prompts: Enter received quantity
(may differ from PO quantity if short-delivered)
         │
         ▼
Fresh stock quantity increases
Transaction logged: type=IN, reference=PO
```

### Finished Goods — Via Production Completion

```
All order stages completed
         │
         ▼
QC passes garments as fresh
         │
         ▼
Admin logs finished goods into stock
         │
         ▼
Fresh finished goods quantity increases
Transaction logged: type=IN, reference=Order
```

### DC Returns (Good Condition)

```
Customer returns goods
         │
         ▼
Admin inspects → condition: GOOD
         │
         ▼
Goods added back to fresh finished goods stock
Transaction logged: type=IN, reference=DC Return
```

---

## How Fresh Stock Leaves the System

|Reason|Action|Transaction Type|
|---|---|---|
|Production started (raw material issued)|Admin logs material issue to order|OUT|
|Dispatch to customer|DC created|OUT|
|Material transferred to seconds (damaged)|Admin logs adjustment|OUT (from fresh) + IN (to seconds)|

---

## Fresh Stock Screen

```
┌──────────────────────────────────────────────────────────┐
│  FRESH STOCK                    [Add Item] [Log Movement] │
├──────────────────────────────────────────────────────────┤
│  Category: [All ▾]    Search: [____________]             │
├──────────────────────────────────────────────────────────┤
│  Item Name           │ Category   │ Qty    │ Unit │Alert │
│  Cotton Fabric Blue  │ Raw Mat.   │  450   │ mtrs │  —   │
│  Cotton Fabric White │ Raw Mat.   │   80   │ mtrs │ 🔴   │
│  Thread — Black      │ Raw Mat.   │   12   │ cone │  —   │
│  Finished Shirts     │ Fin. Goods │  200   │ pcs  │  —   │
│  Finished Trousers   │ Fin. Goods │   45   │ pcs  │  —   │
└──────────────────────────────────────────────────────────┘
```

Low stock alert (🔴) fires when `current_qty < minimum_qty`.

---

## Fresh Stock Item Detail

Clicking an item opens:

- Current quantity (large display)
- Minimum quantity threshold
- Full IN/OUT transaction history with dates and references
- Quick actions:
    - **Log Manual Adjustment** (with reason)
    - **Raise PO** (for raw materials on low stock)

---

## Quality Acceptance on Receipt

When a PO is received, admin can note:

- **Full receipt** — all units accepted as fresh
- **Partial receipt** — some accepted, some rejected (rejected goes to supplier or logged as seconds)
- **Quantity variance** — received less than ordered (PO stays partially open)

---

## Business Rules

- Fresh stock can never go below zero — system blocks it
- All fresh stock movements must reference a document (PO, Order, DC, Return) or be a manual adjustment
- Manual adjustments to fresh stock require a mandatory reason
- Transferring from fresh to seconds requires admin action and reason
- Fresh finished goods are only created from orders that have passed quality check

---

## Related Documents

- Seconds Stock — Defective/substandard stock
- Stock Overall Workflow — Full stock flow
- PO Overview — How PO receipt adds fresh stock
- DC Overview — How dispatch removes fresh stock