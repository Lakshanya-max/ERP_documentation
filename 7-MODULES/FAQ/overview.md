## Purpose

This document answers the most frequently asked questions about using the LEO garment manufacturing management platform, covering both Admin and User concerns.

---

## General

**Q: What is LEO?** LEO is an internal management system for a garment manufacturing business. It handles orders, supplier management, purchase orders, delivery challans, stock, wages, payments, profit & loss reporting, and user administration — all in one platform.

**Q: Who can access LEO?** Only registered users with an account created by an Admin. There is no self-registration.

**Q: What devices can I use LEO on?** LEO works on desktops, tablets, and mobile phones via a web browser. No app installation is required.

**Q: What happens if I forget my password?** Contact your Admin. They can trigger a password reset that sends a new temporary password to your registered phone number.

---

## Orders

**Q: How do I raise a new order?** Go to **Orders → New Order**, fill in the buyer name, garment type, piece count, and delivery date, then submit. The order enters PENDING status until Admin approves it.

**Q: Can I edit an order after submitting it?** Orders in PENDING or APPROVED status can be edited only by an Admin. If you need a change, raise the request with your Admin.

**Q: What does each order status mean?**

|Status|Meaning|
|---|---|
|Draft|Saved but not submitted|
|Pending|Submitted, awaiting admin approval|
|Approved|Confirmed and in production|
|In Progress|Production underway|
|Completed|Production done, ready for dispatch|
|Cancelled|Order cancelled by Admin|

---

## Tasks

**Q: Who assigns tasks to me?** Admins assign tasks. You will receive an in-app notification when a task is assigned to you.

**Q: How do I mark a task as done?** Open the task from **Tasks → My Tasks**, click **Mark Complete**, and add a completion note if required.

**Q: Can I reassign a task to someone else?** Only Admins can reassign tasks. Contact your Admin if a task has been assigned to the wrong person.

---

## Suppliers & Purchase Orders

**Q: Who can add a new supplier?** Only Admins can add, edit, or deactivate suppliers.

**Q: How does a Purchase Order get created?** Admin creates a PO against a supplier, specifying item, quantity, and price. The PO is then approved internally before the order is placed with the supplier.

**Q: Can I attach a bill to a PO?** Yes. Admins can attach scanned bill documents (PDF or image, max 5 MB) to any PO record.

---

## Wages

**Q: When are wages calculated?** Wages are calculated on a weekly basis. The Admin enters the week's production data and the system computes the payable amount based on the worker's rate.

**Q: How do I request a wage advance?** Go to **Wages → Request Advance**, enter the amount and reason, and select your repayment period. The request goes to Admin for approval.

**Q: How is my advance deducted?** Once approved, the advance amount is split equally across your selected repayment weeks and deducted from your net wages automatically.

**Q: Can I have two advances at the same time?** No. You must fully repay your current advance before a new request can be raised.

---

## Approvals

**Q: How do I know if my request was approved or rejected?** You will receive an in-app notification. You can also check **Approval Status → My Requests** to see the current status and any Admin remark.

**Q: Why was my request rejected?** The Admin is required to provide a remark when rejecting. You can see this remark in the Approval Status module under your request detail.

**Q: Can I re-submit a rejected request?** Yes. Correct any issues based on the Admin's remark and raise a new request.

---

## Stock

**Q: Who can adjust stock levels?** Only Admins can perform manual stock adjustments. All adjustments are logged in the Audits module.

**Q: Where do I see current stock levels?** Go to **Stock Management → Stock Overview**. You can filter by material type, garment type, or location.

---

## Due Payments

**Q: What is a due payment?** A due payment is an outstanding amount owed to a supplier or worker that has not yet been settled.

**Q: How are due payments created?** They are automatically created when a bill is approved but not yet paid, or when a wage is marked as pending payment.

**Q: How do I mark a payment as settled?** Admin can go to **Due Payments**, select the record, and click **Mark as Paid** or **Partial Payment**.

---

## Audits

**Q: Can I see the audit log?** The Audit log is accessible to Admins only. If you need to verify a specific action, contact your Admin.

**Q: How long are audit records kept?** Audit logs are retained for a minimum of 2 years.

---

## Technical

**Q: The page is not loading. What should I do?** Try refreshing the browser. If the issue persists, check your internet connection. If it continues, contact your system administrator.

**Q: Can two people log in with the same account?** No. Each user account is for one person. Shared logins are not supported and can cause data integrity issues.

**Q: Is my data secure?** Yes. LEO uses role-based access control, encrypted connections (HTTPS), and a full audit trail. Only Admins can access sensitive financial and user data.

---

## Related Documents

- UI Overview
- Admin Role
- User Role
- Approval Overview