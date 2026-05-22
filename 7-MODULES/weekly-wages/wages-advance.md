# Weekly Wages — Advanced Reference

**Module:** Weekly Wages **System:** LEO Fashions ERP **Scope:** PDF generation, permissions, integrations, and edge-case behaviour

---

## PDF Generation

### Overview

The Weekly Wages module generates a single-page, print-ready PDF report for a selected order and date range. The PDF is produced on demand when the user clicks **Print** and is stamped with the date and time of generation. It is digitally generated and requires no physical signature.

---

### Trigger & Output

|Property|Description|
|---|---|
|Trigger|User clicks the **Print** button on the list view or detail view|
|Scope|One PDF per order per selected date range|
|Output filename|`WeeklyWages_{OrderNo}_{FromDate}-{ToDate}_{Timestamp}.pdf`|
|Example filename|`WeeklyWages_LEO-2026-008_15May-21May_10-50-37AM.pdf`|

**Filename segment breakdown:**

|Segment|Description|Example|
|---|---|---|
|`WeeklyWages`|Static prefix|`WeeklyWages`|
|`{OrderNo}`|Order number|`LEO-2026-008`|
|`{FromDate}`|From date, no spaces|`15May`|
|`{ToDate}`|To date, no spaces|`21May`|
|`{Timestamp}`|Time of generation (HH-MM-SSam/pm)|`10-50-37AM`|

---

### Document Layout

```
┌─────────────────────────────────────────────────────────┐
│  SECTION 1 — Document Header                            │
│  Order No. (left) | WEEKLY WAGES REPORT (centre)        │
│  Date Range (right)                                     │
├─────────────────────────────────────────────────────────┤
│  SECTION 2 — Company Block                              │
│  Logo (left) | Company Name, Address, GST, Mobile       │
├─────────────────────────────────────────────────────────┤
│  SECTION 3 — Order Info Block                           │
│  Order No. | Order Name | Style No. | Total Panels      │
├─────────────────────────────────────────────────────────┤
│  SECTION 4 — Panel Table(s)                             │
│  Panel: [code]                                          │
│  ┌──────────────┬────┬────┬────┬────┬────┬────┬────┬───┐│
│  │ Department   │Fri │Sat │Sun │Mon │Tue │Wed │Thu │Tot││
│  │ Cutting      │ –  │ –  │ –  │ –  │ –  │ –  │ –  │ – ││
│  │ Feeding      │ –  │ –  │ –  │ –  │ –  │ –  │ –  │ – ││
│  │ Production   │ –  │ –  │ –  │ –  │ –  │ –  │ –  │ – ││
│  │ Checking     │ –  │ –  │ –  │ –  │ –  │ –  │ –  │ – ││
│  │ Finishing    │ –  │ –  │ –  │ –  │ –  │ –  │ –  │ – ││
│  │ Day Total    │ –  │ –  │ –  │ –  │ –  │ –  │ –  │ – ││
│  └──────────────┴────┴────┴────┴────┴────┴────┴────┴───┘│
│  (Repeated for each panel)                              │
├─────────────────────────────────────────────────────────┤
│  SECTION 5 — Grand Total Bar                            │
│  Grand Total (All Panels)              Rs. [amount]     │
├─────────────────────────────────────────────────────────┤
│  SECTION 6 — Footer                                     │
│  * Digitally generated — Generated on [date]            │
└─────────────────────────────────────────────────────────┘
```

---

### Section-by-Section Field Reference

#### Section 1 — Document Header

|Field|Source|Example|
|---|---|---|
|Order Number|Order record|`LEO-2026-008`|
|Report Title|Static label|`WEEKLY WAGES REPORT`|
|Date Range|Date range filter|`15/05/26 – 21/05/26`|

Header spans the full page width. Order number is top-left, title is centred, date range is top-right.

---

#### Section 2 — Company Block

|Field|Source|Example|
|---|---|---|
|Company Logo|Static asset|LEO Fashions logo|
|Company Name|Static|`LEO Fashions`|
|Address|Static|`576/2B, Ayyar Thottam, Rayarpalayam, Tirupur Main Road, Palladam – 641 664`|
|GST Number|Static|`33AAEFE5039K1ZH`|
|Mobile|Static|`8668084013`|

---

#### Section 3 — Order Info Block

|Field|Source|Example|
|---|---|---|
|Order No.|Order record|`LEO-2026-008`|
|Order Name|Order record|`name`|
|Style No.|Order record|`M`|
|Total Panels|Panel count on the order|`2`|

---

#### Section 4 — Panel Tables

One table is printed per panel, stacked vertically. Each table carries:

|Element|Description|
|---|---|
|Panel Label|Bold heading above the table (e.g., `Panel: j`)|
|Department rows|Cutting, Feeding, Production, Checking, Finishing|
|Day columns|Fri [DD] through Thu [DD]|
|Total column|Row total per department across 7 days|
|Day Total row|Column total for all departments per day|
|Empty cells|Rendered as `–` — never left blank on the printed document|

