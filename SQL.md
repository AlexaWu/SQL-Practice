# 175. Combine Two Tables [easy]

Table: `Person`

Column Name | Type
-- | --
PersonId    | int
FirstName   | varchar
LastName    | varchar

*PersonId* is the primary key column for this table.

Table: `Address`

Column Name | Type
-- | --
AddressId   | int
PersonId    | int
City        | varchar
State       | varchar

*AddressId* is the primary key column for this table.
 

Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:

> FirstName, LastName, City, State

---

SQL Schema
```javascript
Create table Person (PersonId int, FirstName varchar(255), LastName varchar(255))
Create table Address (AddressId int, PersonId int, City varchar(255), State varchar(255))
Truncate table Person
insert into Person (PersonId, LastName, FirstName) values ('1', 'Wang', 'Allen')
Truncate table Address
insert into Address (AddressId, PersonId, City, State) values ('1', '2', 'New York City', 'New York')
```
### Approach: Using _**outer join**_ [Accepted]

#### Algorithm

Since the *PersonId* in table `Address` is the foreign key of table `Person`, we can join this two table to get the address information of a person.

Considering there might not be an address information for every person, we should use _**outer join**_ instead of the default _**inner join**_.

#### MySQL
```javascript
select FirstName, LastName, City, State
from Person left join Address
on Person.PersonId = Address.PersonId
;
```
> Note: Using _**where**_ clause to filter the records will fail if there is no address information for a person because it will not display the name information.

#### Output
> {"headers": ["FirstName", "LastName", "City", "State"], "values": [["Allen", "Wang", null, null]]}

![](https://github.com/AlexaWu/Leetcode/blob/main/SQL%20illustration/join.jpg)

# 176. Second Highest Salary [easy]

Write a SQL query to get the second highest salary from the `Employee` table.

Id | Salary
-- | ----
1  | 100
2  | 200
3  | 300

For example, given the above Employee table, the query should return `200` as the second highest salary. If there is no second highest salary, then the query should return `null`.

SecondHighestSalary
--|
200           

---

SQL Schema
```javascript
Create table If Not Exists Employee (Id int, Salary int)
Truncate table Employee
insert into Employee (Id, Salary) values ('1', '100')
insert into Employee (Id, Salary) values ('2', '200')
insert into Employee (Id, Salary) values ('3', '300')
```

## Approach: Using sub-query and _**LIMIT**_ clause [Accepted]
#### Algorithm

Sort the distinct salary in descend order and then utilize the LIMIT clause to get the second highest salary.
```javascript
SELECT DISTINCT
    Salary AS SecondHighestSalary
FROM
    Employee
ORDER BY Salary DESC
LIMIT 1 OFFSET 1
```
However, this solution will be judged as 'Wrong Answer' if there is no such second highest salary since there might be only one record in this table. To overcome this issue, we can take this as a temp table.

#### MySQL
```javascript
SELECT
    (SELECT DISTINCT
            Salary
        FROM
            Employee
        ORDER BY Salary DESC
        LIMIT 1 OFFSET 1) AS SecondHighestSalary
;
```
## Approach: Using _**IFNULL**_ and _**LIMIT**_ clause [Accepted]
Another way to solve the 'NULL' problem is to use IFNULL funtion as below.

#### MySQL
```javascript
SELECT
    IFNULL(
      (SELECT DISTINCT Salary
       FROM Employee
       ORDER BY Salary DESC
        LIMIT 1 OFFSET 1),
    NULL) AS SecondHighestSalary
```
#### Output
> {"headers": ["SecondHighestSalary"], "values": [[200]]}

# 177. Nth Highest Salary [medium]

Write a SQL query to get the nth highest salary from the `Employee` table.

Id | Salary |
-- | --
1  | 100  
2  | 200   
3  | 300   

For example, given the above Employee table, the nth highest salary where n = 2 is 200. If there is no nth highest salary, then the query should return `null`.

getNthHighestSalary(2)
-- |
200

## Approach:
```javascript
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  DECLARE M INT;
  SET M=N-1;
  RETURN (
      SELECT DISTINCT Salary
        FROM Employee
        ORDER BY Salary DESC
        LIMIT M, 1
  );
END
```
#### Output
> {"headers": ["getNthHighestSalary(2)"], "values": [[200]]}

# 178. Rank Scores [medium]

Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks.

Id | Score
-- | --
1  | 3.50  
2  | 3.65  
3  | 4.00  
4  | 3.85  
5  | 4.00  
6  | 3.65  

For example, given the above Scores table, your query should generate the following report (order by highest score):

score | Rank    
-- | --
 4.00  | 1       
 4.00  | 1       
 3.85  | 2       
 3.65  | 3       
 3.65  | 3       
 3.50  | 4       

> Important Note: For MySQL solutions, to escape reserved words used as column names, you can use an apostrophe before and after the keyword. For example `Rank`.

### Approach:



---
---
---

# 1440. Evaluate Boolean Expression [medium]

Table `Variables`:
| Column Name   | Type    |
-- |--
 name          | varchar 
 value         | int     
 
*name* is the primary key for this table.
This table contains the stored variables and their values.
 

Table `Expressions`:
Column Name   | Type    
-- |--
left_operand  | varchar 
operator      | enum    
right_operand | varchar 

> (*left_operand, operator, right_operand*) is the primary key for this table.
This table contains a boolean expression that should be evaluated.\
operator is an enum that takes one of the values ('<', '>', '=')\
The values of left_operand and right_operand are guaranteed to be in the Variables table.
 

Write an SQL query to evaluate the boolean expressions in Expressions table.

Return the result table in any order.

The query result format is in the following example.

`Variables` table:
 name | value 
-- |--
 x    | 66    
 y    | 77    

`Expressions` table:
left_operand | operator | right_operand 
-- |-- |--
x            | >        | y             
x            | <        | y             
 x            | =        | y             
 y            | >        | x             
 y            | <        | x             
 x            | =        | x             

`Result` table:
left_operand | operator | right_operand | value
-- |-- |-- |--
 x            | >        | y             | false 
 x            | <        | y             | true  
 x            | =        | y             | false 
 y            | >        | x             | true  
 y            | <        | x             | false 
 x            | =        | x             | true  

As shown, you need find the value of each boolean exprssion in the table using the variables table.

---

SQL Schema
```javascript
Create Table If Not Exists Variables (name varchar(3), value int)
Create Table If Not Exists Expressions (left_operand varchar(3), operator ENUM('>', '<', '='), right_operand varchar(3))
Truncate table Variables
insert into Variables (name, value) values ('x', '66')
insert into Variables (name, value) values ('y', '77')
Truncate table Expressions
insert into Expressions (left_operand, operator, right_operand) values ('x', '>', 'y')
insert into Expressions (left_operand, operator, right_operand) values ('x', '<', 'y')
insert into Expressions (left_operand, operator, right_operand) values ('x', '=', 'y')
insert into Expressions (left_operand, operator, right_operand) values ('y', '>', 'x')
insert into Expressions (left_operand, operator, right_operand) values ('y', '<', 'x')
insert into Expressions (left_operand, operator, right_operand) values ('x', '=', 'x')
```
