# UI Flow — LEO Fashions

## How Every Screen Connects

---

## Entry Flow

```
App Opens
    ↓
LOGIN SCREEN
    ↓ (success)
DASHBOARD
    ↓
[Sidebar Navigation]
```

---

## Orders Flow

```
ORDERS LIST
├── Filters: Status / Classification / Unit / Search
├── Click card
│       ↓
│   ORDER DETAIL
│   ├── Tab: Order Summary
│   ├── Tab: Quantities (size-wise table)
│   ├── Tab: Fabric + Yarn details
│   ├── Tab: Trims
│   ├── Tab: Other Prices
│   └── Tab: Stages
│           ├── Stage 1: Fabric
│           ├── Stage 2: Cutting → click → STAGE DETAIL
│           ├── Stage 3: Feeding
│           ├── Stage 4: Production
│           ├── Stage 5: Checking
│           ├── Stage 6: Finishing
│           ├── Stage 7: Store
│           └── Stage 8: Quality
│
└── + Order button
        ↓
    CREATE ORDER FORM
    (multi-section form)
        ↓ submit
    Order saved as Draft
        ↓
    Back to ORDERS LIST
```

---

## Tasks Flow

```
TASKS LIST
├── Tabs: My Tasks / Given Tasks / All
├── Filters: Status (Completed / Pending) / Search
├── Click task card
│       ↓
│   TASK DETAIL
│   (view task info, order link, assignee)
│
└── + Task button (Admin only)
        ↓
    CREATE TASK FORM
        ↓ submit
    Task assigned to user
        ↓
    Back to TASKS LIST
```

---

## Supplier Management Flow

```
SUPPLIERS LIST
├── Tabs: Process Suppliers / Other Suppliers
├── Filters: Search / Supplier Type / Status (Active)
├── Click supplier card
│       ↓
│   SUPPLIER DETAIL
│   ├── Tab: Basic Details
│   │   (Name, Contact, Address, GST, PAN,
│   │    Bank Details, Verification Info)
│   └── Tab: Bills
│       (All invoices from this supplier)
│       └── + Add Bill → BILL FORM
│
└── + Supplier button (Admin only)
        ↓
    CREATE SUPPLIER FORM
        ↓ submit
    Supplier saved (Pending verification)
        ↓
    Admin verifies → Status = Verified
```

---

## PO & Bill Management Flow

```
PO LIST
├── Filters: Search / Supplier / Status / Material Category
├── Click PO card
│       ↓
│   PO DETAIL
│   ├── Tab: Basic Details
│   │   (Supplier, yarn type, qty, rate, GST, order link)
│   ├── Tab: Inwards
│   │   └── + Add Inward → INWARD FORM
│   ├── Tab: Bills
│   │   └── + Add Bill → BILL FORM
│   └── Tab: Remaining Stocks
│
└── + Purchase Order button
        ↓
    CREATE PO FORM
        ↓ submit
    PO saved → Admin approves
        ↓
    Back to PO LIST
```

---

## DC Management Flow

```
DC LIST
├── Filters: Search / Status / Supplier / Date
├── Tabs: Processing DC / General DC / Return DC
├── Click DC card
│       ↓
│   DC DETAIL
│   ├── Tab: Basic Details
│   ├── Tab: DC Inwards
│   │   └── + Add Inward → INWARD FORM
│   ├── Tab: DC Bills
│   │   └── + Add Bill → BILL FORM
│   └── Tab: Remaining Stocks
│
└── + Create DC button
        ↓
    CREATE DC FORM
    (Processing / General / Return DC)
        ↓ submit
    DC saved → Admin approves
```

---

## Weekly Wages Flow

```
WEEKLY WAGES LIST
├── Filters: From Date / To Date / Search
├── Click order card
│       ↓
│   WAGE DETAIL (for that order)
│   ├── Select Week (from/to dates)
│   ├── Panel-wise breakdown table
│   │   (department × day × pieces)
│   ├── Grand Total
│   ├── Add Advance button
│   │       ↓
│   │   ADVANCE FORM
│   │   (worker name + amount)
│   └── Download PDF button
│
└── Print button (for full wage report)
```

---

## Approval Status Flow

```
APPROVAL STATUS LIST
(badge shows pending count e.g. 31)
├── Shows: Orders / POs / DCs pending approval
├── Click item
│       ↓
│   Opens the detail screen
│   (Order Detail / PO Detail / DC Detail)
│       ↓
│   Admin reviews
│       ↓
│   Click Approve button
│       ↓
│   Status updated → removed from approval list
│   Badge count decreases
```