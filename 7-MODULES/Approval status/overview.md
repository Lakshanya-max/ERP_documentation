## Purpose

This document describes the Approval Status module — a centralised hub where all approval-required actions across LEO are tracked, reviewed, and actioned by Admins, and monitored by Users.

---

## Overview

Many operations in LEO require explicit Admin approval before they take effect. Rather than approvals being buried inside individual modules, the Approval Status module provides a **single queue** where all pending, approved, and rejected items are visible in one place.

---

## Modules That Trigger Approvals

|Module|Action Requiring Approval|
|---|---|
|Orders|New order submission|
|Purchase Orders|PO creation above threshold|
|Supplier Bills|Bill submission for payment|
|DC Returns|Return request raised by user|
|Wage Advance|Advance payment request|
|Due Payments|Payment settlement request|
|Stock Adjustment|Manual stock correction|

---

## Approval Flow

```
User / System creates a record
        │
        └── Record Status = PENDING
                │
                └── Appears in Admin's Approval Queue
                            │
                            ├── Admin: APPROVE
                            │       └── Status = APPROVED
                            │               └── Action executed in originating module
                            │
                            └── Admin: REJECT
                                    └── Status = REJECTED
                                            └── Remark stored and shown to User
```

---

## Admin — Approval Queue View

The queue displays all pending items across all modules in one table:

|Column|Description|
|---|---|
|Request ID|Unique reference for the approval item|
|Module|Which module raised the request (Orders, PO, Wages, etc.)|
|Raised By|Name of the user who submitted the request|
|Date Raised|Timestamp of submission|
|Summary|Brief description of what is being approved|
|Status|PENDING / APPROVED / REJECTED|
|Action|Approve or Reject button|

**Filters available:**

- By module
- By date range
- By user
- By status (Pending / Approved / Rejected)

---

## Admin — Approval Detail View

Clicking any item opens the full detail view, which shows:

- Complete record details from the originating module.
- Attachments (if any, e.g. bill scans, DC documents).
- History of previous approval actions on the same record.
- Remark field — mandatory when rejecting.

---

## User — Approval Status View

Users see only their own submitted items:

|Column|Description|
|---|---|
|Request ID|Reference ID|
|Module|Type of request|
|Date Submitted|When they submitted it|
|Status|PENDING / APPROVED / REJECTED|
|Admin Remark|Shown if rejected|

Users cannot action approvals — view only.

---

## Approval Status Reference

|Status|Colour|Meaning|
|---|---|---|
|PENDING|Amber|Awaiting admin review|
|APPROVED|Green|Admin approved; action is live|
|REJECTED|Red|Admin rejected; remark explains reason|

---

## Notifications

- User receives an **in-app notification** when their request is approved or rejected.
- Admin receives a notification when a new item enters the queue.
- Notifications are accessible via the bell icon in the top navigation bar.

---

## Rules

- Admin must provide a remark when rejecting any request.
- An approved record cannot be un-approved directly — a new corrective record must be raised.
- All approval actions are logged in the Audit module with timestamp and Admin identity.

---

## Related Documents

- Admin Role
- User Role
- Audits Overview
- Orders Overview