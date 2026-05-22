# Weekly Wages — Flow

**Module:** Weekly Wages **System:** LEO Fashions ERP **Scope:** End-to-end user workflow, page navigation, and state transitions

---

## End-to-End User Flow

The complete Weekly Wages workflow — from opening the module to downloading the final PDF — follows five sequential steps.

```
STEP 1          STEP 2            STEP 3           STEP 4          STEP 5
Open Module  →  Select Week   →   Find Order   →   Enter Wages  →  Print PDF
(Sidebar)       (Date Filter)     (Search/List)    (Per Panel)     (Report)
```

---

## Step-by-Step Walkthrough

### Step 1 — Open the Module

The user clicks **Weekly Wages** in the left sidebar. The module opens to the list view, defaulting to the current week's date range if previously set, or an empty filter if opening for the first time.

**Entry state:** List view with date range controls visible at the top.

---

### Step 2 — Select the Wage Week

The user sets the **From Date** and **To Date** to define the payroll week they want to view or enter wages for.

|Action|Result|
|---|---|
|Set From Date to `15 May 2026`|Filter activates|
|Set To Date to `21 May 2026`|List updates to show orders modified in that range|
|Label confirms|_Orders modified: 15 May 2026 – 21 May 2026_|
|Total Orders card|Updates to reflect the count of matching orders|

**Exit state:** Date range active; order list filtered and visible.

---

### Step 3 — Find the Order

The user locates the relevant order from the list. They can scroll, or use the search bar to find a specific order by number or name.

|Action|Result|
|---|---|
|Search `LEO-2026-008`|List filters to show only that order|
|No search|All orders for the selected week are visible|
|Read card|Order number, name, style, panel count, and panel badges visible|

**Exit state:** Target order card is visible on screen.

---

### Step 4 — Enter Wages

The user clicks the order card (_Click to view weekly wages_). This opens the wage detail view for that order.

Inside the detail view:

|Action|Result|
|---|---|
|Review order header|Confirms Order No., Name, Style No., Total Panels|
|Identify panel|Each panel (e.g., `j`, `hm`) has its own wage table|
|Enter daily amounts|User types the wage amount for each Department × Day cell|
|Day Total auto-updates|Column totals calculate instantly as values are entered|
|Row Total auto-updates|Row totals calculate instantly as values are entered|
|Repeat for each panel|All panels must be filled independently|

**Exit state:** All wage amounts entered; Grand Total visible and accurate.

---

### Step 5 — Print the Wage Report

The user clicks the **Print** button (top-right of the list view or detail view). The system generates a PDF wage report for the selected order and date range.

|Action|Result|
|---|---|
|Click Print|PDF generation triggers|
|Download prompt|Browser downloads the file|
|Filename auto-generated|e.g., `WeeklyWages_LEO-2026-008_15May-21May_10-50-37AM.pdf`|
|Footer stamped|`* Digitally generated — Generated on 21 May 2026`|

**Exit state:** PDF downloaded; wage reporting complete for the week.

---

## Page Navigation Map

```
Left Sidebar
    └── Weekly Wages
            │
            ▼
    ┌──────────────────────────────────────┐
    │         LIST VIEW                    │
    │  [From Date]  [To Date]  [Search]    │
    │  Total Orders: 1 | Current Page: 1   │
    │                                      │
    │  ┌────────────────────────────────┐  │
    │  │  LEO-2026-008    ₹             │  │
    │  │  name            Style: M      │  │
    │  │  Panels: 2       [j]  [hm]     │  │
    │  │  Click to view weekly wages    │  │
    │  └────────────────────────────────┘  │
    │                         [Print ▾]    │
    └──────────────────────────────────────┘
            │
            │  (Click order card)
            ▼
    ┌──────────────────────────────────────┐
    │         DETAIL VIEW                  │
    │  ← Back                    [🔔 2]   │
    │                                      │
    │  Order No: LEO-2026-008              │
    │  Order Name: name                    │
    │  Style No: M  |  Total Panels: 2     │
    │                                      │
    │  Panel: j                            │
    │  ┌──────┬───┬───┬───┬───┬───┬───┬──┐│
    │  │Dept  │Fr │Sa │Su │Mo │Tu │We │Th ││
    │  │Cutting│–  │–  │–  │–  │–  │–  │– ││
    │  │Feeding│–  │–  │–  │–  │–  │–  │– ││
    │  │Prod. │–  │–  │–  │–  │–  │–  │– ││
    │  │Check.│–  │–  │–  │–  │–  │–  │– ││
    │  │Finish│–  │–  │–  │–  │–  │–  │– ││
    │  │Total │–  │–  │–  │–  │–  │–  │– ││
    │  └──────┴───┴───┴───┴───┴───┴───┴──┘│
    │                                      │
    │  Panel: hm                           │
    │  [same grid structure]               │
    │                                      │
    │  Grand Total (All Panels)  Rs. –     │
    └──────────────────────────────────────┘
            │
            │  (Click Print)
            ▼
    ┌──────────────────────────────────────┐
    │         PDF WAGE REPORT              │
    │  WeeklyWages_LEO-2026-008_           │
    │  15May-21May_10-50-37AM.pdf          │
    └──────────────────────────────────────┘
```

---

## State Transitions

|State|Trigger|Next State|
|---|---|---|
|Module opens|Sidebar click|List view (empty or last-used filter)|
|Date range set|Both dates selected|List view filtered by date range|
|Search active|Text entered in search|List filtered by search + date range|
|Order card clicked|User taps _Click to view weekly wages_|Wage detail view for that order|
|Wage amount entered|User types in a cell|Row total and Day Total auto-recalculate|
|Print clicked|User clicks Print button|PDF generated and downloaded|
|Back clicked|User clicks ← arrow|Returns to list view|
|Sidebar module clicked|User navigates elsewhere|Exits Weekly Wages entirely|

---

## Approval Sub-Flow (when applicable)

When wages for an order week are complete, a Manager or Admin may submit the wage record for approval before payroll is processed.

```
Wage Entry Complete
        │
        ▼
Submit for Approval
        │
        ▼
Appears in Approval Status queue
(count badge increments in sidebar)
        │
        ├── Approved ──→ wage record marked Approved
        │                Payroll can proceed
        │
        └── Rejected ──→ wage record returned
                         User reviews and resubmits
```

---

## Navigation Controls Reference

|Control|Location|Action|
|---|---|---|
|**Weekly Wages** (sidebar)|Left navigation|Opens the module list view|
|**← Back arrow**|Top-left of detail view|Returns to the list view|
|**Print ▾**|Top-right of list view|Opens print/download for current selection|
|**🔔 Notification badge**|Top-right of detail view|Opens notification panel (ERP-wide)|
|**🏠 Home icon**|Top-right of detail view|Returns to the ERP dashboard|
|**Sidebar module links**|Left navigation|Navigate to any other ERP module|

---

## Summary

The Weekly Wages module follows a linear, five-step workflow: open → filter → find → enter → print. Every step maps to a distinct UI state with clear entry and exit conditions. The module is designed for weekly use by supervisors or managers responsible for payroll data, and produces a digitally stamped PDF that serves as the final wage record for each order week.