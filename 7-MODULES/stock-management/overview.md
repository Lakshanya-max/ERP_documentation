## What Is Stock Management?

Stock Management tracks all physical inventory in Leo Fashion — raw materials coming in from suppliers, materials consumed during production, and finished goods dispatched to customers. Every movement in and out of stock is recorded.

---

## Why Stock Management Matters

|Without Stock Management|With Stock Management|
|---|---|
|Run out of material mid-production|Low stock alerts before it's too late|
|Over-order and waste money|Know exactly what's on hand|
|No visibility into consumption|Track material used per order|
|Manual counting errors|System-calculated real-time quantities|
|Supplier disputes on quantities|Every receipt is documented|

---

## Stock Item Categories

|Category|Examples|
|---|---|
|**Raw Material**|Cotton fabric, lining, thread, buttons, zippers|
|**Consumable**|Needles, chalk, tape, packaging material|
|**Finished Goods**|Completed garments ready for dispatch|

---

## Stock Item Record

|Field|Description|
|---|---|
|**Item Name**|e.g. "Cotton Fabric — Blue 40s"|
|**Category**|Raw material / Consumable / Finished goods|
|**Unit**|metres / kg / pieces / rolls / boxes|
|**Current Quantity**|Live count (auto-updated)|
|**Minimum Quantity**|Alert threshold — trigger reorder warning|
|**Cost per Unit**|For valuation (optional)|
|**Is Active**|Toggle inactive items without deletion|

---

## How Stock Moves

### Stock IN (Inbound)

|Source|Trigger|
|---|---|
|PO received|Admin marks PO as `received`|
|DC return (good condition)|Return status → `inspected` (good)|
|Manual adjustment|Admin adds a correction entry|

### Stock OUT (Outbound)

|Source|Trigger|
|---|---|
|Production started|Admin logs material issue to an order|
|DC dispatched|Finished goods removed from stock|
|Damaged / scrapped|Admin logs write-off entry|

---

## Stock Transaction Record

Every movement is recorded with:

|Field|Description|
|---|---|
|**Item**|Which stock item moved|
|**Type**|`in` / `out` / `adjustment`|
|**Quantity**|How much moved|
|**Reference Type**|`purchase_order` / `order` / `dc` / `return` / `manual`|
|**Reference ID**|The specific PO/Order/DC it's linked to|
|**Notes**|Reason (especially for adjustments)|
|**Date**|Transaction date|
|**Created By**|Which admin logged it|

---

## Stock Overview Screen

Admin sees:

```
┌─────────────────────────────────────────────────────┐
│  STOCK MANAGEMENT                  [Add Item] [Search]│
├──────────────────────────────────────────────────────┤
│  🔴 LOW STOCK ALERTS (3 items)                       │
│  ┌─────────────────────────────────────────────────┐ │
│  │ Thread — White | Current: 2 rolls | Min: 5 rolls│ │
│  └─────────────────────────────────────────────────┘ │
├──────────────────────────────────────────────────────┤
│  Item Name       │ Category   │ Qty    │ Unit │ Status│
│  Cotton Fabric   │ Raw Mat.   │ 450    │ mtrs │ ✅ OK │
│  Thread — White  │ Raw Mat.   │ 2      │ rolls│ 🔴 Low│
│  Zippers         │ Raw Mat.   │ 1,200  │ pcs  │ ✅ OK │
│  White Shirts    │ Fin. Goods │ 80     │ pcs  │ ✅ OK │
└──────────────────────────────────────────────────────┘
```

---

## Stock Item Detail Screen

Clicking any item shows:

- Current quantity (large, prominent)
- Transaction history (in/out timeline)
- Low stock indicator
- Quick action: **Log Adjustment**

---

## Low Stock Alerts

When `current_quantity < minimum_quantity`:

- Item is highlighted in red on stock overview
- Alert badge shows count in sidebar nav
- Admin can click through to raise a PO directly from the alert

---

## Manual Adjustments

Admin can log a manual adjustment when:

- Physical count doesn't match system count (periodic stock take)
- Material is damaged/scrapped
- Entry correction is needed

Adjustments require a mandatory **reason** and are always logged in audit trail.

---

## Stock Valuation (Optional)

If cost per unit is entered per item:

- System calculates total stock value = qty × cost per unit
- Visible on stock overview as aggregate
- Feeds into Profit & Loss as inventory value

---

## Business Rules

- Stock cannot go below zero — system blocks out-movements that would result in negative stock
- Every transaction must have a reference (PO, order, DC) or be a manual adjustment
- Manual adjustments require a reason — mandatory
- Finished goods stock is updated automatically when a DC is created
- Damaged returns are tracked separately from good stock

---

## Related Documents

- PO Overview — How PO receipt adds stock
- DC Overview — How dispatches reduce stock
- DC Returns — How returns add back to stock
- Profit & Loss — Stock valuation in P&L
- DB Schema — stock_items