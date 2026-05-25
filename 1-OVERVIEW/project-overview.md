# Project Overview — LEO Fashions

## What Is LEO Fashions?

LEO Fashions is a **garment manufacturing management system** — a web and mobile application that digitizes and manages the complete lifecycle of garment production. From the moment a customer places a clothing order to the final delivery of finished garments, every step is tracked, managed, and recorded in this system.

The platform is built for a garment manufacturing unit where customers place orders for clothing (t-shirts, pants, hoodies, etc.), and the factory manages buying raw materials, processing fabric, stitching garments, checking quality, packing, and delivering — all tracked in one place.

**Live URL:** `https://dev.activeeerp.in`

---

## The Problem It Solves

Before this system, garment factories managed everything manually:

|Problem|How Leo Fashions Solves It|
|---|---|
|Orders tracked on paper|Digital order management with full history|
|No visibility into production stages|8-stage tracking with real-time status|
|Material shortages discovered too late|PO and DC tracking with shortage alerts|
|Supplier payments missed|Bill management with due payment tracking|
|Worker salary calculated manually|Automated weekly wage calculation|
|No accountability for who did what|Full audit trail on every action|
|Multiple tools needed|Single platform for everything|

---

## Who Uses It

|Role|Who They Are|What They Do|
|---|---|---|
|**Admin**|Factory owner / manager|Approves everything, manages all modules|
|**User**|Customer / buyer|Places orders, tracks their order status|
|**Merchandiser**|Internal coordinator|Tracks stages, updates progress|
|**Department Staff**|Cutting, stitching workers|Updates their stage completion|

---

## Core Modules

|#|Module|Category|
|---|---|---|
|1|Dashboard|Overview|
|2|Orders|Core Production|
|3|Tasks|Task Management|
|4|Supplier Management|Supplier|
|5|PO & Bill Management|Procurement|
|6|Due Payments|Finance|
|7|Stock Management|Inventory|
|8|DC Management|Processing|
|9|Profit & Loss|Finance|
|10|Weekly Wages|HR|
|11|Approval Status|Workflow|
|12|Users|Admin|
|13|Audits|Admin|
|14|FAQ|Help|

---

## Key Business Concepts

**Bulk Order** — A large quantity production order. Example: 1000 t-shirts.

**Sample Order** — A trial piece to check quality before bulk production.

**CMT (Cut, Make, Trim)** — The cost charged per garment piece for stitching and assembly.

**DC (Delivery Challan)** — Official document when material is sent to a supplier for processing (knitting, dyeing, washing).

**PO (Purchase Order)** — Official document when factory buys raw materials (yarn, fabric, trims) from suppliers.

**Processing Loss** — Normal material loss during processing. Example: 20 Kg fabric sent, 19 Kg returned. 1 Kg is processing loss.

**Tolerance** — 3% extra pieces cut above order quantity to cover wastage. 100 pieces ordered = 103 pieces cut.

---

## Application Type

| Property     | Detail                                              |
| ------------ | --------------------------------------------------- |
| Type         | Web Application + Mobile Application                |
| Access       | Browser (desktop/laptop) + Mobile app (iOS/Android) |
| Users        | Multi-role (Admin and User)                         |
| Connectivity | Internet required                                   |
| Language     | English                                             |