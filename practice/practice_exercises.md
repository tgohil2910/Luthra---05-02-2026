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

### 11. Gross Profit Margin (Measure)
**Goal:** (Sales - Cost) / Sales. Handling zeros.
**Solution:**
```dax
Gross Profit Margin = 
VAR TotalCost = SUMX(Sales, RELATED(Products[CostPrice]) * Sales[Quantity])
RETURN DIVIDE([Total Sales] - TotalCost, [Total Sales], 0)
```
**Visual Suggestion:** Gauge or Line Chart (Month over Month Margin).

---

# Step-by-Step Dashboard Building Guide

Follow these steps to build a professional-grade Sales Dashboard using all the DAX formulas practiced above.

## Phase 1: Data Preparation & Modeling
1. **Load Data:** Import the three CSV files (`Sales.csv`, `Products.csv`, `Customers.csv`) into Power BI Desktop using "Get Data".
2. **Setup Relationships:** Go to the **Model View** and ensure the following connections are active:
   * **Sales[ProductID]** → **Products[ProductID]** (Many-to-One)
   * **Sales[CustomerID]** → **Customers[CustomerID]** (Many-to-One)
3. **Hide IDs:** Right-click the ID columns in the Model view and select "Hide in Report View" to keep your fields list clean.

## Phase 2: Logic Implementation (DAX)
1. **Calculated Columns:** Create these first on the tables:
   * `Order Size`, `Regional Bonus`, `Price Label`, `Days Since Order`, `Is Month End` (on **Sales** table).
   * `Customer Label` (on **Customers** table).
2. **Measures:** Create a separate table called "Key Measures" (Enter Data > Name it "Key Measures") and create:
   * `Total Sales`, `Average Order Value`, `Order Count`, `Total Sales - All Regions`, and `Gross Profit Margin`.

## Phase 3: Dashboard Layout & Visualization
1. **Header Layer:**
   * Place a **Text Box** at the top: "Executive Sales Overview".
   * Add a **Slicer** using `Customers[Region]` or your `Is Month End` column for filtering.
2. **Main KPI Layer:**
   * Use **Card Visuals** for `Total Sales`, `Order Count`, and `Average Order Value`.
   * Use a **Gauge Visual** for `Gross Profit Margin`.
3. **Analysis Layer:**
   * **Area Chart:** `Total Sales` by `OrderDate`.
   * **Donut Chart:** `Order Count` by `Order Size Category`.
   * **Clustered Bar Chart:** `Total Sales` vs `Total Sales - All Regions` by `Region` (to see market share).
4. **Detail Layer:**
   * **Table Visual:** List `Customer Label`, `Total Sales`, and `Gross Profit Margin`.

## Phase 4: Polish
1. **Formatting:** Ensure currency columns are formatted as "$ Currency" and percentages as "%".
2. **Themes:** Go to the "View" tab and select a professional dark or corporate theme to make your visuals pop.
