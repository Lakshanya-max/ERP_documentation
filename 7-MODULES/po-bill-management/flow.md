# PO & Bill Management — Complete Flow

```
FACTORY NEEDS RAW MATERIAL
(e.g. Yarn for Order LEO-2026-002)
        │
        ▼
ADMIN OPENS PO & BILL MANAGEMENT
        │
        ▼
CLICKS + PURCHASE ORDER
        │
        ▼
FILLS PO FORM:
├── Supplier       → SUREYA TRADERS
├── Material       → Yarn
├── Order Link     → LEO-2026-002
├── Yarn Type      → 10s, 100% cotton
├── Color          → FLEECE-Blue-TOP
├── Quantity       → 1,000 Kg
├── Rate           → ₹10 per Kg
├── GST            → 5%
└── Delivery Address
        │
        ▼
SYSTEM CALCULATES:
├── Subtotal  = 1000 × ₹10 = ₹10,000
├── GST       = ₹10,000 × 5% = ₹500
└── Total     = ₹10,500
        │
        ▼
PO SAVED
├── PO ID     = PO-2026-0051
├── Status    = Open
└── Approval  = Pending
        │
        ▼
ADMIN APPROVES PO
(from Approval Status or PO detail)
        │
        ▼
PO STATUS = OPEN + APPROVED
        │
        ▼
PO SHARED WITH SUPPLIER
(Print / Share button)
        │
        ▼
SUPPLIER DELIVERS MATERIAL
        │
        ▼
EMPLOYEE ADDS PO INWARD:
├── Received Date
├── Received Qty   → e.g. 500 Kg
└── Remarks
        │
        ▼
SYSTEM UPDATES:
├── Received Qty  = 500
├── Remaining     = 500
└── Status        = Partial
        │
        ▼
REMAINING MATERIAL ARRIVES
        │
        ▼
ANOTHER INWARD ENTRY ADDED
(Received 500 more Kg)
        │
        ▼
SYSTEM UPDATES:
├── Received Qty  = 1,000
├── Remaining     = 0
└── Status        = CLOSED ✅
        │
        ▼
SUPPLIER RAISES INVOICE
        │
        ▼
ADMIN ADDS PO BILL:
├── Amount ₹
├── GST %
├── Bill Date
└── Bill Photo
        │
        ▼
BILL PAYMENT STATUS = Open
        │
        ▼
PAYMENT MADE
        │
        ▼
BILL PAYMENT STATUS = Paid ✅
        │
        ▼
PO FULLY COMPLETE
```