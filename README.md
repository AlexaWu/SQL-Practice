# Leetcode

`Table Name`            *primary key*         **SQL Function**

# SQL

[175. Combine Two Tables [easy]](https://github.com/AlexaWu/Leetcode/blob/main/SQL.md#175-combine-two-tables-easy)\
[176. Second Highest Salary [easy]](https://github.com/AlexaWu/Leetcode/blob/main/SQL.md#176-second-highest-salary-easy)\
[177. Nth Highest Salary [medium]](https://github.com/AlexaWu/Leetcode/blob/main/SQL.md#177-nth-highest-salary-medium)\
[178. Rank Scores [medium]](https://github.com/AlexaWu/Leetcode/blob/main/SQL.md#178-rank-scores-medium)\
[180. Consecutive Numbers [medium]](https://github.com/AlexaWu/Leetcode/blob/main/SQL.md#180-consecutive-numbers-medium)\
[181. Employees Earning More Than Their Managers [easy]](https://github.com/AlexaWu/Leetcode/blob/main/SQL.md#181-employees-earning-more-than-their-managers-easy)\
[182. Duplicate Emails [easy]](https://github.com/AlexaWu/Leetcode/blob/main/SQL.md#182-duplicate-emails-easy)\





```javascript
select        2
from      ]
where     ]   1
group by  ]
having    ]
order by      3
```

![](https://github.com/AlexaWu/Leetcode/blob/main/SQL%20illustration/cheatsheet.PNG)

![](https://github.com/AlexaWu/Leetcode/blob/main/SQL%20illustration/cheatsheet%201.png)

![](https://github.com/AlexaWu/Leetcode/blob/main/SQL%20illustration/cheatsheet%202.png)

![](https://github.com/AlexaWu/Leetcode/blob/main/SQL%20illustration/cheatsheet%203.png)


## Querying data from a table
Query data in columns c1, c2 from a table
```javascript
SELECT c1, c2 FROM t;
```
Query all rows and columns from a table
```javascript
SELECT * FROM t;
```
Query data and filter rows with a condition
```javascript
SELECT c1, c2 FROM t
WHERE condition;
```
Query distinct rows from a table
```javascript
SELECT DISTINCT c1 FROM t
WHERE condition;
```
Sort the result set in ascending or descending order
```javascript
SELECT c1, c2 FROM t
ORDER BY c1 ASC [DESC];
```
Skip offset of rows and return the next n rows
```javascript
SELECT c1, c2 FROM t
ORDER BY c1 
LIMIT n OFFSET offset;
```
Group rows using an aggregate function
```javascript
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1;
```
Filter groups using HAVING clause
```javascript
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
HAVING condition;
```
## Using SQL Operators
Combine rows from two queries
```javascript
SELECT c1, c2 FROM t1
UNION [ALL]
SELECT c1, c2 FROM t2;
```
Return the intersection of two queries
```javascript
SELECT c1, c2 FROM t1
INTERSECT
SELECT c1, c2 FROM t2;
```
Subtract a result set from another result set
```javascript
SELECT c1, c2 FROM t1
MINUS
SELECT c1, c2 FROM t2;
```
Query rows using pattern matching %, _
```javascript
SELECT c1, c2 FROM t1
WHERE c1 [NOT] LIKE pattern;
```
Query rows in a list
```javascript
SELECT c1, c2 FROM t
WHERE c1 [NOT] IN value_list;
```
Query rows between two values
```javascript
SELECT c1, c2 FROM t
WHERE  c1 BETWEEN low AND high;
```
Check if values in a table is NULL or not
```javascript
SELECT c1, c2 FROM t
WHERE  c1 IS [NOT] NULL;
```

