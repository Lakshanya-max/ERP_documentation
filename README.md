# LEO Fashions — Official Documentation

> **Version:** 1.0 **Last Updated:** May 2026 **Maintained By:** Leo Fashions Development Team

---

## 👋 Welcome

This is the complete technical and functional documentation for **LEO Fashions** — a garment manufacturing management system that handles everything from customer order placement to final delivery, including raw material purchasing, fabric processing, manufacturing stages, supplier management, billing, and worker wages.

Whether you are a **new developer joining the project**, a **business team member**, or an **external organization** evaluating the system — this documentation will give you a complete, clear understanding of how everything works.

---

## 📖 How to Read This Documentation

|You Are|Start Here|
|---|---|
|New developer joining the project|`1-OVERVIEW` → `5-ARCHITECTURE` → `2-DATABASE` → `7-MODULES`|
|Business / operations person|`1-OVERVIEW` → `3-BUSINESS-LOGIC` → `6-ROLES` → `7-MODULES`|
|UI/UX designer|`1-OVERVIEW` → `4-UI-UX` → `7-MODULES`|
|External organization evaluating|`1-OVERVIEW` → `6-ROLES` → `7-MODULES`|
|Taking over from someone who left|`README` → `1-OVERVIEW` → all sections in order|

---

## 📁 Documentation Structure

```
LEO-FASHION-DOCS/
│
├── README.md                        ← You are here
│
├── 1-OVERVIEW/
│   ├── project-overview.md          ← What is Leo Fashions
│   └── system-overview.md           ← How all modules connect
│
├── 2-DATABASE/
│   ├── db-overview.md               ← How data flows
│   └── db-schema.md                 ← All tables and fields
│
├── 3-BUSINESS-LOGIC/
│   ├── bl-overview.md               ← Core business rules
│   ├── bl-workflow.md               ← End to end workflow
│   └── bl-status-flow.md            ← All statuses explained
│
├── 4-UI-UX/
│   ├── ui-overview.md               ← Screen structure
│   ├── ui-flow.md                   ← How screens connect
│   ├── ui-forms.md                  ← All forms and fields
│   └── ui-screens.md                ← Every screen listed
│
├── 5-ARCHITECTURE/
│   ├── arch-overview.md             ← System design
│   ├── arch-flow.md                 ← Request to response flow
│   └── arch-security.md             ← Auth and security
│
├── 6-ROLES/
│   ├── admin-role.md                ← Everything Admin can do
│   └── user-role.md                 ← Everything User can do
│
├── 7-MODULES/
│   ├── orders/
│   │   ├── orders-overview.md       ← What orders module does
│   │   ├── orders-stages.md         ← 8 manufacturing stages
│   │   └── orders-flow.md           ← Complete order flow
│   ├── tasks/
│   │   ├── tasks-overview.md        ← What tasks module does
│   │   ├── tasks-types.md           ← My tasks, given, all
│   │   └── tasks-flow.md            ← Task assignment flow
│   ├── supplier-management/
│   │   ├── supplier-overview.md     ← Supplier records
│   │   ├── supplier-bills.md        ← Supplier billing
│   │   └── supplier-flow.md         ← Supplier lifecycle flow
│   ├── po-bill-management/
│   │   ├── po-overview.md           ← Purchase orders
│   │   ├── po-bills.md              ← PO billing
│   │   └── po-flow.md               ← PO lifecycle flow
│   ├── dc-management/
│   │   ├── dc-overview.md           ← Delivery challans
│   │   ├── dc-return.md             ← Return DC
│   │   └── dc-flow.md               ← DC lifecycle flow
│   └── weekly-wages/
│       ├── wages-overview.md        ← Wage calculation
│       ├── wages-advance.md         ← Advance payments
│       └── wages-flow.md            ← Wages flow
│
└── 8-FUTURE/
    └── future-enhancements.md       ← Planned improvements
```

---

## 🚀 Quick Module Reference

|Module|Purpose|
|---|---|
|Orders|Customer garment orders — bulk or sample|
|Tasks|Assign and track work tasks|
|Supplier Management|Manage all supplier records|
|PO & Bill Management|Purchase raw materials from suppliers|
|DC Management|Send materials for processing|
|Weekly Wages|Calculate and track worker salaries|
|Approval Status|Admin approval queue|
|Stock Management|Track material inventory|
|Due Payments|Pending supplier payments|
|Profit & Loss|Financial reports|
|Audits|System activity tracking|
|Users|User account management|

---

## 👥 User Roles

|Role|Access Level|
|---|---|
|**Admin**|Full access — approve, create, manage everything|
|**User**|Limited access — place orders, view own data|

See `6-ROLES/admin-role.md` and `6-ROLES/user-role.md` for complete details.

---

## ⚙️ Tech Stack

| Layer      | Technology                         |
| ---------- | ---------------------------------- |
| Frontend   | Web Application + Mobile App       |
| Backend    | REST API Server                    |
| Database   | Relational Database                |
| Auth       | Role-based session authentication  |
| Deployment | Cloud hosted — `dev.activeeerp.in` |