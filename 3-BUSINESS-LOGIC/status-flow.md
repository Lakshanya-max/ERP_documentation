# Status Flow — LEO Fashions

## All Statuses Across All Modules

---

## Orders

```
Draft ──► In Progress ──► Completed
```

|Status|Meaning|
|---|---|
|`Draft`|Created, waiting for admin approval|
|`In Progress`|Approved, manufacturing happening|
|`Completed`|All 8 stages done, delivered|

---

## Purchase Orders (PO)

```
Open + Pending ──► Open + Approved ──► Partial ──► Closed
```

|Status|Meaning|
|---|---|
|`Open`|Approved, waiting for material delivery|
|`Partial`|Some material received, not all|
|`Closed`|All material received|
|`Pending`|Waiting for admin approval|
|`Approved`|Admin has verified|

---

## Delivery Challans (DC)

```
Partial + Pending ──► Partial + Approved ──► Inward: Partial ──► Inward: Complete
Bill: Open ──────────────────────────────────────────────────► Bill: Paid
```

|Status|Meaning|
|---|---|
|`Partial`|Not all goods returned yet|
|`Completed`|All goods returned|
|`Inward: Partial`|Some goods received back|
|`Inward: Complete`|All goods received back|
|`Bill: Open`|Supplier bill not yet paid|
|`Bill: Paid`|Payment done|
|`Approved`|Admin verified|

---

## Manufacturing Stages

```
Open ──► In Progress ──► Completed
```

|Status|When|
|---|---|
|`Open`|Stage created, work not started|
|`In Progress`|Some work done (1–99%)|
|`Completed`|All pieces done (100%)|

---

## Tasks

```
Pending ──► Completed
```

|Status|Meaning|
|---|---|
|`Pending`|Task assigned, not done|
|`Completed`|Task finished|

---

## Supplier

|Status|Meaning|
|---|---|
|`Verified`|Admin has verified supplier details|
|`Pending`|Not yet verified|

---

## Bills

```
Open ──► Partial ──► Paid
```

|Status|Meaning|
|---|---|
|`Open`|Bill raised, payment pending|
|`Partial`|Partially paid|
|`Paid`|Fully settled|

---

## Material Flags

|Flag|Where|Meaning|
|---|---|---|
|`SHORTAGE`|Stages / DC|Received less than expected|
|`Partial`|PO / DC|Partially completed|
|`~87.38%`|Stage jobs|Exact completion percentage|

---

## Complete Status Color Reference

| Status      | Color      |
| ----------- | ---------- |
| Draft       | Grey       |
| In Progress | Blue       |
| Completed   | Green      |
| Open        | Orange     |
| Partial     | Purple     |
| Closed      | Green      |
| Approved    | Green tick |
| Pending     | Grey       |
| Bill: Open  | Orange dot |
| Bill: Paid  | Green dot  |
| SHORTAGE    | Red        |