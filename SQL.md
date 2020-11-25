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
## Approach: Using _**outer join**_ [Accepted]

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
|--
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
However, this solution will be judged as 'Wrong Answer' if there is no such second highest salary since there might be only one record in this table. To overcome this issue, we can take this as a temp table.
```
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
