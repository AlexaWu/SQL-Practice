# [Introducing_CTE](https://www.linkedin.com/learning/querying-microsoft-sql-server-2012/introducing-common-table-expressions)

```javascript
-- Using database
USE AdventureWorks2012;
GO

-- Define the CTE expression name(Sales_CTE) and column list(will use when referenced in a query later).
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)
AS

-- This is the inner query(generates the structure of the CTE and returns the data values that will be contained in the CTE)
(
    SELECT SalesPersonID, SalesOrderID, 
	YEAR(OrderDate) AS SalesYear
    FROM Sales.SalesOrderHeader
    WHERE SalesPersonID IS NOT NULL
)

-- Note that inner query can execute by itself

SELECT SalesPersonID, COUNT(SalesOrderID) AS TotalSales, 
	SalesYear
FROM Sales_CTE
GROUP BY SalesYear, SalesPersonID
ORDER BY SalesPersonID, SalesYear;
GO
```
