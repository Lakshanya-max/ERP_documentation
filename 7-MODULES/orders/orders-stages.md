# Orders Module — Stages

## What are Stages?

Stages are production milestones tracked inside an order. They represent the real-world steps a garment passes through on the factory floor — from raw material to finished product. Each stage has an owner, a status, and timestamps.

Stages are visible under the **Stages** tab inside any Order Detail page.

---

## Stages Tab Location

```
Order Detail Page
│
├── [ Summary ]     ← order data, fabric, trims, pricing
├── [ Stages ]      ← production milestone tracking   ◄ THIS TAB
└── [ Files ]       ← attachments
```

---

## Typical Production Stages

The following stages represent the standard garment manufacturing flow at LEO Fashions. Stages may be configured per order type (Bulk / Sample):

```
┌─────────────────────────────────────────────────────────┐
│  Stage               Status         Assigned To          │
├─────────────────────────────────────────────────────────┤
│  1. Yarn Procurement     ● Done      Store Manager        │
│  2. Knitting             ● Done      Production           │
│  3. Fabric Processing    ● Done      Processing Unit      │
│  4. Cutting              ◐ In Prog   Cutting Supervisor   │
│  5. Stitching            ○ Pending   —                    │
│  6. Checking             ○ Pending   —                    │
│  7. Washing / Finishing  ○ Pending   —                    │
│  8. Packing              ○ Pending   —                    │
│  9. Dispatch             ○ Pending   —                    │
└─────────────────────────────────────────────────────────┘
```

---

## Stage Status Values

|Status|Indicator|Description|
|---|---|---|
|Pending|○ Empty ring|Stage not yet started|
|In Progress|◐ Half-filled|Stage actively being worked|
|Done|● Filled / Green|Stage completed|

---

## Stage Fields

Each stage record contains:

|Field|Description|
|---|---|
|Stage Name|Name of the production step|
|Status|`Pending` · `In Progress` · `Done`|
|Assigned To|User or team responsible for this stage|
|Started At|Timestamp when stage was marked In Progress|
|Completed At|Timestamp when stage was marked Done|
|Remarks|Optional notes or issues flagged at this stage|

---

## Stage Progress Ring

The stage completion progress is visible as a **circular ring** on the Order card in the Orders list page. The ring fills as more stages reach `Done` status, giving a quick at-a-glance view of how far along production is without opening the order.

```
Orders List
│
├── [👕] Draft  LEO-2026-036 | nn         ◌   ← 0% stages done
├── [👕] Draft  LEO-2026-033 | testorg    ◑   ← ~50% stages done
└── [👕] Draft  LEO-2026-032 | hoodie     ●   ← all stages done
```

---

## Order Status Driven by Stages

Stage completion directly drives the order's top-level `status` field:

```
All stages = Pending / In Progress
        │
        ▼
   Status: In Progress

All stages = Done
        │
        ▼
   Status: Completed
```

---

## Order Status State Machine

```
              CREATE
                │
                ▼
          ┌──────────┐
          │  Draft   │  ◄── default on creation
          └────┬─────┘
               │  First stage started / manual trigger
               ▼
       ┌─────────────┐
       │ In Progress │
       └──────┬──────┘
              │  All stages marked Done
              ▼
        ┌──────────┐
        │ Completed│
        └──────────┘
```

|Transition|Trigger|Who|
|---|---|---|
|Draft → In Progress|First stage started or manual trigger|Admin / Manager|
|In Progress → Completed|All stages marked Done|System / Manager|

---

## Approval Status State Machine

Approval is tracked separately from production status. An order can be `In Progress` in production while still `Draft` in approval.

```
              CREATE
                │
                ▼
          ┌──────────┐
          │  Draft   │
          └────┬─────┘
               │  Submit for Approval
               ▼
          ┌──────────┐
          │ Pending  │  ← appears in Approval Status queue
          └────┬─────┘
          ┌────┴─────┐
          ▼          ▼
     ┌─────────┐ ┌──────────┐
     │Approved │ │ Rejected │
     └─────────┘ └──────────┘
```

|Transition|Trigger|Who|
|---|---|---|
|Draft → Pending|Staff submits for approval|Admin / Manager|
|Pending → Approved|Approver approves in queue|Approver / Admin|
|Pending → Rejected|Approver rejects with remarks|Approver / Admin|

---

## Edit Permissions by Status

|Action|Draft|In Progress|Completed|
|---|---|---|---|
|Edit order fields|✅|✅|❌|
|Add / modify quantities|✅|⚠️|❌|
|Change CMT price|✅|✅|❌|
|Create DC|❌|✅|✅|
|Mark stages done|❌|✅|❌|

---

## Files Tab

The **Files** tab stores all documents attached to the order:

|File Type|Examples|
|---|---|
|Tech Packs|Buyer-provided garment specifications|
|Garment Images|Style reference photos|
|Approval Documents|Buyer sample approvals|
|Other Specs|Size charts, print artwork|

Files are uploaded via the Files tab and stored server-side, linked to the order by its ID. All roles can view files; only Admin and Manager can upload.