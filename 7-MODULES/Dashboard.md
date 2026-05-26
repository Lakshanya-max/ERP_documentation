## Overview

The Dashboard is the **first screen** the admin sees after login. It provides a real-time snapshot of the entire operation — active orders, approvals, POs, DCs, wages, and a monthly spend chart — all in one place.

---

## Dashboard Layout

```
┌─────────────────────────────────────────────────────────────────┐
│  ← (back)           Dashboard               [download] [home]   │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────────┐  ┌──────────────────┐  ┌───────────────┐  │
│  │ In Progress       │  │ Completed         │  │ Tasks         │  │
│  │ Orders      115  │  │ Orders       28  │  │            2  │  │
│  └──────────────────┘  └──────────────────┘  └───────────────┘  │
│                                                                  │
│  ┌──────────────────┐  ┌──────────────────┐  ┌───────────────┐  │
│  │ Pending           │  │ Pending           │  │ Completed     │  │
│  │ Approvals    31  │  │ PO           40  │  │ PO       20   │  │
│  └──────────────────┘  └──────────────────┘  └───────────────┘  │
│                                                                  │
│  ┌──────────────────┐  ┌──────────────────┐  ┌───────────────┐  │
│  │ Pending           │  │ Completed         │  │ This Week     │  │
│  │ DC           34  │  │ DC            4  │  │ Wages     ₹0  │  │
│  └──────────────────┘  └──────────────────┘  └───────────────┘  │
│                                                                  │
├─────────────────────────────────────────────────────────────────┤
│  Monthly CMT Spend Estimate                                      │
│  From: [February 2026]  To: [Jan 2027]   Capacity: ₹26,000     │
│                                                                  │
│  [Bar Chart — Blue: CMT Spend, Green: Order Value per month]    │
│  Feb–Jun 2026 show bars, Jul–Jan 2027 are empty (future)        │
│  Red horizontal line = Capacity limit (₹26,000)                 │
│  "Click on a bar to view order details"                         │
├─────────────────────────────────────────────────────────────────┤
│  Order Overview                          [Search] [Close All]   │
│                                                                  │
│  ▼ #LEO-2026-012  testerror  Style: 1234  [BULK] [IN PROGRESS] │
│    Qty: 150  Cut: 150  📅 20-01-2026                            │
│    ┌── Yarn ──────────────────────────────────────────────┐     │
│    │ Color                    Required    Received         │     │
│    │ 1.TCX-11-0103 FLEECE[10s]   120          0           │     │
│    └──────────────────────────────────────────────────────┘     │
│    ┌── Store / Trims ─────────────────────────────────────┐     │
│    │ Trim Type         Required    Received                │     │
│    │ Main Label           200          0                   │     │
│    │ Main Tag             200          0                   │     │
│    └──────────────────────────────────────────────────────┘     │
│                                                                  │
│  ▼ #LEO-2026-035  hoodie  Style: Full Sleeve  [BULK][IN PROGRESS]│
│    Qty: 1000  Cut: 1000  📅 16-05-2026  🏭 25-05-2026           │
│                                                                  │
│  ▼ #LEO-2026-036  nn  Style: ejr  [BULK][IN PROGRESS]          │
│    Qty: 3  Cut: 3  📅 19-05-2026  🏭 19-05-2026                 │
│                                                                  │
│  ▼ #LEO-2026-008  name  Style: M  [BULK][IN PROGRESS]          │
│    Qty: 100  Cut: 100  📅 13-01-2026                            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Section 1 — Summary Stat Cards (Top Grid)

Nine cards arranged in a 3×3 grid give the admin an instant count of everything active.

### Row 1 — Orders

|Card|Icon Color|Value Shown|What It Counts|
|---|---|---|---|
|**In Progress Orders**|Orange (spinner)|115|Orders currently in production|
|**Completed Orders**|Green (tick)|28|Orders fully finished|
|**Tasks**|Dark (clipboard)|2|Open tasks pending action|

### Row 2 — Procurement & Approvals

|Card|Icon Color|Value Shown|What It Counts|
|---|---|---|---|
|**Pending Approvals**|Red (clipboard tick)|31|Bills, wages, advances awaiting admin approval|
|**Pending PO**|Orange (box)|40|Purchase orders not yet received/closed|
|**Completed PO**|Green (box crossed)|20|Purchase orders fully settled|

### Row 3 — Delivery & Wages

|Card|Icon Color|Value Shown|What It Counts|
|---|---|---|---|
|**Pending DC**|Orange (truck)|34|Delivery challans not yet delivered|
|**Completed DC**|Green (truck)|4|Delivery challans marked as delivered|
|**This Week Wages**|Blue (rupee ₹)|₹0|Total wages payable for the current week|

### Card Behaviour

- Each card is **clickable** — tapping it navigates to the relevant module filtered to that status
- Numbers update in real time as records change
- **Pending Approvals** card shows a red badge (notification bubble with count) at top-right

---

## Section 2 — Monthly CMT Spend Estimate (Bar Chart)

### What Is CMT?

CMT stands for **Cut, Make & Trim** — the core production cost paid to workers and contractors per garment.

### Chart Controls

|Control|Description|
|---|---|
|**From**|Start month of the date range (e.g. February 2026)|
|**To**|End month of the date range (e.g. Jan 2027)|
|**Capacity**|A fixed monthly CMT budget limit, shown as a red horizontal line (e.g. ₹26,000)|

### Chart Data

|Bar Color|Represents|
|---|---|
|🔵 Blue|Actual CMT spend for the month (wages + task costs)|
|🟢 Green|Total order value for the month (revenue)|
|🔴 Red line|Monthly capacity limit|

### Chart Behaviour

- Months with completed/in-progress orders show bars; future months are empty
- **Clicking a bar** opens a detail view of all orders in that month
- Y-axis left: rupee amounts (₹0 to ₹30L+)
- Y-axis right: piece count (0 to 6,000)
- X-axis: months from selected date range

### What It Tells the Admin

- Is the factory operating above or below capacity?
- Which months had high spend vs high revenue?
- Seasonality patterns — busiest and slowest months

---

## Section 3 — Order Overview (Expandable List)

Below the chart, the dashboard shows **all active orders** in a live accordion list.

### Controls

|Control|Function|
|---|---|
|🔍 Search|Filter orders by order number, name, or style|
|✕ Close All|Collapses all expanded order cards|

### Order Card — Collapsed View

Each order shows as a single row:

```
#LEO-2026-035   hoodie   Style: Full Sleeve   [BULK]  [IN PROGRESS]
Qty: 1000   Cut: 1000   📅 16-05-2026   🏭 25-05-2026
```

|Field|Meaning|
|---|---|
|`#LEO-2026-035`|Unique order number (auto-generated)|
|`hoodie`|Customer or order name|
|`Style: Full Sleeve`|Garment style / product type|
|`[BULK]`|Order type tag — Bulk production|
|`[IN PROGRESS]`|Current order status badge|
|`Qty: 1000`|Total pieces ordered|
|`Cut: 1000`|Pieces cut so far|
|📅 `16-05-2026`|Cut date / order date|
|🏭 `25-05-2026`|Expected delivery / completion date|

