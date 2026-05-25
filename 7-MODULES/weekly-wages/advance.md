# Weekly Wages — Advance Payments

## What Is an Advance?

An advance is **salary paid to a worker before the official payday**. When a worker requests money early due to personal need, the admin records it in the system. At salary time, this advance is automatically deducted from the total wages.

---

## Why Advances Matter

|Without System|With System|
|---|---|
|Advance noted on paper, forgotten|Recorded digitally, never forgotten|
|Manual deduction calculations|Auto-deducted from final salary|
|Disputes about amount given|Clear record with date and amount|
|No audit trail|Full history maintained|

---

## Add Advance Form

|Field|Type|Required|Description|
|---|---|---|---|
|Worker Name|Text / Dropdown|✅|Who received the advance|
|Advance Amount|Number ₹|✅|How much was given|
|Advance Date|Date picker|✅|When it was given|
|Remarks|Textarea|❌|Optional notes|

---

## How Advance Is Used

```
Admin adds advance entry:
Worker: Gowri
Amount: ₹500
Date: 18 May 2026
        ↓
System stores advance record
linked to order + worker
        ↓
End of week:
Total Wages    = ₹1,200
Advance Given  = ₹500
─────────────────────────
Net Salary     = ₹700
```

---

## Advance Access

|Action|Who Can Do It|
|---|---|
|Add advance|Admin only|
|View advances|Admin only|
|See deduction in wage sheet|Admin|
|Download PDF with advance|Admin|

---

## Advance in PDF

When downloading the weekly wage PDF:

- Total wages shown
- Advance amount shown separately
- Net payable amount clearly displayed
- All panel-wise breakdown included