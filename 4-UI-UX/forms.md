# UI Forms — LEO Fashions

## Every Form in the System

---

## Form 1 — Login

|Field|Type|Required|
|---|---|---|
|Username|Text|✅|
|Password|Password|✅|

---

## Form 2 — Create Order

**Sections:**

**Basic Info**

|Field|Type|Required|
|---|---|---|
|Name|Text|✅|
|Classification|Toggle (Bulk/Sample)|✅|
|Unit|Dropdown|✅|
|Style|Text|✅|
|Description|Textarea|❌|
|CMT Price|Number ₹|✅|
|Delivery Date|Date picker|✅|
|Shipment Date|Date picker|❌|

**Quantity**

|Field|Type|Required|
|---|---|---|
|Size selector|Multi-select|✅ (min 1)|
|Qty per size|Number|✅|

**Fabric**

|Field|Type|Required|
|---|---|---|
|Color|Text + color|✅|
|Fabric Weight|Number (Kg)|✅|
|Fabric GSM|Number|❌|
|Fabric Dia|Text|❌|
|Piece Weight|Number (g)|✅|
|Unit Price|Number ₹|✅|
|Due Date|Date|✅|
|15 process prices|Number ₹ each|❌|

**Yarn**

|Field|Type|Required|
|---|---|---|
|Yarn Required?|Toggle|✅|
|Yarn Type|Text|If enabled|
|Yarn Weight|Number (Kg)|If enabled|
|Unit Price|Number ₹|If enabled|
|4 process prices|Number ₹ each|❌|

**Trims**

|Field|Type|Required|
|---|---|---|
|Trim Type|Dropdown|✅|
|Unit Price|Number ₹|✅|
|Qty per size|Number|✅|
|Remarks|Text|❌|

**Other Prices (7 items)**

|Field|Type|Required|
|---|---|---|
|Unit Price|Number ₹|❌|
|Quantity|Number|❌|
|Remarks|Text|❌|

---

## Form 3 — Create Supplier

|Field|Type|Required|
|---|---|---|
|Supplier Name|Text|✅|
|Contact Number|Number|✅|
|Address|Textarea|✅|
|GST Number|Text|✅|
|PAN Number|Text|✅|
|Supplier Types|Multi-select|✅|
|Payment Terms|Number (days)|❌|
|State|Dropdown|✅|
|Bank Name|Text|❌|
|Account Number|Text|❌|
|Account Type|Dropdown|❌|
|IFSC Code|Text|❌|
|Account Holder Name|Text|❌|

---

## Form 4 — Create Purchase Order

|Field|Type|Required|
|---|---|---|
|Supplier|Dropdown|✅|
|Material Category|Dropdown|✅|
|Delivery Address|Textarea|✅|
|Order Number|Searchable dropdown|✅|
|Yarn Type|Text|✅|
|Color|Text|✅|
|Quantity|Number (Kg)|✅|
|Rate|Number ₹|✅|
|GST %|Number|✅|
|Description|Textarea|❌|

---

## Form 5 — Add PO Inward

|Field|Type|Required|
|---|---|---|
|Received Date|Date picker|✅|
|Received Quantity|Number (Kg)|✅|
|Remarks|Textarea|❌|

---

## Form 6 — Create DC

|Field|Type|Required|
|---|---|---|
|DC Date|Date picker|✅|
|Order Number|Dropdown|✅|
|Supplier From|Text/Dropdown|✅|
|Supplier To|Dropdown|✅|
|Department|Dropdown|✅|
|Process|Dropdown|✅|
|Quantity Sent|Number (Kg)|✅|

---

## Form 7 — Create Return DC

|Field|Type|Required|
|---|---|---|
|DC Date|Date picker|✅|
|Order Number|Dropdown|✅|
|Select DC|Dropdown|✅|
|From Supplier|Auto-filled|—|
|To Supplier|Dropdown|✅ (Other Supplier tab)|
|DC Remarks|Textarea|❌|
|Photo|Camera / Gallery|❌|

---

## Form 8 — Add DC Inward

|Field|Type|Required|
|---|---|---|
|Received Date|Date picker|✅|
|Received Quantity|Number (Kg)|✅|
|Remarks|Textarea|❌|

---

## Form 9 — Add Bill

|Field|Type|Required|
|---|---|---|
|Bill Date|Date picker|✅|
|Description|Text|✅|
|Quantity|Number|✅|
|Amount|Number ₹|✅|
|GST %|Number|✅|
|Bill Photo|File upload|❌|

---

## Form 10 — Update Stage

|Field|Type|Required|
|---|---|---|
|Job Type / Panel|Text|✅|
|Date|Date picker|✅|
|Quantity Type|Toggle (Partial/Full)|✅|
|Completed Qty (per size)|Number|✅|
|QR Count|Number|❌|
|Remarks|Textarea|❌|

---

## Form 11 — Create Task

|Field|Type|Required|
|---|---|---|
|Task Name|Text|✅|
|Assign To|Dropdown (users)|✅|
|Order Number|Dropdown|❌|
|Due Date|Date picker|✅|
|Description|Textarea|❌|

---

## Form 12 — Add Wage Advance

|Field|Type|Required|
|---|---|---|
|Worker Name|Text / Dropdown|✅|
|Advance Amount|Number ₹|✅|
|Advance Date|Date picker|✅|
|Remarks|Textarea|❌|