---

#### Section 5 — Grand Total Bar

|Field|Description|
|---|---|
|Label|`Grand Total (All Panels)` — left-aligned|
|Amount|Total wages in Rs. — right-aligned (e.g., `Rs. 10,500.00`)|
|Empty state|Printed as `Rs. –` when no wages have been entered|

---

#### Section 6 — Footer

|Field|Description|
|---|---|
|Digital notice|`* Digitally generated — Generated on [date]`|
|Generation date|Actual date the PDF was produced (e.g., `21 May 2026`)|

The generation stamp is applied at the moment of PDF creation, not at the time of wage entry. Re-generating the PDF on a later date produces a different timestamp.

---

### Print Specifications

|Property|Value|
|---|---|
|Page size|A4 (210 × 297 mm)|
|Orientation|Portrait|
|Margins|Standard (~15 mm all sides)|
|Font|Sans-serif (Arial or equivalent)|
|Table borders|Single-line cell borders throughout|
|Day Total row|Bold text, visually distinguished from department rows|
|Grand Total bar|Full-width highlighted border bar|
|Signature|Not required — `* Digitally created — Requires no signature`|
|Pages|1 page per order; additional pages if panel count causes overflow|

---

## Permissions

### Role Matrix

|Action|Admin|Manager|Supervisor|Operator|
|---|---|---|---|---|
|View Weekly Wages list|✅|✅|✅|❌|
|Filter by date range|✅|✅|✅|❌|
|Search orders|✅|✅|✅|❌|
|View wage detail (read)|✅|✅|✅|❌|
|Enter / edit wage amounts|✅|✅|✅|❌|
|Print / download PDF report|✅|✅|✅|❌|
|Submit for approval|✅|✅|❌|❌|
|Approve wage record|✅|✅|❌|❌|

### Role Descriptions

|Role|Access Summary|
|---|---|
|**Admin**|Full access to all actions including approval and record management|
|**Manager**|Can enter wages, generate reports, and approve submitted records|
|**Supervisor**|Can enter wages and print reports — cannot submit or approve|
|**Operator**|No access to the Weekly Wages module|

Permission changes are managed via the **Users** module by an Admin.

---

## Integrations

### Integration Map

```
                    ┌──────────────────┐
                    │     Orders       │
                    │  (LEO-YYYY-NNN)  │
                    └────────┬─────────┘
                             │ order_id, panels, style
                             ▼
                    ┌──────────────────┐
                    │  Weekly Wages    │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
        Profit & Loss   Approval Status  Print Service
```

---

### Module-by-Module

#### Orders

Weekly Wages are always scoped to a specific order. The order number, order name, style number, and panel definitions are all read from the Orders module when the user navigates into the wage detail view. Weekly Wages does not create or modify order records.

**Data read:** `order_id`, `order_number`, `order_name`, `style_no`, `panels`

---

#### Profit & Loss

The Grand Total wage amount for an order week feeds into the P&L module as a labour cost component. P&L reads the wage totals and compares them against the order's CMT price and other cost lines. P&L does not write back to wage records.

**Data consumed:** `grand_total`, `order_id`

---

#### Approval Status

Wage reports submitted for management sign-off appear in the Approval Status queue with a count badge in the sidebar. The approver acts from the Approval Status screen; the result is written back to the wage record's `approval_status` field.

**Trigger:** Wage record submitted → appears in Approval Status queue **Write-back:** `wages.approval_status`

---

#### Print Service

When the user triggers Print, the system passes the full wage snapshot for the selected order and date range to the Print Service, which renders the formatted PDF.

**Data passed:** `order_id`, `date_range`, `panels`, `department_wages`, `grand_total`

---

### Data Flow Summary

|Event|From|To|Data|
|---|---|---|---|
|Wage view opened|Orders|Weekly Wages|`order_id`, panels, style|
|Wage entry saved|Weekly Wages|Weekly Wages (own record)|Department × day amounts|
|Grand Total computed|Weekly Wages|Profit & Loss (read)|Total wage Rs.|
|Report submitted|Weekly Wages|Approval Status|`order_id`, wage snapshot|
|Approval result|Approval Status|Weekly Wages|`approval_status`|
|Print triggered|Weekly Wages|Print Service|Full wage data snapshot|

---

## Edge Cases & Behaviour Notes

|Scenario|Behaviour|
|---|---|
|No wages entered for the week|All cells display `–`; Grand Total displays `Rs. –`; PDF still generates|
|Order has only one panel|Detail view shows a single panel table; Grand Total equals that panel's total|
|Re-generating the PDF on a later date|Generation timestamp in the footer updates to the new date; wage data remains unchanged|
|Date range cleared by user|List scope widens to show all orders regardless of modification date|
|Search with no matches|Empty list state shown; Total Orders displays `0`|