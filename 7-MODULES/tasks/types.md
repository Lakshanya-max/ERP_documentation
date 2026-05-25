# Tasks — Types and Examples

## Auto Tasks

Auto tasks are **system-generated** when order stages are triggered. They are prefixed with `[Auto]` and always linked to an order.

**Format:**

```
[Auto] #ORDER_ID - task_name - style
Admin → assigned_person
Order# ORDER_ID
Date
```

**Real Examples from System:**

```
[Auto] #LEO-2026-019 - testtask - a
Admin → Gowri | Order# LEO-2026-019 | 28 Feb 2026

[Auto] #LEO-2026-019 - testtask - a
Admin → acc   | Order# LEO-2026-019 | 17 Feb 2026

[Auto] #LEO-2026-011 - ok - m
Admin → Muthuraj | Order# LEO-2026-011 | 24 Feb 2026

[Auto] #LEO-2026-018 - test - M
Admin → CHANDRIKA | Order# LEO-2026-018 | 21 Feb 2026
```

**Note:** Same task can be assigned to multiple people. Each appears as a separate task card.

---

## Manual Tasks

Manual tasks are **created directly by Admin** for any work not tied to an automatic trigger.

**Real Examples from System:**

```
Skip 1week
Admin → acc | 30 Jan 2026

Gvjj
Admin → acc | 31 Jan 2026

Resubmission of Exist PP based on PP comments
Admin → (unassigned) | 29 Nov 2025

Rope dyeing for exist pants
Admin → (unassigned) | 18 Nov 2025

Exists 15195 all colours inspection plan
Admin → (unassigned) | 12 Nov 2025

Leo 69, 1st delivery 750 pcs, 2nd delivery 750 pcs,
I need accountability for pvs
Admin → (unassigned) | 12 Nov 2025
```

---

## Task With Order Link

Tasks that are linked to specific orders:

```
#LEO-2026-008 - name - M, Fabric: GREEN
Admin → Chinnaya | Order# LEO-2026-008 | 20 Jan 2026

#LEO-2026-008 - name - M, Fabric: GREEN
Admin → acc | Order# LEO-2026-008 | 20 Jan 2026
```

---

## Task Assignment — One to Many

The same task can be assigned to multiple team members:

```
Task: [Auto] #LEO-2026-011 - ok - m
├── Admin → Muthuraj  (24 Feb 2026)
├── Admin → Angel     (24 Feb 2026)
└── Admin → Gowri     (24 Feb 2026)
```

Each person gets their own task card in their **My Tasks** view.