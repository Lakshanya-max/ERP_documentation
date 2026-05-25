# Business Logic Workflow — LEO Fashions

## Complete End-to-End Workflow

---

```
STEP 1 ─ CUSTOMER PLACES ORDER
│
│  User fills order form:
│  Classification (Bulk/Sample), Style, Sizes,
│  Quantities, Fabric, Yarn, Trims, CMT Price,
│  Delivery Date
│
│  System does:
│  → Generate Order ID (LEO-YYYY-XXX)
│  → Calculate cutting qty (+3% tolerance)
│  → Set Status = Draft
│  → Notify Admin
│
▼
STEP 2 ─ ADMIN APPROVES ORDER
│
│  Admin opens Approval Status
│  Reviews order details
│  Clicks Approve
│
│  System does:
│  → Status = In Progress
│  → Create 8 Stage records (all = Open)
│  → Auto-generate Tasks for staff
│
▼
STEP 3 ─ RAW MATERIALS PURCHASED (PO)
│
│  Admin creates Purchase Order:
│  Supplier + Material + Qty + Rate + GST
│  Links to Order
│
│  System does:
│  → Generate PO ID (PO-YYYY-XXXX)
│  → Calculate total amount
│  → Status = Open + Pending Approval
│
│  Admin approves PO → Status = Approved
│
│  Supplier delivers material:
│  → PO Inward entry added
│  → Received qty updated
│  → Remaining qty recalculated
│  → Status = Partial or Closed
│
▼
STEP 4 ─ MATERIAL SENT FOR PROCESSING (DC)
│
│  Admin creates Delivery Challan:
│  Supplier + Process + Qty + Order link
│
│  System does:
│  → Generate DC ID (DC-YYYY-XXXX)
│  → Set total_sent, received_back=0, remaining=sent
│  → Status = Partial + Pending Approval
│
│  Admin approves DC → Status = Approved
│
│  Material sent to supplier physically
│
│  Processed goods return:
│  → DC Inward entry added
│  → received_back updated
│  → remaining recalculated
│  → Processing loss recorded
│
│  Supplier raises bill:
│  → DC Bill added
│  → bill_status = Open
│
▼
STEP 5 ─ MANUFACTURING STAGES
│
│  8 stages progress in sequence:
│  Fabric → Cutting → Feeding → Production
│  → Checking → Finishing → Store → Quality
│
│  Each stage:
│  → Staff updates completed quantity
│  → System calculates completion %
│  → Status: Open → In Progress → Completed
│
│  When ALL 8 stages = Completed:
│  → Order Status = Completed
│
▼
STEP 6 ─ BILLS AND PAYMENTS
│
│  Supplier bills tracked in Bill Management
│  Payment recorded when done
│  Due Payments shows overdue bills
│
▼
STEP 7 ─ WEEKLY WAGES
│
│  Every week:
│  → Pieces manufactured per day per dept recorded
│  → Wages auto-calculated (pieces × rate)
│  → Advance deducted if any
│  → PDF generated for salary payment
│
▼
STEP 8 ─ ORDER COMPLETE
│
│  All stages done
│  All bills paid
│  Goods delivered to customer
│  Profit & Loss updated
│  Full audit trail recorded
```