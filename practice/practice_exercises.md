# DAX Practice Exercises & Solutions

Based on the modules in your Masterclass slides, try to implement these formulas using the [Sample Dataset](sample_dataset.md).

## Phase 1: Aggregation & Syntax (Slide 04)

### 1. Total Sales
**Goal:** Create a measure to calculate the sum of total sales.
**Solution:**
```dax
Total Sales = SUMX(Sales, Sales[UnitPrice] * Sales[Quantity])
```

### 2. Average Order Value
**Goal:** Calculate the average amount per line item.
**Solution:**
```dax
Average Order Value = AVERAGE(Sales[UnitPrice])
```

### 3. Transaction Count
**Goal:** Count the total number of rows in the Sales table.
**Solution:**
```dax
Order Count = COUNTROWS(Sales)
```

---

## Phase 2: Logical functions (Slide 04)

### 4. Order Size Category (Calculated Column)
**Goal:** Return "Bulk" if Quantity > 5, else "Standard".
**Solution:**
```dax
Order Size = IF(Sales[Quantity] > 5, "Bulk", "Standard")
```

### 5. Regional Bonus
**Goal:** Use SWITCH to return a bonus percentage based on region.
**Solution:**
```dax
Regional Bonus = 
SWITCH(
    RELATED(Customers[Region]),
    "North", 0.05,
    "South", 0.03,
    0
)
```

---

## Phase 3: Text & Formatting (Slide 04)

### 6. Customer Display
**Goal:** Combine name and region: "Alice Smith (North)".
**Solution:**
```dax
Customer Label = Customers[CustomerName] & " (" & Customers[Region] & ")"
```

### 7. Price Label
**Goal:** Format UnitPrice as a currency string.
**Solution:**
```dax
Price Label = FORMAT(Sales[UnitPrice], "$#,##0")
```

---

## Phase 4: Date & Time (Slide 04/05)

### 8. Days Since Order
**Goal:** Calculate days since the order date.
**Solution:**
```dax
Days Since Order = DATEDIFF(Sales[OrderDate], TODAY(), DAY)
```

### 9. Month End Status
**Goal:** Find if an order was placed on the last day of the month.
**Solution:**
```dax
Is Month End = IF(Sales[OrderDate] = EOMONTH(Sales[OrderDate], 0), "Yes", "No")
```

---

## Phase 5: Advanced & Context (Slide 05/06)

### 10. Total Sales (All Regions)
**Goal:** Show total sales regardless of the region filter.
**Solution:**
```dax
Total Sales (All Regions) = CALCULATE([Total Sales], ALL(Customers[Region]))
```

### 11. Profit Margin
**Goal:** (Sales - Cost) / Sales. Handling zeros.
**Solution:**
```dax
Profit Margin = 
VAR TotalCost = SUMX(Sales, RELATED(Products[CostPrice]) * Sales[Quantity])
RETURN DIVIDE([Total Sales] - TotalCost, [Total Sales])
```
