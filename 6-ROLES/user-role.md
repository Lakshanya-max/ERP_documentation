# User Role — LEO Fashions

## Who Is a User?

A User is a **customer or buyer** who places clothing orders through the LEO Fashions platform. They have limited access — they can place orders, view their own orders and track progress, and receive tasks assigned to them.

---

## User Access — What They Can and Cannot Do

|Module|Can Access|What They Can Do|
|---|---|---|
|Dashboard|✅|View own order summary|
|Orders|✅ Own orders only|View, create new orders|
|Order Detail|✅ Own orders|View all tabs, track stages|
|Tasks|✅ Own tasks only|View My Tasks, mark complete|
|Supplier Management|❌|No access|
|PO & Bill Management|❌|No access|
|DC Management|❌|No access|
|Due Payments|❌|No access|
|Stock Management|❌|No access|
|Weekly Wages|❌|No access|
|Approval Status|❌|No access|
|Profit & Loss|❌|No access|
|Users|❌|No access|
|Audits|❌|No access|
|FAQ|✅|View help content|

---

## User Flow — Step by Step

### Placing a New Order

```
User logs in
        ↓
Opens Orders from sidebar
        ↓
Clicks + Order button
        ↓
Fills order form:
├── Classification (Bulk/Sample)
├── Style and sizes
├── Quantity per size
├── Fabric details (color, weight, GSM)
├── Yarn details
├── Trims (labels, boxes)
├── CMT price
└── Delivery date
        ↓
Submits form
        ↓
Order saved as Draft
        ↓
Admin notified for approval
        ↓
User waits for approval
```

### Tracking an Order

```
User opens Orders List
        ↓
Sees only their own orders
        ↓
Clicks on an order
        ↓
Views Order Detail:
├── Current status (Draft/In Progress/Completed)
├── Stage progress (which stage is active)
├── Fabric and yarn status
├── Trim availability
└── Completion percentage
```

### Managing Tasks

```
User opens Tasks
        ↓
Sees My Tasks tab (tasks assigned to them)
        ↓
Views task details:
├── Task name
├── Linked order
├── Due date
├── Assigned by (Admin)
        ↓
Completes task
        ↓
Marks task as Completed
```

---

## User Sidebar — Visible Items Only

```
✅ Dashboard
✅ Orders
✅ Tasks
❌ Supplier Management   (hidden)
❌ PO & Bill Management  (hidden)
❌ Due Payments          (hidden)
❌ Stock Management      (hidden)
❌ DC Management         (hidden)
❌ Profit & Loss         (hidden)
❌ Weekly Wages          (hidden)
❌ Approval Status       (hidden)
❌ Users                 (hidden)
❌ Audits                (hidden)
✅ FAQ
```

---

## What User Cannot See

|Restricted Data|Reason|
|---|---|
|Other users' orders|Data privacy|
|Supplier information|Internal factory data|
|Purchase orders|Procurement is internal|
|Delivery challans|Processing is internal|
|Financial reports|Business sensitive|
|Worker wages|HR data|
|Approval queue|Admin function only|
|System audit logs|Admin function only|

---

## User Notifications

|Event|Notification|
|---|---|
|Order approved by admin|Status changes to In Progress|
|Task assigned|Appears in My Tasks|
|Stage completed|Visible in order detail|
|Order completed|Status changes to Completed|