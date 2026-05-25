# Admin Role — LEO Fashions

## Who Is an Admin?

The Admin is the **factory owner or manager** who has full access to every module in the system. Nothing in the system proceeds without admin involvement — all approvals, creations of POs and DCs, supplier management, and financial tracking are admin responsibilities.

---

## Admin Access — Complete Screen List

|Module|Can View|Can Create|Can Edit|Can Approve|Can Delete|
|---|---|---|---|---|---|
|Dashboard|✅ All data|—|—|—|—|
|Orders|✅ All orders|✅|✅|✅|✅|
|Order Stages|✅ All|✅ Update|✅|—|—|
|Tasks|✅ All tasks|✅|✅|—|✅|
|Supplier Management|✅ All|✅|✅|✅ Verify|✅|
|PO & Bill Management|✅ All|✅|✅|✅|✅|
|DC Management|✅ All|✅|✅|✅|✅|
|Return DC|✅ All|✅|✅|—|—|
|Due Payments|✅ All|—|✅|—|—|
|Stock Management|✅ All|—|✅|—|—|
|Weekly Wages|✅ All orders|✅ Add advance|✅|—|—|
|Approval Status|✅ All pending|—|—|✅|—|
|Profit & Loss|✅ Full report|—|—|—|—|
|Users|✅ All users|✅|✅|—|✅|
|Audits|✅ Full log|—|—|—|—|
|FAQ|✅|✅|✅|—|✅|

---

## Admin Flow — Day to Day

### Morning Routine

```
1. Open Dashboard
   → Check overview stats
        ↓
2. Open Approval Status (badge count)
   → Approve pending Orders / POs / DCs
        ↓
3. Open Due Payments
   → Check overdue supplier bills
```

### When a New Order Arrives

```
Order notification appears
        ↓
Admin opens Approval Status
        ↓
Reviews order: style, qty, fabric, price
        ↓
Approves → Order goes In Progress
        ↓
Creates PO for raw materials (if needed)
        ↓
Creates DC for processing (if needed)
        ↓
Assigns tasks to staff
```

### When Material Arrives (PO Inward)

```
Supplier delivers material
        ↓
Admin adds PO Inward entry
├── Date, Qty received, Remarks
        ↓
System updates remaining qty
        ↓
If fully received → PO status = Closed
```

### When Processed Goods Return (DC Inward)

```
Supplier returns processed material
        ↓
Admin adds DC Inward entry
        ↓
System calculates processing loss
        ↓
Adds DC Bill (supplier's processing charge)
```

### End of Week

```
Opens Weekly Wages
        ↓
Reviews panel-wise work done
        ↓
Adds advance payments if any
        ↓
Downloads PDF wage sheets
        ↓
Makes salary payments
```

---

## What Only Admin Can Do

|Action|Why Admin Only|
|---|---|
|Approve orders|Ensures quality check before production|
|Approve POs|Controls purchasing budget|
|Approve DCs|Controls material movement|
|Verify suppliers|Ensures trusted supplier network|
|View all orders|Full factory visibility|
|Access financial data|Sensitive business information|
|Manage users|Control system access|
|View audit logs|Security and accountability|
|Export reports|Business decision making|

---

## Admin Sidebar — All Visible Items

```
✅ Dashboard
✅ Orders
✅ Tasks
✅ Supplier Management
✅ PO & Bill Management
✅ Due Payments
✅ Stock Management
✅ DC Management
✅ Profit & Loss
✅ Weekly Wages
✅ Approval Status  [31]  ← badge count
✅ Users
✅ Audits
✅ FAQ
```