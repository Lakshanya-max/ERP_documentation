# Weekly Wages — Overview

**Module:** Weekly Wages **System:** LEO Fashions ERP **Scope:** Functional documentation — UI, fields, and behaviour

---

## Purpose

The Weekly Wages module captures, tracks, and reports daily production wages for every active garment order in LEO Fashions ERP. Wages are recorded per department, per panel, and per working day across a Friday-to-Thursday payroll week. At the end of each week, the module produces a digitally generated PDF wage report used internally for payroll processing and factory-floor accountability.

---

## Module Entry Point

The module is accessed via **Weekly Wages** in the left sidebar of the ERP. It is available to all roles with wage access and displays a filtered list of orders based on the selected date range.

---

## Core Concepts

### Wage Week

The payroll cycle in LEO Fashions runs **Friday to Thursday** — seven calendar days. Every wage table in the module is structured around this fixed seven-day window. Users select the week using the From Date and To Date filters before entering or reviewing wage data.

### Panel

Each garment order is divided into one or more **panels**. A panel represents a distinct production grouping within an order — for example, a different fabric type, garment part, or buyer specification. Wages are entered independently for each panel. An order with two panels (e.g., `j` and `hm`) will contain two separate wage grids.

### Department

Within each panel, wages are broken down by **production department**. The five departments are:

|Department|Role|
|---|---|
|Cutting|Workers performing fabric cutting operations|
|Feeding|Workers feeding fabric and components to sewing machines|
|Production|Core sewing and garment assembly workforce|
|Checking|Quality control and inspection staff|
|Finishing|Workers handling ironing, tagging, folding, and packing|

Each department has its own row in the wage grid, and wages are entered for each working day individually.

---

## Module Structure

```
Weekly Wages Module
    ├── 1. Order Discovery & Filtering
    │       ├── 1.1 Date Range Filter
    │       ├── 1.2 Order Search
    │       └── 1.3 Order Count Summary
    │
    ├── 2. Order Card (List View)
    │       ├── 2.1 Order Identifier
    │       ├── 2.2 Style & Name Display
    │       └── 2.3 Panel Summary Badges
    │
    ├── 3. Wage Entry (Detail View)
    │       ├── 3.1 Order Header Info
    │       ├── 3.2 Panel Selector
    │       └── 3.3 Department × Day Grid
    │               ├── 3.3.1 Cutting
    │               ├── 3.3.2 Feeding
    │               ├── 3.3.3 Production
    │               ├── 3.3.4 Checking
    │               └── 3.3.5 Finishing
    │
    ├── 4. Totals & Aggregation
    │       ├── 4.1 Row Total (per Department)
    │       ├── 4.2 Day Total (per Panel per Day)
    │       ├── 4.3 Panel Total
    │       └── 4.4 Grand Total (All Panels)
    │
    ├── 5. Wage Report (Print / PDF)
    │       ├── 5.1 Report Header
    │       ├── 5.2 Per-Panel Wage Table
    │       └── 5.3 Report Footer
    │
    └── 6. Actions & Navigation
            ├── 6.1 Print / Download
            ├── 6.2 Back Navigation
            └── 6.3 Notifications
```

---

## Key Entities

```
Weekly Wages
    └── Order (e.g., LEO-2026-008)
            ├── Date Range  (Fri 15 May → Thu 21 May)
            └── Panel(s)    (e.g., j, hm)
                    └── Department Rows
                            ├── Cutting
                            ├── Feeding
                            ├── Production
                            ├── Checking
                            └── Finishing
                                    └── Day Columns (Fri → Thu)
                                            └── Wage Amount (Rs.)
```

---

## Field Reference — List View

### Date Range Filter

|Field|Description|
|---|---|
|From Date|Start of the wage week (e.g., 15 May 2026)|
|To Date|End of the wage week (e.g., 21 May 2026)|
|Clear (×)|Clears the individual date field, widening the scope|
|Active label|Confirms the selected range: _Orders modified: 15 May 2026 – 21 May 2026_|

### Order Search

|Field|Description|
|---|---|
|Input|Free-text; matches on order number or order name|
|Scope|Operates within the currently active date range|

### Order Count Summary

|Card|Description|
|---|---|
|Total Orders|Count of all orders matching the current filter|
|Current Page|Count of orders rendered on the visible page|

---

## Field Reference — Order Card

|Field|Description|
|---|---|
|Order Number|Unique system identifier (e.g., `LEO-2026-008`)|
|Currency Badge (₹)|Indicates wage data is associated with this order|
|Order Name|Descriptive label for the order|
|Style No.|Short style code badge (e.g., `M`)|
|Panels Count|Number of panels defined on the order (e.g., `2`)|
|Panel Badges|One pill per panel showing its code (e.g., `j`, `hm`)|
|Click to View|Navigates into the wage detail view for this order|

---

## Field Reference — Wage Entry Detail

### Order Header

|Field|Description|
|---|---|
|Order No.|e.g., `LEO-2026-008`|
|Order Name|e.g., _name_|
|Style No.|e.g., `M`|
|Total Panels|Total panel count for the order (e.g., `2`)|

### Department × Day Grid

|Column|Description|
|---|---|
|Department|Row label: Cutting, Feeding, Production, Checking, Finishing|
|Fri [DD] – Thu [DD]|Wage amount for each day of the wage week|
|Total|Auto-calculated row total across all 7 days|
|Day Total (row)|Auto-calculated column total for all departments on that day|

---

## Totals Logic

|Total|Formula|
|---|---|
|Row Total|`Fri + Sat + Sun + Mon + Tue + Wed + Thu` (per department, per panel)|
|Day Total|`Cutting + Feeding + Production + Checking + Finishing` (per day, per panel)|
|Grand Total|Sum of all Day Totals across all panels|

All totals are computed automatically. No manual entry is required or permitted in total fields.

---

## Empty State Behaviour

When no wage amounts have been entered for an order week, the module and its generated PDF still display the full grid structure. Every cell renders as `–` (dash). The Grand Total displays as `Rs. –`. This confirms the report was generated even when no wage data has been recorded for that period.

---

## Related Modules

| Module          | Relationship                                                                                         |
| --------------- | ---------------------------------------------------------------------------------------------------- |
| Orders          | Weekly Wages are always scoped to a specific order — order, style, and panel data are read from here |
| Profit & Loss   | Grand Total wage amounts feed into the order's labour cost computation                               |
| Approval Status | Wage reports may be routed for management approval before payroll is processed                       |
| Users           | Role-based access to wage entry, report viewing, and print actions is managed here                   |
| Audits          | All changes to wage records are logged for traceability                                              |