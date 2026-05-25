# Weekly Wages — Complete Flow

## Weekly Wage Entry Flow

```
WORKER COMPLETES WORK EACH DAY
(Cutting / Feeding / Production /
 Checking / Finishing)
        │
        ▼
ADMIN / SUPERVISOR RECORDS DAILY WORK:
├── Order     → LEO-2026-008
├── Panel     → j or hm
├── Dept      → e.g. Cutting
├── Date      → e.g. Mon 18 May
└── Pieces    → e.g. 50 pieces
        │
        ▼
SYSTEM CALCULATES:
Daily Wage = 50 pieces × ₹2 = ₹100
        │
        ▼
ENTRY SAVED TO WAGE TABLE
        │
        ▼
REPEATED DAILY FOR ALL WORKERS
ALL DEPARTMENTS ALL PANELS
        │
        ▼ (end of week)
ADMIN OPENS WEEKLY WAGES MODULE
        │
        ▼
SELECTS DATE RANGE:
From: 15 May 2026
To:   21 May 2026 (auto +6 days)
        │
        ▼
SEES ORDER CARDS WITH PANEL INFO
        │
        ▼
CLICKS ORDER CARD (e.g. LEO-2026-008)
        │
        ▼
WAGE DETAIL SCREEN OPENS:
│
├── PANEL j TABLE:
│   Dept      │ Fr │ Sa │ Su │ Mo │ Tu │ We │ Th │ Total
│   Cutting   │ 20 │ 30 │  - │ 50 │ 45 │ 40 │ 35 │  220
│   Feeding   │ 20 │ 30 │  - │ 50 │ 45 │ 40 │ 35 │  220
│   Production│ 15 │ 25 │  - │ 40 │ 35 │ 30 │ 30 │  175
│   Checking  │ 10 │ 15 │  - │ 20 │ 20 │ 15 │ 15 │   95
│   Finishing │  5 │ 10 │  - │ 15 │ 10 │ 10 │ 10 │   60
│   Day Total │ 70 │110 │  - │175 │155 │135 │125 │  770
│
├── PANEL hm TABLE:
│   (same structure)
│
└── GRAND TOTAL (all panels combined)
        │
        ▼
IF WORKER TOOK ADVANCE:
Admin clicks "Add Advance"
├── Worker Name
├── Amount ₹
└── Date
        │
        ▼
SYSTEM UPDATES NET SALARY:
Total Wages - Advance = Final Payable
        │
        ▼
ADMIN DOWNLOADS PDF
(complete wage sheet for payment)
        │
        ▼
SALARY PAID TO WORKERS
        │
        ▼
FULL RECORD MAINTAINED IN SYSTEM
```

---

## Wage Viewing Flow (Check Any Week)

```
ADMIN OPENS WEEKLY WAGES
        │
        ▼
CHANGES DATE FILTER:
From: [any past date]
To:   [auto +6 days]
        │
        ▼
SYSTEM LOADS:
├── All orders active in that week
├── All panel-wise work done
└── All advances given
        │
        ▼
ADMIN REVIEWS OR PRINTS REPORT
```