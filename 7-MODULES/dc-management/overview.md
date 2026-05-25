# DC Management — Overview

## What Is DC Management?

DC (Delivery Challan) Management handles the movement of materials **from LEO Fashions to external suppliers for processing** — such as knitting, dyeing, washing, or printing. Every time material leaves the factory for processing and comes back, it is tracked through a DC.

---

## DC Types

|Type|Purpose|
|---|---|
|**Processing DC**|Send material to supplier for process work|
|**General DC**|General material movement|
|**Return DC**|Handle return of unsatisfied or damaged goods|

---

## DC Record — Full Details

```
DC Contains:
├── DC ID          → DC-2026-0028(R)
├── DC Date        → 5/5/2026
├── Order Link     → LEO-2026-031
├── Supplier From  → SHIVALAYA KNITS
├── Supplier To    → Harish
├── Address        → 3/13 A east car street, Thoothukudi
├── Department     → Fabric
├── Process        → Knitting
├── Classification → Bulk
├── Style Number   → 1234
├── Total Sent     → 20 Kg
├── Received Back  → 5 Kg
├── Remaining      → 15 Kg
├── Total Amount   → ₹0 (bill not yet raised)
├── DC Status      → Partial
├── Inward Status  → Inward: Partial
├── Bill Status    → Bill: Open
└── Approval Status→ Approved
```

---

## DC Tabs

|Tab|Purpose|
|---|---|
|Basic Details|Supplier info, order, process, amounts|
|DC Inwards|Return entries when goods come back|
|DC Bills|Supplier processing charges|
|Remaining Stocks|Pending material table|

---

## DC Status Flow

```
Partial + Pending
    ↓ Admin approves
Partial + Approved
    ↓ Some goods returned
Inward: Partial
    ↓ All goods returned
Inward: Complete

Bill: Open → Bill: Paid (runs independently)
```

---

## Processing Loss

Normal material loss during processing:

```
Sent     = 20 Kg
Returned = 19 Kg
Loss     = 1 Kg

Causes:
- Water evaporation during dyeing
- Fabric shrinkage
- Machine wastage
- Dye absorption
```

---

## Processes Tracked

|Process|Department|
|---|---|
|Knitting|Fabric|
|Dyeing|Fabric|
|Washing|Fabric|
|Compacting|Fabric|
|Printing|Fabric|
|Embroidery|Fabric|
|Yarn Dyeing|Yarn|
|Winding|Yarn|

---

## Key Rules

- DC must be linked to an order
- Admin must approve before material is sent
- Every return triggers a DC Inward entry
- Processing loss is automatically recorded
- Bill is tracked separately from inward status
- Only verified suppliers can be selected