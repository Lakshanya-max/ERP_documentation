# PO & Bill Management — Bills

## What Are PO Bills?

When a supplier delivers raw materials and raises an invoice, that invoice is recorded as a **PO Bill** inside the Purchase Order. This tracks how much is owed to each supplier for materials purchased.

---

## Bills Tab Summary

At the top of the Bills tab:

|Summary Field|Description|
|---|---|
|Total Bills|Count of all bills raised|
|Total Quantity|Combined qty across all bills|
|Total Amount|Total payable ₹|

---

## Individual Bill Entry

|Field|Description|Example|
|---|---|---|
|Bill Number|Auto-generated|SUPBILL-0001|
|Description|What the bill covers|"Yarn delivery batch 1"|
|Quantity|Material qty in this bill|500 Kg|
|Amount|Bill value ₹|₹5,000|
|GST %|Tax percentage|5%|
|Total Amount|Amount + GST|₹5,250|
|Bill Date|When bill was raised|03 Jan 2026|
|Bill Photo|Uploaded invoice scan|View / Not attached|
|Payment Status|Current payment state|Open / Partial / Paid|
|Created On|When entered in system|03 Jan 2026, 7:24 PM|

---

## Payment Status Flow

```
Bill raised by supplier
        ↓
Bill added → Payment Status = Open
        ↓
Partial payment made
        ↓
Payment Status = Partial
        ↓
Full payment made
        ↓
Payment Status = Paid
```

---

## How Bills Are Added

```
Admin opens PO Detail
        ↓
Clicks Bills tab
        ↓
Clicks + Add Bill
        ↓
Fills bill form:
├── Description
├── Quantity
├── Amount ₹
├── GST %
├── Bill Date
└── Bill Photo (optional)
        ↓
System calculates Total = Amount + GST
        ↓
Bill saved with Payment Status = Open
        ↓
Summary totals auto-updated
```

---

## PO Bills vs Supplier Bills — Difference

||PO Bills|Supplier Bills|
|---|---|---|
|Where|Inside a PO record|Inside Supplier record|
|For what|Specific material delivery|Any supplier transaction|
|Linked to|Purchase Order|Supplier profile|
|Access|PO & Bill Management module|Supplier Management module|