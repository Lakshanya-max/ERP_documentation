# Supplier Management — Complete Flow

## Adding a New Supplier

```
ADMIN OPENS SUPPLIER MANAGEMENT
        │
        ▼
CLICKS + SUPPLIER
        │
        ▼
FILLS SUPPLIER FORM:
├── Name, Contact, Address
├── GST Number, PAN Number
├── Supplier Types (multi-select)
├── Payment Terms
├── State
└── Bank Details (optional)
        │
        ▼
SUPPLIER SAVED
Status = Pending Verification
        │
        ▼
ADMIN REVIEWS DETAILS
(GST, PAN, Bank verified manually)
        │
        ▼
ADMIN CLICKS VERIFY
        │
        ▼
Status = ✅ VERIFIED
Verified By = Admin
Verified On = Today's date
        │
        ▼
SUPPLIER AVAILABLE FOR USE IN:
├── PO (Purchase Orders)
└── DC (Delivery Challans)
```

---

## Supplier in PO Flow

```
ADMIN CREATES PURCHASE ORDER
        │
        ▼
SELECTS SUPPLIER from verified list
        │
        ▼
PO linked to this supplier
        │
        ▼
SUPPLIER DELIVERS MATERIAL
        │
        ▼
PO INWARD ADDED
        │
        ▼
SUPPLIER RAISES INVOICE
        │
        ▼
BILL ADDED to PO Bills tab
        │
        ▼
PAYMENT MADE → bill_status = Paid
```

---

## Supplier in DC Flow

```
ADMIN CREATES DC
        │
        ▼
SELECTS SUPPLIER (from / to)
        │
        ▼
DC linked to this supplier
        │
        ▼
MATERIAL SENT to supplier for processing
        │
        ▼
PROCESSED GOODS RETURNED
        │
        ▼
DC INWARD ADDED
        │
        ▼
SUPPLIER RAISES PROCESSING BILL
        │
        ▼
BILL ADDED to DC Bills tab
```

---

## Supplier List View Flow

```
ADMIN OPENS SUPPLIERS
        │
        ├── TAB: Process Suppliers
        │   (Knitting, Dyeing, CMT etc.)
        │
        └── TAB: Other Suppliers
            (Yarn, Fabric, Transport etc.)
        │
        ▼
FILTERS:
├── Search by name
├── Filter by Supplier Type
└── Filter by Status (Active)
        │
        ▼
CLICK SUPPLIER CARD
        │
        ▼
SUPPLIER DETAIL SCREEN
├── Tab: Basic Details
└── Tab: Bills
```