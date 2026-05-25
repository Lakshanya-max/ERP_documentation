# Architecture Flow — LEO Fashions

## How Every Request Flows Through the System

---

## Standard Request Flow

```
USER ACTION (click / submit / tap)
        │
        ▼
CLIENT (Web / Mobile)
Builds HTTP request with:
├── URL endpoint
├── Auth token (from session)
├── Request data (JSON body)
        │
        ▼ HTTPS
API SERVER
├── Step 1: Authenticate
│   └── Is token valid? Role check?
├── Step 2: Validate
│   └── Are all required fields present?
├── Step 3: Business Logic
│   └── Calculate values, set defaults
├── Step 4: Database Operation
│   └── Read or Write
├── Step 5: Build Response
│   └── Format data as JSON
        │
        ▼
CLIENT receives response
├── Success → Update UI, show message
└── Error   → Show error to user
```

---

## Order Creation Flow

```
User fills form → submits
        ↓
POST /api/orders
        ↓
API: validate fields
        ↓
API: generate LEO-YYYY-XXX
        ↓
API: calculate cutting qty (×1.03)
        ↓
API: set status = Draft
        ↓
DB: INSERT into ORDERS + related tables
        ↓
API: trigger approval notification
        ↓
Response: { order_id, status: "Draft" }
        ↓
UI: show success, redirect to order detail
```

---

## Admin Approval Flow

```
Admin clicks Approve
        ↓
PATCH /api/orders/:id/approve
        ↓
API: verify admin role
        ↓
API: update status = In Progress
        ↓
API: create 8 ORDER_STAGES records
        ↓
API: auto-generate tasks
        ↓
DB: UPDATE ORDERS + INSERT STAGES + TASKS
        ↓
Response: { status: "In Progress" }
        ↓
UI: update badge count, show approved
```

---

## Data Retrieval Flow (List Screen)

```
User opens Orders List
        ↓
GET /api/orders?status=In+Progress&unit=Main+Unit
        ↓
API: check role
├── Admin  → WHERE no user filter
└── User   → WHERE created_by = current user
        ↓
API: apply filters + pagination
        ↓
DB: SELECT from ORDERS JOIN STAGES
        ↓
API: calculate completion % per order
        ↓
Response: { orders: [...], total: 120, page: 1 }
        ↓
UI: render order cards with progress rings
```

---

## PO Inward Update Flow

```
Employee adds inward entry
        ↓
POST /api/po/:id/inwards
        ↓
API: save inward record
        ↓
API: recalculate:
├── received_qty += new received
├── remaining = total - received
└── if remaining = 0: status = Closed
    else: status = Partial
        ↓
DB: INSERT PO_INWARDS
DB: UPDATE PURCHASE_ORDERS
DB: UPDATE STOCK
        ↓
Response: { updated PO data }
        ↓
UI: refresh PO detail screen
```

---

## Stage Update Flow

```
Staff updates stage completion
        ↓
PATCH /api/stages/:id
        ↓
API: save completed quantities
        ↓
API: calculate % = (completed ÷ total) × 100
        ↓
API: update stage status:
├── 0%       → Open
├── 1-99%    → In Progress
└── 100%     → Completed
        ↓
API: check if ALL 8 stages = Completed
└── Yes → UPDATE ORDER status = Completed
        ↓
DB: UPDATE ORDER_STAGES
DB: UPDATE STAGE_PANEL_JOBS
DB: UPDATE ORDERS (if all done)
```