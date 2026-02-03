1. OVERALL WORKFLOW (ALWAYS FOLLOW THIS ORDER)

Load data → Power Query

Append / Merge tables

Build Star Schema (1 Fact + Dimensions)

Disable Load for helper tables

Load to Power BI

Create relationships

Create Date table

Add calculated columns

Create measures

Build visuals

2. WHEN TO USE APPEND VS MERGE
Append (UNION)

Use when tables have same structure and need to be stacked vertically.

Example:

Sales2024

Sales2025

Result → One Sales table

Merge (JOIN)

Use when combining columns from different tables using a key.

Example:

Sales + Returns

Sales + Products

3. MERGING SALES WITH RETURNS (LEFT JOIN)

Power Query:

Select Sales table

Merge Queries

Choose Returns table

Join Column: SaleID / OrderID

Join Type: Left Outer

Expand:

ReturnDate

ReturnQty

ReturnAmount

Result: Every sale row contains return info (null if not returned)

4. HANDLING NULL VALUES

Replace in Power Query:

ReturnQty → Replace null → 0 ReturnAmount → Replace null → 0 City → Replace null → "Unknown" Category → Replace null → "Unknown"

Goal: No nulls in Fact or Dimensions

5. STAR SCHEMA STRUCTURE
FACT TABLE

SaleID

ProductID

CustomerID

StoreID

SaleDate

Quantity

UnitPrice

TotalAmount

ReturnDate

ReturnQty

ReturnAmount

DIMENSIONS

DimProduct:

ProductID

ProductName

Category

DimCustomer:

CustomerID

CustomerName

City

DimStore:

StoreID

StoreName

State

DimDate:

Date

Year

Month

Day

6. DISABLE LOAD (VERY IMPORTANT)

In Power Query: Right click helper tables → Disable Load

Only these should load:

Fact

Dimensions

7. DATE TABLE

Modeling → New Table

DateTable =
CALENDAR (DATE(2020,1,1), DATE(2026,12,31))

Add columns:

Year = YEAR(DateTable[Date])
Month = FORMAT(DateTable[Date],"MMM")
MonthNum = MONTH(DateTable[Date])
Day = DAY(DateTable[Date])

Relationship: Fact[SaleDate] → DateTable[Date]

8. CALCULATED COLUMNS (FACT)
Year
Year = YEAR(Fact[SaleDate])
Month
Month = MONTH(Fact[SaleDate])
Days Between Sale and Return
DaysToReturn =
IF(
 ISBLANK(Fact[ReturnDate]),
 BLANK(),
 DATEDIFF(Fact[SaleDate], Fact[ReturnDate], DAY)
)
Return Amount Column
ReturnAmountCalc = Fact[ReturnQty] * Fact[UnitPrice]
9. CORE MEASURES (COPY & PASTE)
Total Sales
Total Sales = SUM(Fact[TotalAmount])
Total Returns
Total Returns = SUM(Fact[ReturnAmountCalc])
Return Percentage
Return % = DIVIDE([Total Returns],[Total Sales])
Average Return Days
Avg Return Days = AVERAGE(Fact[DaysToReturn])
Orders Count
Orders Count = COUNT(Fact[SaleID])
Current Year Sales
Current Year Sales =
CALCULATE(
 [Total Sales],
 YEAR(DateTable[Date]) = YEAR(TODAY())
)
Previous Year Sales
Previous Year Sales =
CALCULATE(
 [Total Sales],
 YEAR(DateTable[Date]) = YEAR(TODAY())-1
)
10. VISUAL PATTERNS
Sales by Product

Axis → ProductName Values → Total Sales

Sales by Customer

Axis → CustomerName Values → Total Sales

Sales by City / State

Legend → City or State Values → Total Sales

Sales by Store

Axis → StoreName Values → Total Sales

Sales Over Time

Axis → DateTable[Month] Values → Total Sales

11. REQUIRED VISUAL TYPES

Card

Column Chart

Bar Chart

Pie or Donut

Table

Matrix

12. REPORT PAGE STRUCTURE
Page 1 – Summary

Cards:

Total Sales

Total Returns

Return %

Orders Count

Charts:

Sales by Month

Sales by Product

Slicers:

Year

Category

Store

Page 2 – Customers

Bar: Customer → Total Sales Table: Customer, Orders Count, Return %

Page 3 – Products

Column: Product → Total Sales Matrix: Product x City → Return %

13. INSIGHT IDEAS (WRITE ANY ONE)

Product X has highest return rate in City Y

Category A generates highest revenue

Store B has lowest average return days

Returns spike in certain months

14. QUICK GOOGLE QUERIES

Power BI merge two tables left join Power BI star schema example Power BI date table dax DAX days between two dates DAX return percentage
