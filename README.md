Total Sales
Total Sales = SUM(fact_sales[TotalAmount])

Total Quantity
Total Quantity = SUM(fact_sales[Quantity])

Orders Count
Orders = COUNT(fact_sales[OrderID])

Average Order Value
Avg Order Value =
DIVIDE([Total Sales],[Orders])
