# DC Management — Return Delivery Note

## What is a Return Delivery Note?

A Return Delivery Note (RDN) is a special type of Delivery Challan raised when fabric needs to be **sent back to the supplier** instead of being dispatched outward for processing. It is identical in structure to a standard DC but carries the `(R)` suffix in its number and is titled **RETURN DELIVERY NOTE** on the printed document.

---

## How to Identify a Return DC

|Indicator|Standard DC|Return DC|
|---|---|---|
|Number format|`DC-2026-0028`|`DC-2026-0028(R)`|
|PDF title|DELIVERY CHALLAN|RETURN DELIVERY NOTE|
|Purpose|Fabric sent out for processing|Fabric returned to supplier|

---

## When is a Return DC Raised?

|Scenario|Description|
|---|---|
|Quality rejection|Fabric received from supplier is defective and must be returned|
|Wrong specification|Fabric colour, GSM, or count does not match the order requirement|
|Excess quantity|More fabric was delivered than required; surplus is returned|
|Processing failure|Fabric sent for knitting/dyeing comes back with defects; returned again|

---

## Return DC — PDF Document

### Document Header

```
┌──────────────────────────────────────────────────────────────┐
│  No. : DC-2026-0028(R)    RETURN DELIVERY NOTE   Date: 05/05/26 │
├──────────────────────────────────────────────────────────────┤
│  [LEO Logo]        LEO Fashions                              │
│                    576/2B, Ayyar Thottam, Rayarpalayam,      │
│                    Tirupur Main Road, Palladam - 641 664.    │
│                    GST NO: 33AAEFE5039K1ZH                   │
│                    Mob.: 8668084013                          │
├──────────────────────────────────────────────────────────────┤
│  To                        Order No. : LEO-2026-031          │
│  M/s. Harish               Style No. : 1234                  │
│  3/13 A east car street                                      │
│  Thoothukudi - 628907                                        │
│  Ph: 6374777961                                              │
│  GSTIN: 22AAAAA1234W1W2                                      │
└──────────────────────────────────────────────────────────────┘
```

### Fabric Details Table

```
┌──────────────────────┬──────────┬─────────┬─────────┬──────────┬───────────────┐
│   FABRIC DETAILS     │ LAB CARD │ LOT NO. │ FIN DIA │ BAGS/    │    Weight     │
│                      │   No.    │         │         │ ROLLS    │  Kilo │ Gram  │
├──────────────────────┼──────────┼─────────┼─────────┼──────────┼───────┼───────┤
│ Colour: Single       │          │         │         │          │  20   │       │
│ Jersey-Blue-Bottom   │          │         │         │          │       │       │
│ TCX colour: 11-0103  │          │         │         │          │       │       │
│ 10s, 100% cotton     │          │         │         │          │       │       │
│ Combed VL, 100 Kg    │          │         │         │          │       │       │
└──────────────────────┴──────────┴─────────┴─────────┴──────────┴───────┴───────┘
  Gross Total: 20 Kg
```

### Remarks Section

Free-text field for notes about the reason for return or condition of the fabric.

```
Remarks: [Free text — e.g., "Fabric rejected due to colour mismatch"]
```

### Process Section

Knitting / fabric technical specifications recorded for traceability:

|Field|Example Value|
|---|---|
|Knitting Gauge|4646|
|Loop Length|7676|
|Knitting Dia|76|
|Needle Drop|NO|

### Footer

```
┌─────────────────────────────────────────────────────┐
│  Receiver's Signature       For LEO Fashions         │
│                             Created by  : admin       │
│                             Approved by : Admin       │
│       *Digitally created — Requires no signature     │
└─────────────────────────────────────────────────────┘
```

---

## Return DC — All Fields Reference

### Recipient (To) Section

|Field|Description|Example|
|---|---|---|
|Name|Supplier / recipient name|M/s. Harish|
|Address|Full delivery address|3/13 A east car street, Thoothukudi - 628907|
|Phone|Contact number|6374777961|
|GSTIN|Recipient GST number|22AAAAA1234W1W2|
|Order No.|Linked production order|LEO-2026-031|
|Style No.|Garment style reference|1234|

### Fabric Details Section

|Field|Description|
|---|---|
|Fabric Details|Colour name, TCX code, yarn count, cotton type, original weight|
|Lab Card No.|Reference to the lab test card for this fabric batch|
|Lot No.|Supplier batch / lot identifier|
|Fin Dia|Finished diameter of the knitted fabric|
|Bags / Rolls|Physical count of bags or rolls being returned|
|Weight (Kilo)|Weight in kilograms|
|Weight (Gram)|Weight in grams (for precision)|
|Gross Total|Total return weight across all fabric entries|
|Remarks|Reason for return or any additional notes|

### Process Details Section

|Field|Description|
|---|---|
|Knitting Gauge|The gauge setting used during knitting|
|Loop Length|Loop length specification|
|Knitting Dia|Knitting diameter setting|
|Needle Drop|Whether needle drop was applied (Yes / No)|

---

## Return DC Status Flow

```
Admin raises Return DC
        │
        ▼
  DC created with (R) suffix
  Status: Partial
        │
        ▼
  Submit for Approval
        │
        ▼
  Approval Status queue
        │
   ┌────┴────┐
   ▼         ▼
Approved   Rejected
   │
   ▼
  Fabric physically returned to supplier
  Stock updated (quantity added back)
        │
        ▼
  DC Status → Closed
  (when all fabric in the return is accounted for)
```

---

## Return DC vs Standard DC — Side by Side

|Attribute|Standard DC|Return DC|
|---|---|---|
|Number|`DC-2026-0028`|`DC-2026-0028(R)`|
|PDF Title|DELIVERY CHALLAN|RETURN DELIVERY NOTE|
|Direction|LEO → Processing unit / vendor|Processing unit / vendor → LEO (or supplier)|
|Stock Effect|Stock reduced (fabric goes out)|Stock increased (fabric comes back)|
|Trigger|Fabric dispatched for processing|Fabric rejected, excess, or wrong spec|
|Billing Impact|Can be billed against|Reduces billed quantity|
|Linked Order|Yes — carries order number|Yes — same order the fabric was for|
|Approval Required|Yes|Yes|
|Receiver Signs|Recipient signs on receipt|Supplier signs on receiving return|

---

## Stock Impact of a Return DC

When a Return DC is approved and closed:

```
Before Return:
  Stock — Jersey-Blue-Bottom: 80 Kg remaining

Return DC raised: 20 Kg

After Return Closed:
  Stock — Jersey-Blue-Bottom: 100 Kg
  (20 Kg added back to available stock)
```

The stock adjustment is handled by the **Stock Management** module, triggered by the DC status moving to `Closed`.

---

## Approval & Audit

Every Return DC goes through the same approval workflow as a standard DC:

- Created by a named user (`Created by: admin`)
- Approved by an authorised approver (`Approved by: Admin`)
- Digitally signed — no physical signature required on the document itself
- Full audit trail maintained in the **Audits** module