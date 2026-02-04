# DAX Practice Exercises & Solutions

Based on the modules in your Masterclass slides, try to implement these formulas using the [Sample Dataset](sample_dataset.md).

## Phase 1: Aggregation & Syntax (Slide 04)

### 1. Total Sales (Measure)
**Goal:** Create a measure to calculate the sum of total sales.
**Solution:**
```dax
Total Sales = SUMX(Sales, Sales[UnitPrice] * Sales[Quantity])
```
**Visual Suggestion:** Card or Area Chart (Trend over time).

### 2. Average Order Value (Measure)
**Goal:** Calculate the average amount per line item.
**Solution:**
```dax
Average Order Value = AVERAGE(Sales[UnitPrice])
```
**Visual Suggestion:** Card or Gauge Chart.

### 3. Transaction Count (Measure)
**Goal:** Count the total number of rows in the Sales table.
**Solution:**
```dax
Order Count = COUNTROWS(Sales)
```
**Visual Suggestion:** Card or KPI Visual.

---

## Phase 2: Logical functions (Slide 04)

### 4. Order Size Category (Calculated Column)
**Goal:** Return "Bulk" if Quantity > 5, else "Standard".
**Solution:**
```dax
Order Size = IF(Sales[Quantity] > 5, "Bulk", "Standard")
```
**Visual Suggestion:** Pie Chart or Donut Chart (to show distribution of orders).

### 5. Regional Bonus (Calculated Column)
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
**Visual Suggestion:** Table or Bar Chart (Bonus by Region).

---

## Phase 3: Text & Formatting (Slide 04)

### 6. Customer Display (Calculated Column)
**Goal:** Combine name and region: "Alice Smith (North)".
**Solution:**
```dax
Customer Label = Customers[CustomerName] & " (" & Customers[Region] & ")"
```
**Visual Suggestion:** Table or Slicer.

### 7. Price Label (Calculated Column)
**Goal:** Format UnitPrice as a currency string.
**Solution:**
```dax
Price Label = FORMAT(Sales[UnitPrice], "$#,##0")
```
**Visual Suggestion:** Table or Matrix (for row-level details).

---

## Phase 4: Date & Time (Slide 04/05)

### 8. Days Since Order (Calculated Column)
**Goal:** Calculate days since the order date.
**Solution:**
```dax
Days Since Order = DATEDIFF(Sales[OrderDate], TODAY(), DAY)
```
**Visual Suggestion:** Scatter Chart or Histogram (to see aging distribution).

### 9. Month End Status (Calculated Column)
**Goal:** Find if an order was placed on the last day of the month.
**Solution:**
```dax
Is Month End = IF(Sales[OrderDate] = EOMONTH(Sales[OrderDate], 0), "Yes", "No")
```
**Visual Suggestion:** Slicer (to filter for specifically month-end orders).

---

## Phase 5: Advanced & Context (Slide 05/06)

### 10. Total Sales - All Regions (Measure)
**Goal:** Show total sales regardless of the region filter.
**Solution:**
```dax
Total Sales (All Regions) = CALCULATE([Total Sales], ALL(Customers[Region]))
```
**Visual Suggestion:** Combined with [Total Sales] in a Bar Chart to show % of total.

### 11. Profit Margin (Measure)
**Goal:** (Sales - Cost) / Sales. Handling zeros.
**Solution:**
```dax
Profit Margin = 
VAR TotalCost = SUMX(Sales, RELATED(Products[CostPrice]) * Sales[Quantity])

RETURN DIVIDE([Total Sales] - TotalCost, [Total Sales])
```
**Visual Suggestion:** Gauge or Line Chart (Month over Month Margin).
