# Weekly Wages — Overview

## What Is Weekly Wages?

Weekly Wages is the module that **calculates and tracks worker salaries** automatically. Instead of using a calculator, every piece of work done by every worker is recorded in the system — and the salary is calculated automatically based on pieces made per day, per department, per panel.

---

## How Wages Are Structured

Wages in LEO Fashions are tracked at three levels:

```
ORDER
    └── PANEL (e.g. j, hm)
            └── DEPARTMENT (Cutting/Feeding/Production/Checking/Finishing)
                    └── DAY (Mon, Tue, Wed... 7 days)
                            └── PIECES × RATE = DAILY WAGE
```

---

## Wage Calculation Formula

```
Daily Wage   = Pieces Manufactured × Rate per Piece
Weekly Total = Sum of all daily wages (7 days)
Net Salary   = Weekly Total − Advance Given
```

---

## Weekly Wages List Screen

|Element|Description|
|---|---|
|From Date|Week start — e.g. 15 May 2026|
|To Date|Week end — e.g. 21 May 2026|
|Search|Filter by order|
|Total Orders|Orders with wage data in this period|
|Order Card|Shows order ID, name, style, panels|

---

## Wage Detail Screen

When you click an order card:

|Element|Description|
|---|---|
|Order ID|e.g. LEO-2026-008|
|Week Range|15 May 2026 to 21 May 2026 (7 days)|
|Panel Breakdown|One table per panel|
|Department Rows|Cutting, Feeding, Production, Checking, Finishing|
|Day Columns|Mon, Tue, Wed, Thu, Fri, Sat, Sun|
|Day Total|Sum of all dept wages for that day|
|Panel Total|Sum of all days for that panel|
|Grand Total|Sum across all panels|

---

## Available Actions

|Action|Purpose|
|---|---|
|Select Week|Change the week being viewed|
|Add Advance|Record advance payment for a worker|
|Download PDF|Export wage sheet as PDF|
|Print|Print the weekly wage report|

---

## Advance Payment

If a worker needs salary before payday:

```
Admin records advance:
├── Worker Name
├── Advance Amount ₹
├── Date given
└── Remarks

At salary time:
Net Salary = Total Wages − Advance
```

---

## Departments Tracked

|Department|What They Do|
|---|---|
|Cutting|Cut fabric into pieces|
|Feeding|Feed pieces to stitching line|
|Production|Stitch garments|
|Checking|Quality check stitched pieces|
|Finishing|Iron, fold, final touches|

---

## Key Rules

- Wages calculated per **order → panel → department → day**
- One week = always 7 days (auto calculated from + to date)
- Advance is stored and auto-deducted at salary time
- PDF can be downloaded any time for any week
- Admin can view wages for all orders
- Date filter allows checking any past or future week