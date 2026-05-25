# UI Overview — LEO Fashions

## Application Structure

LEO Fashions is available on both **Web (browser)** and **Mobile (app)**. The UI is designed for two types of users — Admin and regular Users — each seeing a different set of screens based on their role.

---

## Layout Structure

### Web Layout

```
┌─────────────────────────────────────────┐
│           TOP BAR                       │
│  [Logo]  LEO Fashions    [User] [Gear]  │
├──────────────┬──────────────────────────┤
│              │                          │
│   SIDEBAR    │      MAIN CONTENT        │
│   MENU       │      AREA                │
│              │                          │
│  Dashboard   │  (List / Detail /        │
│  Orders      │   Form / Report)         │
│  Tasks       │                          │
│  Suppliers   │                          │
│  PO & Bills  │                          │
│  ...         │                          │
│              │                          │
└──────────────┴──────────────────────────┘
```

### Mobile Layout

```
┌─────────────────┐
│   TOP BAR       │
│ [←] Title [🏠]  │
├─────────────────┤
│                 │
│  MAIN CONTENT   │
│                 │
│  (scrollable)   │
│                 │
└─────────────────┘
```

---

## Navigation — Sidebar Menu (Web)

|Menu Item|Icon|Who Sees It|
|---|---|---|
|Dashboard|Clock|Admin + User|
|Orders|Shirt|Admin + User|
|Tasks|Checklist|Admin + User|
|Supplier Management|People|Admin only|
|PO & Bill Management|Document|Admin only|
|Due Payments|Rupee|Admin only|
|Stock Management|Box|Admin only|
|DC Management|Truck|Admin only|
|Profit & Loss|Chart|Admin only|
|Weekly Wages|Rupee|Admin only|
|Approval Status|Clipboard + badge|Admin only|
|Users|Person|Admin only|
|Audits|Report|Admin only|
|FAQ|Question mark|Admin + User|

---

## Common UI Patterns

### List Screen Pattern

Every module list follows this structure:

```
[Search Bar]  [Filter 1]  [Filter 2]  [Export/Print]
─────────────────────────────────────────────────────
[Card 1] → Name | ID | Status | Tags | Time
[Card 2] → ...
[Card 3] → ...
─────────────────────────────────────────────────────
[← 1  2  3  4  5 ... 12  →]  ← Pagination
                              [+ Create Button]
```

### Detail Screen Pattern

```
[← Back]    [Title]    [Action Buttons]
─────────────────────────────────────
[Status Badges]
[Summary Row: Key numbers]
─────────────────────────────────────
[Tab 1] [Tab 2] [Tab 3] [Tab 4]
─────────────────────────────────────
[Tab Content]
```

### Form Pattern

```
[← Back]    [Form Title]
─────────────────────────
Section 1 — Basic Info
  [Field]    [Field]
  [Field]    [Field]

Section 2 — Details
  [Field]    [Field]

Section 3 — Optional
  [Field]
─────────────────────────
        [Save / Submit]
```

---

## Status Badge Colors

|Color|Status|
|---|---|
|Grey pill|Draft / Pending|
|Blue pill|In Progress|
|Green pill|Completed / Approved / Verified|
|Orange pill|Open / Partial|
|Purple pill|Sample|
|Red text|SHORTAGE|

---

## Common Action Buttons

| Button             | Where            | Action           |
| ------------------ | ---------------- | ---------------- |
| `+ Order`          | Orders list      | Create new order |
| `+ Purchase Order` | PO list          | Create new PO    |
| `+ Supplier`       | Supplier list    | Add new supplier |
| `Print`            | DC / PO detail   | Print document   |
| `Export`           | Orders / PO list | Download CSV     |
| `Share`            | PO card          | Share PO         |
| `Add Advance`      | Weekly wages     | Record advance   |
| `Download PDF`     | Weekly wages     | Get wage sheet   |
| `Edit`             | Any detail       | Edit record      |