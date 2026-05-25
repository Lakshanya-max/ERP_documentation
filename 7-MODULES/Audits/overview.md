## Purpose

This document describes the Audits module — the system-wide activity log that records every significant action performed within LEO, providing full traceability for operations, approvals, and data changes in the garment manufacturing workflow.

---

## Overview

The Audits module is a **read-only** log accessible only to Admins. Every time a user or the system creates, updates, approves, rejects, or deletes a record anywhere in LEO, an audit entry is automatically written. This ensures accountability, supports dispute resolution, and enables operational review.

---

## What Gets Logged

|Module|Actions Logged|
|---|---|
|Orders|Created, Updated, Approved, Rejected, Closed|
|Tasks|Created, Assigned, Updated, Completed|
|Suppliers|Created, Updated, Deactivated|
|Purchase Orders|Created, Approved, Rejected, Linked to Bill|
|Bills|Submitted, Approved, Paid, Disputed|
|DC Management|DC Created, Return Raised, Return Processed|
|Due Payments|Payment Recorded, Marked Paid, Partial Payment|
|Stock|Adjusted, Exported|
|Profit & Loss|Report Generated, Period Viewed|
|Weekly Wages|Wage Entry Created, Marked Paid|
|Wage Advance|Requested, Approved, Rejected, Recovered|
|Approval Status|Any Approval or Rejection action|
|Users|Created, Edited, Deactivated, Password Reset|
|Login / Auth|Login, Logout, Failed Login Attempts|

---

## Audit Log Entry Fields

Each audit record captures the following:

|Field|Description|
|---|---|
|Log ID|Unique auto-generated identifier|
|Timestamp|Date and time of the action (IST)|
|User|Name and role of the person who performed the action|
|Module|Which module the action occurred in|
|Action|Type of action (Created / Updated / Approved / Rejected / Deleted)|
|Record Reference|ID or reference of the affected record|
|Summary|Human-readable description of what changed|
|Previous Value|The value before the change (for updates)|
|New Value|The value after the change (for updates)|
|IP Address|Device IP at the time of the action|

---

## Admin — Audit Log View

### List View

Displays all audit entries in reverse chronological order (newest first).

**Filters available:**

- By module
- By action type (Created / Updated / Approved / Rejected / Deleted)
- By user
- By date range
- By record reference (search by Order ID, PO number, etc.)

### Detail View

Clicking any log entry opens the full audit detail, showing:

- Complete before/after values for any field that changed.
- Link to the original record in its module (if the record still exists).

---

## Export

- Admins can export the filtered audit log as a **CSV file**.
- Export is date-range limited (max 90 days per export) to keep file sizes manageable.

---

## Retention Policy

- Audit logs are retained for a minimum of **2 years**.
- Logs cannot be edited or deleted by anyone — including Admins.
- The system stores logs separately from operational data for integrity.

---

## Rules & Access

- The Audits module is **Admin-only**. Users have no access.
- Audit records are **immutable** — no edit or delete is possible on any log entry.
- System-generated actions (auto-deductions, scheduled reports) are logged under the `SYSTEM` user.

---

## Common Use Cases

|Scenario|How to Use Audits|
|---|---|
|Worker disputes a wage deduction|Filter by Wages module + worker name + date|
|Investigate who approved a PO|Filter by PO module + Approved action + date|
|Check if a DC was processed|Search by DC reference number|
|Review all actions by a specific user|Filter by user name|
|Monthly compliance review|Export logs for the calendar month|

---

## Related Documents

- Admin Role
- Approval Overview
- Users Overview