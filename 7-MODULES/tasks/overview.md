# Tasks — Overview

## What Is the Tasks Module?

The Tasks module allows Admin to **assign work to team members** and track whether those tasks are completed. Tasks can be created automatically by the system when an order stage begins, or manually by the Admin for any custom work.

---

## Task Types

|Type|How Created|Prefix|
|---|---|---|
|**Auto Task**|System creates when order stage triggers|`[Auto]`|
|**Manual Task**|Admin creates directly|No prefix|

---

## Task Structure

```
Each Task Contains:
├── Task Name       → Description of work
├── Task ID         → Auto-generated reference
├── Order Link      → Linked order (if any)
├── Assigned By     → Always Admin
├── Assigned To     → Specific team member
├── Due Date        → When task must be done
└── Status          → Pending / Completed
```

---

## Task Views — 3 Tabs

|Tab|Who Sees It|What It Shows|
|---|---|---|
|**My Tasks**|Logged-in user|Tasks assigned TO this person|
|**Given Tasks**|Admin|Tasks Admin has assigned to others|
|**All**|Admin|Every task in the system|

---

## Task Filters

|Filter|Options|
|---|---|
|Status|All / Completed / Pending|
|Search|By task name or order number|

---

## Auto Task Logic

When an order is approved and stages are created:

```
Order approved
        ↓
System creates [Auto] tasks
for each relevant stage/panel
        ↓
Admin → Staff member assigned
        ↓
Staff sees task in My Tasks
```

**Example Auto Task:**

```
[Auto] #LEO-2026-019 - testtask - a
Admin → Gowri
Order# LEO-2026-019
28 Feb, 2026
```

---

## Task Status

|Status|Meaning|
|---|---|
|`Pending`|Task assigned, not yet done|
|`Completed`|Task finished by assignee|

---

## Key Rules

- Tasks can be assigned to **multiple people** for the same order
- Same task can appear multiple times if assigned to different staff
- Admin can view ALL tasks across all users
- Users see ONLY tasks assigned to them
- Auto tasks are prefixed with `[Auto]`
- Tasks without an order link are standalone manual tasks