# Future Enhancements — LEO Fashions

## Overview

This document outlines potential improvements, planned features, and suggestions for making LEO Fashions more powerful, scalable, and user-friendly as the business grows.

---

## 1. Notifications & Alerts

**Current State:** Admin manually checks Approval Status for pending items.

**Enhancement:**

- Push notifications on mobile when a new order/PO/DC is submitted
- Email alerts for overdue payments
- SMS alerts when order stage is completed
- In-app notification bell with real-time updates

**Benefit:** Admin never misses critical actions.

---

## 2. Dashboard Analytics

**Current State:** Dashboard shows basic navigation.

**Enhancement:**

- Order completion rate chart (weekly/monthly)
- Material shortage alerts widget
- Top suppliers by volume
- Revenue vs cost trend graph
- Active orders by stage (funnel view)
- Worker productivity chart per panel

**Benefit:** Management decisions backed by real-time data.

---

## 3. QR Code Full Integration

**Current State:** QR count is tracked per stage.

**Enhancement:**

- Workers scan QR codes on garment pieces using mobile camera
- Each piece tracked from cutting → finishing → packing
- Lost or defective pieces immediately visible
- Full piece-level traceability

**Benefit:** Zero manual counting errors, full accountability per piece.

---

## 4. Customer Portal

**Current State:** Users place orders and track status via the main app.

**Enhancement:**

- Dedicated customer-facing portal (separate from factory UI)
- Customer tracks order progress visually (stage pipeline view)
- Customer uploads design files and references
- Customer approves samples digitally before bulk production
- Order history and invoices downloadable by customer

**Benefit:** Professional customer experience, reduced back-and-forth communication.

---

## 5. Automated Costing & Quotation

**Current State:** CMT price and fabric costs entered manually.

**Enhancement:**

- Auto-calculate order cost estimate based on:
    - Fabric GSM + weight + process costs
    - Yarn type + process costs
    - Trim costs
    - CMT rate
- Generate and share quotation PDF with customer before order confirmation

**Benefit:** Faster quoting, fewer pricing errors.

---

## 6. Inventory Forecasting

**Current State:** Stock management tracks current stock.

**Enhancement:**

- Predict when yarn/fabric will run out based on active orders
- Auto-suggest PO creation when stock falls below threshold
- Color-coded alerts: Green (sufficient), Yellow (low), Red (critical)

**Benefit:** Prevents production delays due to material shortage.

---

## 7. Multi-Unit Management

**Current State:** Orders assigned to units (Main Unit, Leo-unit-2).

**Enhancement:**

- Separate dashboards per unit
- Unit-wise P&L reports
- Inter-unit material transfer tracking
- Unit-wise supplier and staff management

**Benefit:** Scalable to multiple factory locations.

---

## 8. Payroll Integration

**Current State:** Weekly wages calculated, PDF downloaded manually.

**Enhancement:**

- Direct integration with bank payment systems
- Payslip auto-generated and sent to worker mobile
- Monthly salary summary with PF/ESI deductions
- Leave management integrated with wage calculation

**Benefit:** Full automated payroll, no manual bank transfers.

---

## 9. Document Management

**Current State:** Bill photos uploaded individually.

**Enhancement:**

- Centralized document storage per order
- Upload design files, tech packs, buyer specs to order
- Version control for design changes
- Documents accessible to relevant team members only

**Benefit:** All order-related files in one place, no email hunting.

---

## 10. Audit & Compliance Reports

**Current State:** Audit module tracks changes.

**Enhancement:**

- Auto-generate compliance reports for buyer audits
- Social compliance checklist (worker hours, wages, safety)
- Export audit trail as PDF for buyer verification
- Scheduled audit report emails to management

**Benefit:** Ready for buyer factory audits at any time.

---

## 11. Offline Mode (Mobile)

**Current State:** Mobile app requires internet connection.

**Enhancement:**

- Stage updates possible without internet
- Data syncs automatically when connection restored
- Critical for factory floor where WiFi may be weak

**Benefit:** No work interruption due to connectivity issues.

---

## 12. Role Expansion

**Current State:** Two roles — Admin and User.

**Enhancement:**

- **Merchandiser role** — track stages, cannot approve
- **Accounts role** — manage bills and payments only
- **Store Manager role** — manage stock and trims only
- **Quality Manager role** — manage quality stage only
- Custom permission sets per role

**Benefit:** Better access control, each person sees only what they need.

---

## Known Limitations (Current Version)

|Limitation|Impact|Suggested Fix|
|---|---|---|
|No real-time notifications|Admin must manually check approval queue|Push notification system|
|Manual QR counting|Human error possible|Full QR scan integration|
|No offline mode|Factory floor usage limited|Progressive Web App (PWA)|
|Basic dashboard|No data insights|Analytics dashboard|
|Two roles only|Limited access control|Expanded role system|
|Manual payroll|Weekly PDF, manual payment|Payroll integration|