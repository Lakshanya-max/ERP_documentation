# DC Management — Return DC

## What Is Return DC?

Return DC manages the return of goods when a product is **damaged or the customer is not satisfied**. The returned product is either sent to another supplier for redesign or stored in the warehouse as stock.

---

## Return DC Types

| Tab                | What Happens                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------- |
| **Other Supplier** | Returned product sent to another customer/supplier who wants to redesign it for their needs |
| **Stock**          | Returned product stored in warehouse for future use                                         |

---

## Return DC Form Fields

### Basic Information

|Field|Required|Note|
|---|---|---|
|DC Date|✅|Auto-filled with today's date|
|Order Number|✅|Select which order this return is for|
|Select DC|✅|Loads items from original DC for return|
|From Supplier|Auto-filled|Pulled from selected DC automatically|
|To Supplier|✅ (Other tab)|Where returned goods go next|

### Additional Information

|Field|Required|
|---|---|
|DC Remarks|❌ Optional|

### Photo

|Option|Description|
|---|---|
|Camera|Take live photo of returned goods|
|Gallery|Upload from device|

---

## Smart Field Logic

```
Step 1: Select Order Number
            ↓
        DC dropdown populates
            ↓
Step 2: Select DC
            ↓
        From Supplier auto-fills
        (no manual entry needed)
            ↓
Step 3: Select To Supplier
        (Other Supplier tab only)
```

---

## Return DC vs Regular DC

||Regular DC|Return DC|
|---|---|---|
|Direction|Factory → Supplier|Supplier/Customer → Factory|
|Purpose|Send for processing|Handle returned goods|
|Result|Processed goods return|Goes to another supplier or stock|
|Bill|Processing charge|Not applicable|
|Created by|Admin|Admin|

---

## Stock Tab vs Other Supplier Tab

### Other Supplier Tab

```
Returned goods arrive at factory
        ↓
Return DC (Other Supplier) created
        ↓
Goods sent to new customer/supplier
        ↓
New customer redesigns the product
        ↓
Product delivered to new customer
```

### Stock Tab

```
Returned goods arrive at factory
        ↓
Return DC (Stock) created
        ↓
Goods stored in warehouse
        ↓
Available as stock for future orders
        ↓
Used when similar order comes in
```