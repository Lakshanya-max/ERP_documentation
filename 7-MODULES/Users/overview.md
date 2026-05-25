## Purpose

This document covers the Users module — the admin-controlled area for creating, managing, and deactivating user accounts within the LEO garment manufacturing platform.

---

## Overview

Every person who accesses LEO must have a registered user account. Accounts are created exclusively by Admins. There is no public self-registration. The Users module gives Admins full visibility and control over who can access the system, what role they hold, and whether they are currently active.

---

## User Roles

LEO supports two roles:

|Role|Description|
|---|---|
|**Admin**|Full access to all modules, approvals, reports, and user management|
|**User**|Restricted access — can raise requests, view own records, and track status|

> See Admin Role and User Role for a full permission matrix.

---

## User Record Fields

|Field|Description|
|---|---|
|Full Name|Worker or staff member's full name|
|Phone Number|Primary login identifier|
|Email Address|Optional; used for notifications|
|Role|Admin or User|
|Department|Production / Cutting / Finishing / Accounts / Logistics|
|Date Joined|Account creation date|
|Status|Active / Inactive|
|Weekly Wage Rate (₹)|Base rate used by the Wages module|

---

## Admin Actions

### Create User

1. Go to **Users → Add New User**.
2. Fill in name, phone, role, and department.
3. Set the initial wage rate if the worker is on the factory floor.
4. Submit — the user receives an SMS/notification with their login credentials.

### Edit User

- Update name, phone, department, or wage rate.
- Role changes require re-login on the user's device to take effect.

### Deactivate User

- Deactivated users **cannot log in**.
- Their historical records (orders, wages, DCs) are **preserved** and remain visible to Admins.
- Deactivation is reversible — Admin can reactivate at any time.

### Reset Password

- Admin can trigger a password reset, which sends a new temporary password to the user's phone.

---

## User List View

The user list shows all registered accounts with the following columns:

|Column|Description|
|---|---|
|Name|Full name|
|Phone|Login phone number|
|Role|Admin / User|
|Department|Assigned department|
|Status|Active / Inactive badge|
|Actions|Edit / Deactivate / Reset Password|

**Filters available:**

- By role (Admin / User)
- By department
- By status (Active / Inactive)
- Search by name or phone

---

## User Detail View

Clicking a user opens their profile, which shows:

- Personal and role information.
- Wage history (linked from Wages module).
- Advance history (linked from Wages Advance).
- Approval submissions history.
- Last login timestamp.

---

## Security Rules

- Only **Admins** can create, edit, or deactivate users.
- An Admin cannot deactivate their own account.
- There must always be at least **one active Admin** in the system.
- Phone numbers must be unique — duplicates are rejected at creation.
- All user management actions are logged in the Audit module.

---

## Status Reference

|Status|Meaning|
|---|---|
|Active|User can log in and use the system|
|Inactive|Account suspended; login blocked|

---

## Related Documents

- Admin Role
- User Role
- Weekly Wages Overview
- Audits Overview