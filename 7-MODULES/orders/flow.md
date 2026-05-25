# Orders — Complete Flow

```
USER OPENS APP
        │
        ▼
LOGIN → DASHBOARD
        │
        ▼
ORDERS LIST
(User sees own orders / Admin sees all)
        │
        ├─────────────────────────────────────┐
        │                                     │
        ▼                                     ▼
CLICK + ORDER                        CLICK EXISTING ORDER
        │                                     │
        ▼                                     ▼
CREATE ORDER FORM                    ORDER DETAIL SCREEN
│                                    │
├── Basic Info                       ├── Status Badge
├── Sizes + Quantities               ├── Summary info
├── Fabric Details                   ├── Tabs:
├── Yarn Details                     │   ├── Quantities
├── Trims                            │   ├── Fabric/Yarn
└── Other Prices                     │   ├── Trims
        │                            │   └── Stages
        ▼                            │         │
ORDER SAVED AS DRAFT                 │         ▼
        │                            │   STAGE DETAIL
        ▼                            │   (click any stage)
ADMIN NOTIFIED                       │   ├── Status
(Approval Status badge +1)           │   ├── Panel jobs table
        │                            │   ├── Size × Qty table
        ▼                            │   └── Completion %
ADMIN REVIEWS                        │
        │
        ├── REJECTS → stays Draft
        │
        └── APPROVES
                │
                ▼
        ORDER = IN PROGRESS
                │
                ▼
        8 STAGES CREATED (all Open)
                │
                ▼
        TASKS AUTO-ASSIGNED TO STAFF
                │
                ▼
        STAGE 1: FABRIC
        Check yarn + fabric received
                │ (if shortage → flag SHORTAGE)
                ▼
        STAGE 2: CUTTING
        Staff updates completed qty daily
        System calculates % completion
                │
                ▼
        STAGE 3: FEEDING
                │
                ▼
        STAGE 4: PRODUCTION
                │
                ▼
        STAGE 5: CHECKING
                │
                ▼
        STAGE 6: FINISHING
                │
                ▼
        STAGE 7: STORE
        Trims checked (labels, boxes)
                │
                ▼
        STAGE 8: QUALITY
        Final inspection
                │
                ▼
        ALL STAGES = COMPLETED
                │
                ▼
        ORDER STATUS = COMPLETED
                │
                ▼
        GOODS DELIVERED TO CUSTOMER
                │
                ▼
        PROFIT & LOSS UPDATED
        AUDIT TRAIL RECORDED
```