### Order Card — Expanded View

Clicking the ∨ arrow expands the card to show **material requirements**:

#### Yarn Section

Shows all yarn/fabric requirements for this order:

|Column|Meaning|
|---|---|
|Color|Yarn code and description (e.g. `1.TCX-11-0103 FLEECE [10s]`)|
|Required|Total quantity needed for the order|
|Received|Quantity received from supplier so far|

#### Store / Trims Section

Shows all trim/accessory requirements:

|Column|Meaning|
|---|---|
|Trim Type|Name of the trim (e.g. Main Label, Main Tag, Button)|
|Required|Total quantity needed|
|Received|Quantity received so far|

### Visual Status at a Glance

- If **Received = 0** while **Required > 0** → materials not yet sourced (flag for admin)
- If **Received = Required** → fully stocked for this order
- This lets admin see material readiness for every in-progress order without going into each order

---

## Navigation from Dashboard

|Click Target|Goes To|
|---|---|
|In Progress Orders card|Orders list → filtered to `in_progress`|
|Completed Orders card|Orders list → filtered to `completed`|
|Tasks card|Tasks list → filtered to open tasks|
|Pending Approvals card|Approval Queue|
|Pending PO card|PO list → filtered to pending|
|Completed PO card|PO list → filtered to completed|
|Pending DC card|DC list → filtered to pending|
|Completed DC card|DC list → filtered to delivered|
|This Week Wages card|Weekly Wages → current week|
|Chart bar|Orders list → filtered to that month|
|Order number in Order Overview|Order detail page|

---

## Top Navigation Icons

|Icon|Function|
|---|---|
|← (back arrow)|Navigate to previous screen|
|Download icon|Export current dashboard data|
|🏠 Home icon|Return to dashboard from any screen|
|🔴 Badge on Approvals|Live count of pending approvals|

---

## Data Refresh

- Stat cards update **on page load** and reflect live database counts
- The chart updates when the date range is changed
- The Order Overview list reflects all currently active orders in real time

---

## Related Documents

- Orders Overview
- Approval Overview
- PO Overview
- DC Overview
- Weekly Wages
- Profit & Loss