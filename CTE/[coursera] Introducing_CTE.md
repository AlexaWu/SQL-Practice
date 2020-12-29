# [Introducing_CTE](https://www.linkedin.com/learning/querying-microsoft-sql-server-2012/introducing-common-table-expressions)

```javascript
USE AdventureWorks2012;
GO

-- Define the CTE expression name(Sales_CTE) and column list(will use when referenced in a query later).
WITH Sales_CTE (SalesPersonID, SalesOrderID, SalesYear)
AS

-- This is the query that generates the structure of the CTE and returns the data values that will be contained in the CTE.
(
    SELECT SalesPersonID, SalesOrderID, 
		YEAR(OrderDate) AS SalesYear
    FROM Sales.SalesOrderHeader
    WHERE SalesPersonID IS NOT NULL
)

-- Now that the inner query has been created, we can define the CTE outer query that will use the result set from the previous query.
-- Note that the previous query can execute by itself, but this query will generate an error if you execute it alone, demonstrating that the CTE only exists in the scope of the entire query operation

SELECT SalesPersonID, COUNT(SalesOrderID) 
	AS TotalSales, SalesYear
FROM Sales_CTE
GROUP BY SalesYear, SalesPersonID
ORDER BY SalesPersonID, SalesYear;
GO
```
