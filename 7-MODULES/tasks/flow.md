# Tasks — Complete Flow

## Auto Task Flow

```
ORDER APPROVED BY ADMIN
        │
        ▼
SYSTEM AUTO-CREATES TASKS
(based on order stages and panels)
        │
        ▼
TASKS ASSIGNED TO STAFF MEMBERS
(prefix: [Auto], linked to Order ID)
        │
        ▼
STAFF OPENS APP → TASKS → MY TASKS TAB
        │
        ▼
STAFF SEES ASSIGNED TASK:
├── Task name
├── Order link
├── Assigned by Admin
└── Due date
        │
        ▼
STAFF WORKS ON THE TASK
        │
        ▼
STAFF MARKS TASK AS COMPLETED
        │
        ▼
TASK MOVES TO COMPLETED TAB
        │
        ▼
ADMIN SEES COMPLETION IN GIVEN TASKS TAB
```

---

## Manual Task Flow (Admin Creates)

```
ADMIN OPENS TASKS MODULE
        │
        ▼
CLICKS + TASK BUTTON
        │
        ▼
FILLS TASK FORM:
├── Task Name
├── Assign To (select user)
├── Order Number (optional)
└── Due Date
        │
        ▼
TASK SAVED → STATUS = PENDING
        │
        ▼
ASSIGNED PERSON SEES IT IN MY TASKS
        │
        ▼
PERSON COMPLETES TASK
        │
        ▼
STATUS = COMPLETED
        │
        ▼
APPEARS IN COMPLETED FILTER
```

---

## Admin Monitoring Flow

```
ADMIN OPENS TASKS
        │
        ▼
CLICKS "GIVEN TASKS" TAB
        │
        ├── Filter: All      → See everything
        ├── Filter: Pending  → See what's not done
        └── Filter: Completed→ See what's done
        │
        ▼
ADMIN TRACKS WHO DID WHAT AND WHEN
```

---

## Task Visibility Summary

```
MY TASKS TAB
└── Shows tasks assigned TO the logged-in user

GIVEN TASKS TAB (Admin only)
└── Shows all tasks Admin has assigned to others

ALL TAB (Admin only)
└── Shows every task in the entire system
```