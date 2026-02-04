# Sample Dataset for DAX Practice

To practice the DAX formulas in the slides, you can use this sample retail dataset.

## Table: Sales
| OrderID | OrderDate | ProductID | CustomerID | Quantity | UnitPrice | Discount |
|---------|-----------|-----------|------------|----------|-----------|----------|
| 1001    | 2024-01-01| P001      | C001       | 2        | 1200      | 0.05     |
| 1002    | 2024-01-02| P002      | C002       | 1        | 800       | 0        |
| 1003    | 2024-01-05| P001      | C003       | 5        | 1200      | 0.10     |
| 1004    | 2024-01-10| P003      | C001       | 3        | 500       | 0        |
| 1005    | 2024-01-15| P002      | C004       | 2        | 800       | 0.05     |
| 1006    | 2024-02-01| P003      | C002       | 10       | 500       | 0.15     |

## Table: Products
| ProductID | ProductName | Category   | CostPrice |
|-----------|-------------|------------|-----------|
| P001      | Laptop      | Electronics| 900       |
| P002      | Desk Chair  | Furniture  | 500       |
| P003      | Keyboard    | Accessories| 200       |

## Table: Customers
| CustomerID | CustomerName | Region |
|------------|--------------|--------|
| C001       | Alice Smith  | North  |
| C002       | Bob Jones    | South  |
| C003       | Charlie Day  | West   |
| C004       | Diana Prince | East   |

## Table: Calendar (Derived)
A standard calendar table from `2024-01-01` to `2024-12-31`.
