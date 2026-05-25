# Architecture Security — LEO Fashions

## Authentication

```
User enters username + password
        ↓
POST /api/auth/login
        ↓
Server validates credentials
        ↓
Server generates session token
        ↓
Token stored on device (cookie/storage)
        ↓
Every API request includes token in header
        ↓
Server verifies token on every request
```

---

## Role-Based Access Control (RBAC)

Every API endpoint enforces role checks:

```
Request arrives at API
        ↓
Extract user role from token
        ↓
Check permission:
├── Admin  → Full access to all endpoints
└── User   → Access to own data only
        ↓
Unauthorized → 403 Forbidden response
Authorized   → Process request
```

---

## Data Isolation

|Role|Data Access Rule|
|---|---|
|Admin|All records, all users, all orders|
|User|Only records where `created_by = self`|
|Staff|Only assigned stage updates|

---

## What Is Protected

|Resource|Protection|
|---|---|
|All API endpoints|Auth token required|
|Admin modules|Role = Admin required|
|Other user's orders|Blocked for User role|
|Approval actions|Admin role only|
|Supplier management|Admin role only|
|Financial data|Admin role only|
|User management|Admin role only|

---

## Audit Security

Every data change records:

- `created_by` — who created
- `updated_by` — who last changed
- `created_on` / `updated_on` — exact timestamps

This creates a **tamper-evident audit trail** for all records.

---

## Communication Security

- All data transmitted over **HTTPS**
- No sensitive data in URL parameters
- File uploads (bill photos) stored securely in cloud storage