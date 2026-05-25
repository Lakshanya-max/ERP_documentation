## What Is Seconds Stock?

Seconds Stock refers to **substandard, defective, or damaged inventory** that cannot be dispatched to customers as first-quality goods. This includes raw materials rejected on receipt and finished garments that failed quality inspection.

Seconds are tracked separately from fresh stock to maintain clean inventory records and enable recovery decisions (rework, discount sale, scrap).

---

## Why Track Seconds Separately?

|Reason|Detail|
|---|---|
|Accurate fresh stock count|Defective units don't inflate usable inventory|
|Recovery tracking|Know how many seconds are reworkable vs scrappable|
|Supplier accountability|Trace which supplier delivered defective material|
|Financial clarity|Seconds have lower/zero value — affects stock valuation|
|Quality improvement|Pattern of seconds reveals production or supplier issues|

---

## What Becomes Seconds?

### Raw Material Seconds

|Scenario|How It Happens|
|---|---|
|Supplier delivers damaged fabric|Admin rejects on PO receipt, logs as seconds|
|Material damaged during storage|Admin logs manual adjustment from fresh → seconds|
|Wrong spec material|Material can't be used, logged as seconds|

### Finished Goods Seconds

|Scenario|How It Happens|
|---|---|
|Failed quality check|QC marks garment as defective during inspection|
|Returned goods — damaged|DC return inspected as damaged, added to seconds|
|Production defect (stitching, print, sizing)|Admin logs after QC review|

---

## Seconds Categories

|Category|Description|Typical Action|
|---|---|---|
|**Reworkable**|Defect can be fixed (loose stitching, missing button)|Create rework task|
|**Discountable**|Minor defect, can be sold at lower price|Dispatch at discount|
|**Scrap**|Unusable, cannot be sold or reworked|Write off|

---

## Seconds Stock Screen

```
┌──────────────────────────────────────────────────────────┐
│  SECONDS STOCK                              [Log Entry]  │
├──────────────────────────────────────────────────────────┤
│  Category: [All ▾]  Type: [All ▾]  Search: [__________] │
├──────────────────────────────────────────────────────────┤
│  Item           │ Defect Type   │ Qty  │ Category  │Action│
│  Cotton Fabric  │ Water stain   │  12  │ Scrap     │[Log] │
│  Finished Shirt │ Stitching gap │   8  │ Reworkable│[Log] │
│  Finished Trouser│ Size mismatch│   3  │ Discountable│[Log]│
├──────────────────────────────────────────────────────────┤
│  Total Seconds: 23 units                                 │
└──────────────────────────────────────────────────────────┘
```

---

## How Seconds Enter the System

### Method 1 — At PO Receipt

```
Admin marks PO as received
        │
        ▼
System asks: Any items rejected?
        │
       YES
        │
        ▼
Admin enters:
  • Quantity rejected
  • Defect description
  • Category (reworkable / scrap)
        │
        ▼
Rejected qty → Seconds Stock
Accepted qty → Fresh Stock
```

### Method 2 — Transfer from Fresh Stock (QC Fail)

```
Admin reviews completed garments
        │
        ▼
QC finds defect
        │
        ▼
Admin logs: Fresh → Seconds transfer
  • Item + quantity
  • Defect type
  • Seconds category
        │
        ▼
Fresh qty decreases
Seconds qty increases
Both transactions logged
```

### Method 3 — DC Return (Damaged)

```
Customer returns goods
        │
        ▼
Admin inspects → condition: DAMAGED
        │
        ▼
Goods added to Seconds Stock
Category assigned (reworkable / scrap)
Transaction logged: reference = DC Return
```

---

## Resolving Seconds

### Option A — Rework

```
Admin creates rework task for worker
Worker fixes the defect
QC re-inspects
        │
   PASS │  FAIL
        │
Fresh   Remains in
Stock   Seconds (downgrade to scrap)
```

### Option B — Discount Sale

```
Admin decides to sell at lower price
Creates special order with reduced rate
DC issued as normal
Seconds qty decreases
```

### Option C — Scrap / Write Off

```
Admin logs write-off
  • Quantity
  • Reason
  • Any scrap value recovered
Seconds qty decreases
Loss recorded in P&L (if value tracked)
```

---

## Seconds Stock Detail View

Clicking any seconds item shows:

- Current quantity by defect category
- Source history (which PO / DC Return / transfer created it)
- Resolution history (reworked / scrapped / sold)
- Linked supplier (for raw material seconds — for accountability)

---

## Supplier Accountability

When raw material seconds come from a PO:

- System links seconds to the supplier automatically
- Admin can raise a **supplier quality complaint** (notes field)
- Repeated seconds from the same supplier are visible in supplier history
- Can be used to negotiate credit notes or price adjustments

---

## Business Rules

- Seconds stock is tracked separately — never mixed with fresh stock in counts
- Every seconds entry must have a defect description
- Seconds cannot be dispatched via normal DC (system blocks it)
- To sell seconds, admin must create a special marked order
- Write-offs require admin confirmation and reason — cannot be undone
- Reworked seconds re-enter fresh stock only after QC re-approval

---

## Related Documents

- Fresh Stock — First-quality inventory
- Stock Overall Workflow — Full stock flow
- DC Returns — Source of damaged returns
- Profit & Loss — Write-off losses