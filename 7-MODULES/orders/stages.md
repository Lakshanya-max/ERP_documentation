# Orders — Manufacturing Stages

## The 8 Stages

Every approved order goes through 8 stages in sequence. Each stage is tracked independently with status, quantities, completion %, and cost.

---

## Stage Sequence

```
ORDER APPROVED
      ↓
1. FABRIC      → Are materials ready?
      ↓
2. CUTTING     → Cut fabric into pieces
      ↓
3. FEEDING     → Feed pieces to production line
      ↓
4. PRODUCTION  → Stitch the garment
      ↓
5. CHECKING    → Quality check
      ↓
6. FINISHING   → Iron, fold, thread trim
      ↓
7. STORE       → Pack with labels and boxes
      ↓
8. QUALITY     → Final inspection
      ↓
ORDER COMPLETED
```

---

## Stage 1 — Fabric

**Purpose:** Verify yarn and fabric are received and ready.

|Tracks|Detail|
|---|---|
|Yarn Required|Type, weight expected vs received|
|Fabric Required|Weight, dia, GSM expected vs received|
|Inward Weight|What actually arrived|
|Difference|SHORTAGE if received < required|
|Due Date|When fabric should be ready|

---

## Stage 2 — Cutting

**Purpose:** Cut fabric rolls into garment pieces by size.

|Tracks|Detail|
|---|---|
|Total Qty|From order + 3% tolerance|
|Completed Qty|Pieces cut so far|
|QR Count|QR-tagged pieces|
|Completion %|(Completed ÷ Total) × 100|
|Panel Jobs|Different cut types tracked separately|

---

## Stage 3 — Feeding

**Purpose:** Feed cut pieces into stitching line.

|Tracks|Detail|
|---|---|
|Pieces Fed|How many sent to stitching|
|Panel wise|Per job type|

---

## Stage 4 — Production

**Purpose:** Assemble and stitch the garment.

|Tracks|Detail|
|---|---|
|Completed Qty|Pieces stitched|
|CMT Cost|Stitching cost per panel ₹|
|QR Count|QR-tagged pieces|
|Completion %|Progress|

---

## Stage 5 — Checking

**Purpose:** Quality check all stitched pieces.

|Tracks|Detail|
|---|---|
|Completed Qty|Pieces checked and passed|
|CMT Cost|Cost per panel ₹|
|Completion %|Progress|

---

## Stage 6 — Finishing

**Purpose:** Final touches — ironing, folding, thread trimming.

|Tracks|Detail|
|---|---|
|Completed Qty|Finished pieces|
|Completion %|Progress|

---

## Stage 7 — Store

**Purpose:** Pack garments with trims.

|Tracks|Detail|
|---|---|
|Production Trim|Labels — received vs expected|
|Packing Trim|Carton boxes — received vs expected|
|Inward Qty|What came into store|
|SHORTAGE|Flag if not enough received|

---

## Stage 8 — Quality

**Purpose:** Final quality inspection before delivery.

|Tracks|Detail|
|---|---|
|Pieces Inspected|Total checked|
|Pass / Fail|Quality outcome|
|Remarks|Notes on issues|

---

## Stage Status

|Status|When|
|---|---|
|`Open`|Not started|
|`In Progress`|1–99% done|
|`Completed`|100% done|

---

## Completion % Formula

```
Completion % = (Completed Qty ÷ Total Qty) × 100
Example: 90 ÷ 103 = 87.38%
```

---

## Who Updates Each Stage

|Stage|Updated By|
|---|---|
|Fabric|Merchandiser|
|Cutting|Cutting staff (e.g. Gowri)|
|Feeding|Feeding staff|
|Production|Production staff|
|Checking|Checking staff (e.g. Chinnaya)|
|Finishing|Finishing staff|
|Store|Store staff|
|Quality|Quality team|