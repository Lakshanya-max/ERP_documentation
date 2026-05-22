# Orders Module — Overview

## Purpose

The Orders module is the central production hub of LEO Fashions ERP. It captures every garment production order placed by a buyer (e.g., Zudio), tracks all associated costs, manages fabric and trim planning, and drives downstream procurement and delivery workflows.

---

## Module Location

```
Sidebar → Orders
URL     → /console/orders
```

---

## Order Number Format

```
LEO  -  2026  -  036
 │        │       │
 │        │       └─ Sequential number (auto-generated, zero-padded)
 │        └───────── Calendar year at creation
 └────────────────── Fixed company prefix
```

---

## Order Classifications

|Classification|Description|
|---|---|
|**Bulk**|Full production run for the buyer|
|**Sample**|Pre-production sample garments for buyer approval|

Both types share the same order structure. Quantities, fabric, and trim data are stored separately for Bulk and Sample within the same order record using a `type` flag.

---

## Sub-Modules Inside an Order

```
Order (LEO-YYYY-NNN)
├── 1. Order Summary         → Identity, buyer, pricing, dates, status
├── 2. Order Quantity        → Size-wise buyer piece count (Bulk / Sample)
├── 3. Cutting Quantity      → Production count after tolerance buffer
├── 4. Style Type & Print    → Panel print configuration
├── 5. Fabric                → Colour, weight, GSM, yarn & fabric process costs
├── 6. Production Trim       → Trims used during manufacturing
├── 7. Packing Trim          → Trims used during packing
├── 8. Other Prices          → Embroidery, logistics, testing, etc.
├── 9. Stages                → Production milestone tracking
├── 10. Files                → Attachments — tech packs, images, specs
└── 11. Delivery Challan     → DC created from this order
```

---

## Order Summary Fields

|Field|Description|Example|
|---|---|---|
|Order Number|Auto-generated unique ID|LEO-2026-036|
|Classification|Bulk or Sample|Bulk|
|Unit|Production unit|Main Unit|
|Buyer|External client|Zudio|
|Name|Internal reference name|nn|
|Style|Garment style code|ejr|
|Description|Optional free text|—|
|CMT Price (per Pcs)|Cut-Make-Trim charge per piece billed to buyer|₹ 10|
|Delivery Date|Target delivery to buyer|19 May, 2026|
|Shipment Date|Target dispatch date|19 May, 2026|
|Status|Current production state|In Progress|
|Approval Status|Approval workflow state|Draft|

---

## Order Quantity

Size-wise buyer-facing piece count. Maintained separately for Bulk and Sample.

|Field|Description|
|---|---|
|Size|Garment size (e.g., `8`, `S`, `M`, `L`, `XL`)|
|Quantity|Pieces ordered for that size|
|Total Quantity|Sum across all sizes|

---

## Cutting Quantity

Production-floor quantity after applying a tolerance buffer to cover fabric defects and wastage.

```
cutting_qty = ceil( order_qty × (1 + tolerance% / 100) )
```

**Example — LEO-2026-036:**

|Size|Order Qty|Tolerance|Cutting Qty|
|---|---|---|---|
|8|3|3%|4|

|Field|Description|
|---|---|
|Base Total|Sum of raw order quantities|
|Tolerance|Percentage buffer — default 3%|
|Total Quantity (with tolerance)|Final count sent to cutting floor|

---

## Style Type & Print Panel

When enabled, specifies which garment panels carry print work (e.g., `front`, `back`, `sleeve`). Drives the `PANEL_PRINTING` charge in Other Prices and fabric consumption planning.

|Field|Description|
|---|---|
|Enabled|Yes / No|
|Panel Name|e.g., `front`|

---

## Fabric

One entry per fabric colour used in the order.

|Field|Description|
|---|---|
|Colour|Fabric colour name (e.g., `Jersey-Blue-Bottom`)|
|Colour Code|Pantone / TCX reference (e.g., `TCX-11-0104`)|
|Yarn Required?|Whether yarn needs sourcing|
|Fabric Required?|Whether fabric needs sourcing|
|Fabric Weight|Total weight in Kg|
|Cutted Fabric|Actual fabric cut|
|Fabric Unit Price|Price per unit|
|Fabric Dia|Fabric diameter|
|Fabric GSM|Grams per square metre|
|Piece Weight|Weight of one finished garment (grams)|
|Due Date|Fabric in-house deadline|
|Remarks|Free-text notes|
|Total Piece Weight|Sum of piece weights across all fabrics|

### Yarn Process Costs

|Process|Description|
|---|---|
|YARN_DYEING|Cost to dye the yarn|
|WINDING|Winding process cost|
|KNITTING|Knitting cost|
|DYING|Additional dying cost|

### Fabric Process Costs

|Process|Process|
|---|---|
|TUBULAR_COMPACTING|OW_COMPACTING|
|STENDER|DRYER|
|WASHING|RISING|
|ROTARY_PRINTING|PEACH_FINISH|
|SUEDING|CROPPING|
|SHEARING|TUMBLE_DRYER|
|HEAT_SETTING|SIDE_JOINING|
|MERCERISATION||

---

## Production Trim

Trims consumed during manufacturing (e.g., labels sewn into the garment).

|Field|Description|
|---|---|
|Trim Type|e.g., `Main Tag`|
|Unit Price|Cost per trim unit|
|Remarks|Notes|
|Size / Quantity|Trim count per size|
|Total Quantity|Sum across all sizes|
|Total Price|`unit_price × total_quantity`|

---

## Packing Trim

Same structure as Production Trim. Tracked separately as packing trims are applied at a different stage.

---

## Other Prices

Additional per-order charges.

|Item|Description|
|---|---|
|PANEL_PRINTING|Fabric panel printing charges|
|EMBROIDERY|Embroidery work charges|
|ACID_WASH|Acid wash treatment|
|TIE_AND_DYE|Tie & dye process|
|TESTING|Lab / quality testing fees|
|LOGISTICS|Freight and transport|
|FORWARDING_DOCUMENTS|Customs and documentation|

Each item: `Unit Price` · `Quantity` · `Total` · `Remarks` **Subtotal** = sum of all Other Price totals.

---

## Other Details (Audit Fields)

|Field|Description|
|---|---|
|Created By|User who created the order|
|Modified By|User who last saved the order|
|Created On|Server timestamp at creation|
|Modified On|Server timestamp at last save|

These are read-only and always system-populated.

---

## Order Actions

|Action|Description|
|---|---|
|Print|Generates and downloads the 3-page order PDF|
|Create DC|Creates a Delivery Challan pre-filled from this order|
|Edit|Switches the detail view into editable form mode|
|Submit for Approval|Sends the order to the Approval Status queue|

---

## Status Badge Reference

|Badge|Colour|Meaning|
|---|---|---|
|Draft|Grey|Not yet submitted|
|In Progress|Teal|Active in production|
|Completed|Green|All stages done|
|Bulk|Blue outline|Bulk classification|
|Approved|Green|Approval granted|
|Rejected|Red|Approval denied|