# System Overview — LEO Fashions

## How All Modules Work Together

This document shows the big picture — how every module connects to every other module and how they all work as one complete system.

---

## The Complete System Map

```
┌─────────────────────────────────────────────────────┐
│                    LEO FASHIONS                     │
│              Garment Manufacturing ERP              │
└─────────────────────────────────────────────────────┘
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
   ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
   │   ORDERS    │ │  SUPPLIERS  │ │    USERS    │
   │  (Core)     │ │ (Partners)  │ │  (People)   │
   └──────┬──────┘ └──────┬──────┘ └──────┬──────┘
          │               │               │
          ▼               ▼               ▼
   ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
   │   STAGES    │ │  PO & BILLS │ │    TASKS    │
   │ (8 stages)  │ │ (Purchase)  │ │ (Assign)    │
   └──────┬──────┘ └──────┬──────┘ └─────────────┘
          │               │
          ▼               ▼
   ┌─────────────┐ ┌─────────────┐
   │     DC      │ │    STOCK    │
   │(Processing) │ │ (Inventory) │
   └──────┬──────┘ └─────────────┘
          │
          ▼
   ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
   │   WEEKLY    │ │   PROFIT    │ │   AUDITS    │
   │   WAGES     │ │   & LOSS    │ │  (Tracking) │
   └─────────────┘ └─────────────┘ └─────────────┘
```

---

## Module Connection Explained

### Orders → Everything

Orders are the **heart of the system**. Everything else connects to an order:

```
ORDER (LEO-2026-008)
    │
    ├── generates → STAGES (8 manufacturing stages)
    ├── needs     → PO (buy materials for this order)
    ├── needs     → DC (send material for processing)
    ├── creates   → TASKS (assigned work for staff)
    ├── affects   → STOCK (materials used from stock)
    ├── generates → WEEKLY WAGES (worker payments)
    └── tracked in→ PROFIT & LOSS (revenue vs cost)
```

### Suppliers → PO + DC

```
SUPPLIER
    ├── receives → PO (sell materials to factory)
    └── receives → DC (process factory's materials)
```

### PO → Stock → Orders

```
PO created (buy yarn/fabric)
    ↓
Supplier delivers material
    ↓
Stock increases
    ↓
Material used for Order production
    ↓
Stock decreases
```

### DC → Processing → Return

```
Order needs fabric processed
    ↓
DC created (send to supplier)
    ↓
Supplier processes (knit/dye/wash)
    ↓
Processed goods returned
    ↓
Return DC created (if issues)
    ↓
Stock updated
```

---

## Full Order Lifecycle — System View

```
STEP 1: CUSTOMER PLACES ORDER
User fills order form on web/mobile
        ↓
STEP 2: ORDER SAVED AS DRAFT
System generates Order ID
        ↓
STEP 3: ADMIN APPROVES
Approval Status module notifies admin
        ↓
STEP 4: RAW MATERIALS PURCHASED
PO & Bill Management module
        ↓
STEP 5: MATERIALS PROCESSED
DC Management module
        ↓
STEP 6: MANUFACTURING BEGINS
8 Stages tracked in Orders module
        ↓
STEP 7: TASKS ASSIGNED
Tasks module — work given to staff
        ↓
STEP 8: WAGES CALCULATED
Weekly Wages module
        ↓
STEP 9: BILLS MANAGED
PO & Bill Management + Due Payments
        ↓
STEP 10: ORDER COMPLETED
Profit & Loss updated
Audit trail recorded
```

---

## Data Flow Summary

```
USER INPUT
(Web / Mobile Form)
    ↓
API SERVER
(Validate + Process + Calculate)
    ↓
DATABASE
(Store all records)
    ↓
NOTIFICATIONS
(Alert admin for approvals)
    ↓
REPORTS
(Wages, P&L, Audits generated)
```

---

## Module Status at a Glance

| Module          | Triggered By   | Updates                   |
| --------------- | -------------- | ------------------------- |
| Orders          | Customer       | Stages, Tasks, Wages, P&L |
| Tasks           | Admin / Auto   | Order stages              |
| PO              | Admin          | Stock, Bills              |
| DC              | Admin          | Stock, Bills              |
| Supplier        | Admin          | PO, DC, Bills             |
| Weekly Wages    | Order stages   | Advance, PDF              |
| Approval Status | Any new record | Orders, PO, DC            |
| Stock           | PO Inward / DC | Order production          |
| Due Payments    | Bills          | Payment records           |
| Profit & Loss   | Orders, Bills  | Financial reports         |
| Audits          | Every action   | Full change log           |