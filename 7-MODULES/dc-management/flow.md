# DC Management — Complete Flow

## Regular DC Flow

```
ORDER NEEDS MATERIAL PROCESSED
(e.g. fabric needs knitting)
        │
        ▼
ADMIN OPENS DC MANAGEMENT
        │
        ▼
CLICKS + CREATE DC
        │
        ▼
FILLS DC FORM:
├── DC Date        → Today
├── Order Number   → LEO-2026-031
├── Supplier From  → SHIVALAYA KNITS
├── Supplier To    → Harish
├── Department     → Fabric
├── Process        → Knitting
└── Qty to Send    → 20 Kg
        │
        ▼
DC SAVED:
├── DC ID          = DC-2026-0028
├── Total Sent     = 20 Kg
├── Received Back  = 0 Kg
├── Remaining      = 20 Kg
├── Status         = Partial + Pending
└── Bill Status    = Bill: Open
        │
        ▼
ADMIN APPROVES DC
(Approval Status or DC detail)
        │
        ▼
DC STATUS = Partial + Approved
        │
        ▼
MATERIAL PHYSICALLY SENT TO SUPPLIER
(with printed DC document)
        │
        ▼
SUPPLIER DOES THE PROCESS
(Knitting / Dyeing / Washing...)
        │
        ▼
PROCESSED GOODS RETURNED TO FACTORY
        │
        ▼
EMPLOYEE ADDS DC INWARD:
├── Received Date
├── Received Qty   → e.g. 5 Kg
└── Remarks
        │
        ▼
SYSTEM UPDATES:
├── Received Back  = 5 Kg
├── Remaining      = 15 Kg
├── Processing Loss= tracked
└── Inward Status  = Inward: Partial
        │
        ▼
MORE GOODS RETURN OVER TIME
(more DC Inwards added)
        │
        ▼
WHEN ALL GOODS RECEIVED:
├── Remaining      = 0
└── Inward Status  = Inward: Complete ✅
        │
        ▼
SUPPLIER RAISES PROCESSING BILL
        │
        ▼
ADMIN ADDS DC BILL:
├── Amount ₹
├── GST %
├── Bill Date
└── Bill Photo
        │
        ▼
BILL STATUS = Bill: Open
        │
        ▼
PAYMENT MADE
        │
        ▼
BILL STATUS = Bill: Paid ✅
        │
        ▼
DC FULLY COMPLETE
```

---

## Return DC Flow

```
CUSTOMER NOT SATISFIED / DAMAGED GOODS
        │
        ▼
ADMIN OPENS DC MANAGEMENT
        │
        ▼
CLICKS + CREATE DC → Return DC tab
        │
        ▼
FILLS RETURN DC FORM:
├── Select Order
├── Select original DC
│       ↓ (From Supplier auto-fills)
├── Remarks
└── Photo (optional)
        │
        ▼
CHOOSES DESTINATION:
        │
        ├── OTHER SUPPLIER TAB
        │   ├── Select To Supplier
        │   └── Goods sent to another
        │       customer for redesign
        │
        └── STOCK TAB
            └── Goods stored in
                warehouse as stock
```