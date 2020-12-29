![](https://github.com/AlexaWu/SQL-Questions/blob/main/SQL%20illustration/Common-Table-Expression-Basic.png)

CTE query definition:
```javascript
SELECT NationalIDNumber,
       JobTitle
FROM   HumanResources.Employee
```

CTE acts like a VIEW.

You can define more than one CTE within a WITH statement. This can help you simplify some very complicated queries which are ultimately joined together. Each complicated piece can include in their own CTE which is then referred to and joined outside the WITH clause.

Here is an example using of TWO CTE’s

![](https://github.com/AlexaWu/SQL-Questions/blob/main/SQL%20illustration/Two%20CTE.jpg)

The first common table expression is colored **green**, the second **blue**. From the SELECT statement the CTE’s are joined as if they were tables.

Why CTE?

--Readability – CTE’s promote readability. Rather than lump all you query logic into one large query, create several CTE’s, which are the combined later in the statement.  This lets you get the chunks of data you need and combine them in a final SELECT.
--Substitute for a View – You can substitute a CTE for a view. This is handy if you don’t have permissions to create a view object or you don’t want to create one as it is only used in this one query.
--Recursion – Use CTE’s do create recursive queries, that is queries that can call themselves. This is handy when you need to work on hierarchical data such as organization charts.
--Limitations – Overcome SELECT statement limitations, such as referencing itself (recursion), or performing GROUP BY using non-deterministic functions.
Ranking – Whenever you want to use ranking function such as ROW_NUMBER(), RANK(), NTILE() etc.
