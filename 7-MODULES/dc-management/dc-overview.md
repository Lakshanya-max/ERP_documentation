# DC Management — Overview

## Purpose

The Delivery Challan (DC) Management module handles all fabric movement in and out of LEO Fashions — dispatching fabric to processing units, receiving fabric inward, and returning fabric to suppliers. Every physical fabric movement is backed by a legally valid, digitally approved challan document.

---

## Module Location

```
Sidebar → DC Management
URL     → /console/delivery-challans
```

---

## DC Number Format

```
DC  -  2026  -  0028  (R)
 │      │        │      │
 │      │        │      └─ Optional suffix — present only on Return Delivery Notes
 │      │        └──────── Sequential number (auto-generated, zero-padded to 4 digits)
 │      └───────────────── Calendar year at creation
 └──────────────────────── Fixed module prefix
```

---

## DC Types

|Type|Number Format|Description|
|---|---|---|
|**Delivery Challan**|`DC-YYYY-NNNN`|Fabric dispatched outward to a processing unit or vendor|
|**Return Delivery Note**|`DC-YYYY-NNNN(R)`|Fabric returned back to the supplier|

---

## DC List Page

```
┌────────────────────────────────────────────────────────────┐
│ ←   Delivery Challans                      [🔔 2]  [🏠]   │
├────────────────────────────────────────────────────────────┤
│ [🔍 search...]              [Sort: By DC Number     ▼]    │
│ [Supplier ▼]  [Status ▼]  [Department ▼]      [🖨 Print]   │
├────────────────────────────────────────────────────────────┤
│  DC-2026-0028(R)  Partial  ✓ Approved          [↗] [🖨]   │
│  SHIVALAYA KNITS | Fabric                                  │
│  Order: LEO-2026-031 | 1 fabric type(s)  Qty: 20 Kg       │
│  Modified: a day ago                                       │
├────────────────────────────────────────────────────────────┤
│  DC-2026-0032    Closed   ✓ Approved           [↗] [🖨]   │
│  SHREE HARI TEXTILES | Fabric                              │
│  Order: LEO-2026-035 | 1 fabric type(s)  Qty: 20 Kg       │
│  Modified: 2 days ago                                      │
├────────────────────────────────────────────────────────────┤
│  DC-2026-0023    Closed   ✓ Approved           [↗] [🖨]   │
│  SHIVALAYA KNITS | Fabric                                  │
│  Order: LEO-2026-031 | 1 fabric type(s)  Qty: 100 Kg      │
│  Modified: 15 days ago                                     │
│                                    [+ Delivery Challan]    │
└────────────────────────────────────────────────────────────┘
```

### Filter Controls

|Control|Options|
|---|---|
|Search|Searches by DC number, supplier, order number|
|Sort|By DC Number|
|Supplier|Filter by supplier name|
|Status|`Partial` · `Closed`|
|Department|Filter by department|
|Print|Bulk print filtered list|

### DC Card Fields

|Field|Description|
|---|---|
|DC Number|Unique identifier with optional `(R)` suffix|
|Status Badge|`Partial` (orange) · `Closed` (grey)|
|Approval Badge|`✓ Approved` (green)|
|Supplier|Supplier name and material type|
|Order Link|Linked production order (e.g., `LEO-2026-031`)|
|Fabric Type Count|Number of fabric types in the DC|
|Quantity|Total fabric weight in Kg|
|Timestamp|Relative time of last modification|
|Share (↗)|Open or share the DC detail|
|Print (🖨)|Generate and download the DC PDF|

---

## DC Status Values

|Status|Colour|Meaning|
|---|---|---|
|`Partial`|Orange|Some fabric dispatched; remaining quantity still pending|
|`Closed`|Grey|All fabric fully dispatched or returned; DC is complete|

---

## DC Detail — All Fields

### Header Section

|Field|Example|
|---|---|
|DC Number|DC-2026-0028(R)|
|Document Title|RETURN DELIVERY NOTE or DELIVERY CHALLAN|
|Date|05/05/26|

### Company Section (LEO Fashions)

|Field|Value|
|---|---|
|Company Name|LEO Fashions|
|Address|576/2B, Ayyar Thottam, Rayarpalayam, Tirupur Main Road, Palladam - 641 664|
|GST No|33AAEFE5039K1ZH|
|Mobile|8668084013|

### Recipient Section

|Field|Example|
|---|---|
|Name|M/s. Harish|
|Address|3/13 A east car street, Thoothukudi - 628907|
|Phone|6374777961|
|GSTIN|22AAAAA1234W1W2|
|Order No.|LEO-2026-031|
|Style No.|1234|

### Fabric Details Table

|Column|Description|
|---|---|
|Fabric Details|Colour name, TCX colour code, yarn count, cotton type, quantity|
|Lab Card No.|Lab card reference number|
|Lot No.|Fabric lot / batch number|
|Fin Dia|Finished diameter of the fabric|
|Bags / Rolls|Number of bags or rolls|
|Weight — Kilo|Weight in kilograms|
|Weight — Gram|Weight in grams|

**Example fabric entry:**

```
Colour     : Single Jersey-Blue-Bottom
TCX Colour : 11-0103
Yarn       : 10s, 100% cotton Combed VL, 100 Kg
Weight     : 20 Kg
```

### Summary Row

|Field|Example|
|---|---|
|Gross Total|20 Kg|
|Remarks|Free-text field for any notes about the dispatch or return|

### Process Section

|Field|Example|
|---|---|
|Knitting Gauge|4646|
|Loop Length|7676|
|Knitting Dia|76|
|Needle Drop|NO|

### Footer Section

|Field|Value|
|---|---|
|Receiver's Signature|Physical sign-off space on printed copy|
|Created By|admin|
|Approved By|Admin|
|Disclaimer|*Digitally created — Requires no signature|

---

## DC Actions

|Action|Description|
|---|---|
|+ Delivery Challan|Create a new DC from the list page|
|Create DC (from Order)|Pre-filled DC triggered from the Orders module|
|Edit|Modify DC fields before closing|
|Print (🖨)|Download the DC PDF|
|Share (↗)|View or share the DC detail|
|Submit for Approval|Send DC to the Approval Status queue|

---

## Primary Actors

|Actor|Role|
|---|---|
|Admin|Full access — create, edit, approve, delete DC|
|Warehouse / Dispatch User|Create and dispatch DCs, handle inward entries|
|Accounts User|View DCs for billing linkage|
|Viewer|Read-only access|

---

## Integration Points

| Module               | How DC Connects                                                  |
| -------------------- | ---------------------------------------------------------------- |
| Orders               | DC is created from an Order; carries `order_id` and style number |
| Stock Management     | Stock is reduced on dispatch; increased on return                |
| PO & Bill Management | DC quantity used for billing reconciliation                      |
| Approval Status      | DC submitted for approval appears in the central queue           |
| Supplier Management  | Recipient / supplier details pulled from supplier master         |