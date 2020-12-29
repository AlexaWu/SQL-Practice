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

![]()
