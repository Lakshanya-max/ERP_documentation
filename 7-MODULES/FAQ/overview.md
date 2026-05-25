## Purpose

This is the master FAQ document for the LEO garment manufacturing management system. It covers all user-facing questions organised by topic — from general usage to order management, production, tasks, and notifications.

---

## Table of Contents

1. [General FAQs](#1-general-faqs)
2. [Order Management FAQs](#2-order-management-faqs)
3. [Production FAQs](#3-production-faqs)
4. [Task FAQs](#4-task-faqs)
5. [Notification FAQs](#5-notification-faqs)

---

## 1. General FAQs

**Q: What is LEO?** LEO is an internal management system built for garment manufacturing businesses. It manages the full production lifecycle — from buyer orders and raw material procurement to factory tasks, dispatch, wages, payments, and profit reporting.

**Q: Who can use LEO?** Only registered accounts can log in. Accounts are created by the Admin. There is no self-registration. Two roles exist: **Admin** (full access) and **User** (restricted, personal data only).

**Q: What devices can I use LEO on?** LEO works on any device with a modern web browser — desktop, tablet, or mobile. No app installation is required.

**Q: What is the difference between Admin and User?**

|Feature|Admin|User|
|---|---|---|
|Create and approve orders|Yes|Submit only|
|Manage suppliers and POs|Yes|No|
|Assign tasks|Yes|View & update own tasks only|
|View all wages|Yes|View own wages only|
|Approve requests|Yes|No|
|View P&L reports|Yes|No|
|Access audit log|Yes|No|
|Manage user accounts|Yes|No|

**Q: I forgot my password. What do I do?** Contact your Admin. They will trigger a password reset and a new temporary password will be sent to your registered phone number.

**Q: Can two people share one login?** No. Each account is for one person. Shared logins are not supported and will cause incorrect audit records and wage calculations.

**Q: Is my data secure?** Yes. LEO uses role-based access control (users only see their own data), encrypted HTTPS connections, and a complete audit trail of every action.

**Q: What happens to my records if my account is deactivated?** All your historical records — tasks, wages, orders, requests — are preserved and remain visible to Admins. Deactivation only blocks your ability to log in. It is reversible.

**Q: The page is not loading. What do I do?** Try refreshing your browser. Check your internet connection. If the problem persists for more than a few minutes, contact your Admin or system support.

**Q: Can I use LEO without internet?** No. LEO currently requires an active internet connection for all operations. Offline mode is planned for a future release.

---

## 2. Order Management FAQs

**Q: How is an order created in LEO?** Go to Orders → New Order and fill in the buyer name, garment type, total pieces, and delivery date. Once submitted, the order goes to PENDING status and awaits Admin approval.

**Q: What are the order statuses and what do they mean?**

|Status|Meaning|
|---|---|
|Draft|Saved but not yet submitted for approval|
|Pending|Submitted, awaiting Admin review|
|Approved|Confirmed by Admin, ready for production|
|In Progress|Production tasks have started|
|Completed|All production stages done, ready for dispatch|
|Dispatched|Delivery Challan raised, goods sent to buyer|
|Cancelled|Order cancelled by Admin|

**Q: Can I edit an order after submitting it?** If the order is still in DRAFT, you can edit it freely. Once submitted (PENDING or beyond), only the Admin can make changes. Request the edit directly from your Admin.

**Q: My order was rejected. What should I do?** Check the rejection remark in Approval Status → My Requests. The Admin must provide a reason. Correct the issue and raise a new order.

**Q: Who can cancel an order?** Only Admins can cancel orders. If you need an order cancelled, contact your Admin with the reason.

**Q: How do I know when my order is approved?** You will receive an in-app notification. You can also check Orders → My Orders at any time to see the current status.

**Q: Can one order have multiple delivery challans?** Yes. A large order can be dispatched in multiple batches, each with its own DC. All DCs are linked back to the original order.

**Q: What is the order reference number?** It is a unique auto-generated ID assigned to every order when it is created (e.g. ORD-2025-0042). Use this number when communicating with your Admin about a specific order.

**Q: How long does order approval usually take?** That depends on the Admin's availability. There is no system-enforced SLA, but Admins receive a notification immediately when a new order is submitted.

**Q: Can I see orders from other workers or other buyers?** Users can only see orders they submitted. Admins can see all orders across all buyers and users.

---

## 3. Production FAQs

**Q: What are the production stages in LEO?** LEO tracks garment production through the following stages, each managed as a Task:

|Stage|Description|
|---|---|
|Cutting|Fabric cut as per design and size specifications|
|Stitching|Pieces stitched together by tailors|
|Finishing|Buttons, zips, labels, ironing applied|
|Quality Check (QC)|Garments inspected for defects|
|Packing|Garments packed and labelled for dispatch|

**Q: Who decides which worker handles which stage?** The Admin assigns tasks per stage to specific workers. Workers do not self-assign.

**Q: What happens after all production stages are complete?** Once all tasks are marked complete and approved by the Admin, the order status changes to COMPLETED. The Admin then creates a Delivery Challan (DC) and dispatches the goods to the buyer.

**Q: What is a Delivery Challan (DC)?** A DC is a dispatch document that records: the order it is linked to, the number of pieces dispatched, the delivery vehicle or courier, and the dispatch date. It serves as proof of delivery and is used to track returns.

**Q: What happens if a buyer returns garments?** A DC Return Request is raised (by User or Admin). Admin reviews and processes the return. Returned pieces are added back to stock automatically.

**Q: How is stock updated during production?** Stock is updated in three ways:

- Automatically when a supplier bill is approved (material received).
- Automatically when a DC return is processed (returned pieces back in stock).
- Manually by the Admin when a correction is needed (always logged in Audits).

**Q: What if fabric or material is not available for production to begin?** The Admin will create a Purchase Order (PO) with the relevant supplier to procure the required material. Production tasks will be assigned once material is in stock.

**Q: Can I see the stock levels?** Stock visibility is Admin-only. If you need to know whether material is available for a job, check with your Admin.

**Q: What is the difference between a completed order and a dispatched order?** A Completed order means all production is done — the garments are ready in the factory. A Dispatched order means the DC has been raised and the goods have physically left the factory for the buyer.

---

## 4. Task FAQs

**Q: How do I know a task has been assigned to me?** You will receive an in-app notification. The task also appears in Tasks → My Tasks with a status of ASSIGNED.

**Q: What information does a task contain?** Each task shows:

- Task type (Cutting / Stitching / Finishing / QC / Packing)
- Linked order reference
- Due date
- Special instructions from the Admin
- Current status

**Q: How do I update my task progress?** Open the task from My Tasks and click Mark In Progress when you start. When the work is done, click Mark Done and add a completion note if required.

**Q: What happens after I mark a task as done?** The task enters PENDING REVIEW status. The Admin reviews the completed task.

- If accepted — task is marked COMPLETED.
- If not acceptable — task is returned as REWORK with a remark explaining what needs to be fixed.

**Q: A task was sent back to me for rework. What do I do?** Read the Admin's remark carefully. Fix the issue, then click Mark Done again to re-submit for review.

**Q: Can I reassign a task to another worker?** No. Only Admins can reassign tasks. If a task has been assigned to you incorrectly, inform your Admin.

**Q: What if I cannot complete a task by the due date?** Inform your Admin immediately. They may extend the due date, reassign the task, or reprioritise other tasks. There is no automatic penalty in the system — the Admin manages escalation.

**Q: Can I see tasks assigned to my colleagues?** No. Users can only see their own assigned tasks. Admins can see all tasks across all workers and orders.

**Q: How many tasks can I have at one time?** There is no system limit. The Admin controls how many tasks they assign to each worker.

**Q: Do tasks affect my wages?** Indirectly, yes. Completed tasks contribute to the piece count that the Admin uses to calculate your weekly wage. Uncompleted or reworked tasks may reduce your recorded output.

---

## 5. Notification FAQs

**Q: Where do I see my notifications?** Tap or click the bell icon in the top navigation bar. A red badge shows the count of unread notifications.

**Q: What events trigger a notification for me as a User?**

|Event|Notification Sent To|
|---|---|
|New task assigned to me|Me (User)|
|My task sent back for rework|Me (User)|
|My task approved as completed|Me (User)|
|My order approved or rejected|Me (User)|
|My wage advance approved or rejected|Me (User)|
|My weekly wages marked as paid|Me (User)|
|My DC return request processed|Me (User)|

**Q: What events trigger a notification for the Admin?**

|Event|Notification Sent To|
|---|---|
|New order submitted by a User|Admin|
|New wage advance requested|Admin|
|New DC return request raised|Admin|
|New item enters the approval queue|Admin|
|Low stock threshold reached|Admin|

**Q: Can I turn off notifications?** Notification preferences are set by the Admin at the system level. Individual notification opt-out is not currently available.

**Q: I received a notification but the linked record is not loading. What do I do?** Try refreshing the page. If the issue persists, the record may have been deleted or your access may not include that item. Contact your Admin.

**Q: Are notifications sent via SMS or WhatsApp as well?** Currently, notifications are in-app only. SMS and WhatsApp notification integration is planned as a future enhancement.

**Q: How long do notifications stay in my list?** Notifications are retained for 30 days, after which they are automatically cleared.

**Q: What does it mean when the bell icon shows no new notifications?** It means there are no unread notifications at the moment. All previous notifications have been viewed or cleared.

---

## Related Documents

- Overall Workflow
- Admin Flow
- User Flow
- Approval Overview
- UI Overview