# Supplier Management — Bills

## Supplier Bills

Every supplier has a **Bills tab** inside their detail screen. This tracks all invoices raised by that supplier to LEO Fashions — for materials supplied or work done.

---

## Bills Tab Summary

At the top of the Bills tab:

|Summary Field|Example|
|---|---|
|Total Bills|2|
|Total Quantity|90|
|Total Amount|₹1,090|

---

## Individual Bill Entry

Each bill shows:

|Field|Description|Example|
|---|---|---|
|Bill Number|Auto-generated|SUPBILL-0001|
|Description|What the bill is for|"Test Bill"|
|Quantity|Items/Kg in bill|10|
|Amount|Bill value ₹|₹1,000|
|Bill Date|When bill was raised|03 Jan 2026|
|Bill Photo|Uploaded invoice scan|View / Not attached|
|Created On|When entered in system|03 Jan 2026, 7:24 PM|

---

## Real Examples from System

**SUP-000015 Bills:**

```
Bill 1:
├── SUPBILL-0001
├── Description  → Test Bill
├── Quantity     → 10
├── Amount       → ₹1,000
├── Bill Date    → 03 Jan 2026
└── Bill Photo   → View (attached)

Bill 2:
├── SUPBILL-0002
├── Description  → ok
├── Quantity     → 80
├── Amount       → ₹90
├── Bill Date    → 09 Jan 2026
└── Bill Photo   → Not attached

Summary:
Total Bills   = 2
Total Qty     = 90
Total Amount  = ₹1,090
```

---

## Bill Number Format

```
SUPBILL-0001
SUPBILL-0002
SUPBILL-0003
(auto-incremented per supplier)
```

---

## How Bills Are Added

```
Admin opens Supplier Detail
        ↓
Clicks Bills tab
        ↓
Clicks + Add Bill
        ↓
Fills bill form:
├── Description
├── Quantity
├── Amount
├── Bill Date
└── Bill Photo (optional)
        ↓
Bill saved
        ↓
Summary totals auto-updated
```