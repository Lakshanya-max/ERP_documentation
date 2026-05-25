# Orders — Overview

## What Is the Orders Module?

The Orders module is the **core of LEO Fashions**. Every garment production activity starts with an order. Customers place orders specifying what they want — the type of garment, style, fabric, quantity, and delivery date — and the factory fulfills it through a structured manufacturing process.

---

## Order Types

|Type|Description|Example|
|---|---|---|
|**Bulk**|Large quantity production|1000 t-shirts|
|**Sample**|Trial piece for quality approval|1 prototype hoodie|

---

## What an Order Contains

```
ORDER
├── Basic Info
│   ├── Order ID     → LEO-2026-008
│   ├── Name         → "name"
│   ├── Classification → Bulk / Sample
│   ├── Unit         → Main Unit / Leo-unit-2
│   ├── Style        → M / Full Sleeve
│   ├── CMT Price    → ₹90 per piece
│   └── Delivery Date→ 13 Jan 2026
│
├── Quantities (size-wise)
│   ├── XS: 100, S: 200, M: 150...
│   └── Cutting Qty = +3% tolerance
│
├── Fabric
│   ├── Color, Weight, GSM, Dia
│   ├── Piece Weight
│   └── Process costs (15 processes)
│
├── Yarn
│   ├── Type, Weight, Price
│   └── Process costs (4 processes)
│
├── Production Trim
│   └── Main Label, qty, price
│
├── Packing Trim
│   └── Carton Box, qty, price
│
└── Other Prices
    └── Embroidery, Printing, Logistics etc.
```

---

## Order Status

|Status|Meaning|
|---|---|
|`Draft`|Created, awaiting admin approval|
|`In Progress`|Approved, manufacturing ongoing|
|`Completed`|All 8 stages done, delivered|

---

## Key Rules

- Order ID auto-generated: `LEO-YYYY-XXX`
- 3% tolerance auto-added to cutting quantity
- Admin must approve before manufacturing begins
- After approval, 8 stage records created automatically
- Order completes only when all 8 stages = Completed
- Users see only their own orders
- Admin sees all orders