# Stock Management — Overall Workflow

## The Complete Stock Lifecycle

This document traces how inventory moves through Leo Fashion — from supplier delivery to customer dispatch — covering both fresh and seconds stock at every stage.

---

## Master Flow Diagram

```
┌──────────────────────────────────────────────────────────────────┐
│                    STOCK MANAGEMENT WORKFLOW                      │
└──────────────────────────────────────────────────────────────────┘

INBOUND FLOWS (Stock IN)
─────────────────────────

  [Supplier Delivery]          [DC Return - Good]      [Manual Adj.]
        │                             │                      │
        ▼                             ▼                      ▼
  Admin marks PO           Admin inspects return      Admin logs
  as "received"            → condition: GOOD          adjustment
        │                             │                      │
        ▼                             ▼                      ▼
  QC Check on receipt          ┌──────────────┐      Reason required
        │                      │  Fresh Stock  │      Audit logged
   PASS │  FAIL                │   increases   │
        │      │               └──────────────┘
        ▼      ▼
  Fresh      Seconds
  Stock  +   Stock
  increases  increases


PRODUCTION FLOW (Stock MOVES)
──────────────────────────────

  [Production Order Created]
           │
           ▼
  Admin issues raw materials to order
           │
           ▼
  Fresh Raw Material stock decreases
  (OUT transaction, ref: Order ID)
           │
           ▼
  [Production in progress]
           │
           ▼
  QC on finished garments
           │
      PASS │  FAIL
           │       │
           ▼       ▼
  Fresh Finished   Seconds Stock
  Goods increase   increases
  (IN, ref: Order) (defect logged)


OUTBOUND FLOWS (Stock OUT)
───────────────────────────

  [DC Created - Dispatch]       [Write Off]      [DC Return - Damaged]
          │                         │                     │
          ▼                         ▼                     ▼
  Fresh Finished             Admin logs            Seconds Stock
  Goods decreases            scrap/write-off       increases
  (OUT, ref: DC)             Reason required       (OUT from fresh
                             P&L loss recorded      if transferred)
```

---

## Transaction Reference Map

Every stock movement must reference a source document:

|Movement|Source Reference|Type|
|---|---|---|
|Supplier material received|Purchase Order|IN|
|Material issued to production|Order|OUT|
|Finished goods completed|Order|IN|
|Goods dispatched to customer|Delivery Challan|OUT|
|Good returns from customer|DC Return|IN|
|Damaged returns from customer|DC Return|IN (seconds)|
|Fresh → Seconds transfer|Manual / QC|Adjustment|
|Seconds → Scrap write-off|Manual|OUT|
|Stock count correction|Manual Adjustment|Adjustment|

---

## Stock Level States

At any point, each item has two running balances:

```
┌────────────────────────────────────────────┐
│  Cotton Fabric — Blue                      │
│                                            │
│  🟢 Fresh Stock:     450 metres            │
│  🟡 Seconds Stock:    12 metres            │
│  ─────────────────────────────────         │
│  Total Physical:     462 metres            │
│                                            │
│  Minimum (Fresh):    100 metres  🔴 Alert? │
└────────────────────────────────────────────┘
```

The system always shows fresh and seconds separately. Total physical is informational only.

---

## Daily Stock Operations (Admin Routine)

### Morning Check

1. Open **Stock Overview**
2. Review **Low Stock Alerts** — items below minimum
3. Raise POs for any critical shortages
4. Check **Seconds Pending Resolution** — reworkable items

### During Production

1. When an order starts a new stage, log material issue
2. Fresh raw material stock decreases
3. At end of stage, log finished goods count

### On Supplier Delivery

1. Open PO → Mark as **Received**
2. Enter quantity received (may differ from PO)
3. Flag any defective material as seconds
4. Fresh stock updates automatically

### On DC Creation

1. Create DC for a completed order
2. Finished goods stock decreases automatically
3. If return comes in — log DC return and inspect

---

## Stock Reconciliation (Weekly)

Admin should periodically verify system stock vs physical count:

```
1. Export current stock report
2. Physical count of warehouse / storage
3. Compare item by item
4. Log adjustments for any variances
   (mandatory reason: "Weekly stock take — variance correction")
5. Audit trail records all adjustments
```

Recommended: every Friday or Monday before the week begins.

---

## Low Stock Alert Flow

```
System checks: current_qty < minimum_qty
        │
       YES
        │
        ▼
Alert badge in sidebar nav
Item highlighted red on Stock Overview
        │
        ▼
Admin reviews alert
        │
        ▼
Admin clicks [Raise PO] from the item
        │
        ▼
PO creation form pre-filled with:
  • Supplier (last used for this item)
  • Item name
  • Suggested quantity (min qty × 2)
        │
        ▼
Admin confirms and sends PO
Alert cleared when PO is created
(and fully cleared when stock received)
```

---

## Stock Valuation Flow (Optional)

If cost per unit is set on items:

```
Each fresh stock transaction carries a value:
  IN  → quantity × cost per unit  (adds value)
  OUT → quantity × cost per unit  (removes value)

Total fresh stock value = Σ (all items: qty × cost)
Shown on Stock Overview as aggregate
Reported in P&L as inventory asset
```

Seconds stock is valued at 0 (or a custom reduced value per item).

---

## Key Business Rules

|Rule|Detail|
|---|---|
|No negative stock|System blocks any OUT that would result in negative fresh stock|
|Mandatory reference|Every transaction must link to a document or be a manual adjustment|
|Manual adjustment reason|Mandatory — logged in audit trail|
|Fresh and seconds separate|Cannot combine in a single transaction|
|Write-off is irreversible|Once scrapped, quantity cannot be recovered|
|Stock check on DC creation|System validates sufficient fresh finished goods before DC is created|

---

## Related Documents

- Fresh Stock — First-quality inventory detail
- Seconds Stock — Defective/substandard inventory detail
- PO Overview — Inbound stock trigger
- DC Overview — Outbound stock trigger
- DC Returns — Returns and their stock impact
- Profit & Loss — Stock valuation in financials