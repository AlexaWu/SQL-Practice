>Popular databases: MySQL, Access, Oracle, Microsoft SQL Server, Postgres\
write SQL within other programming frameworks like Python, Scala, and HaDoop.

[Types of SQL](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems): SQLite, PostgreSQL, and MySQL

>Advanced Join: [UNION](https://www.w3schools.com/sql/sql_union.asp), [CROSS JOIN](https://www.w3resource.com/sql/joins/cross-join.php), and [SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp)

>[Date/Time Functions and Operators](https://www.postgresql.org/docs/9.1/functions-datetime.html):\
[DATE_TRUNC](https://mode.com/blog/date-trunc-sql-timestamp-function-count-on/): truncate date to a particular part of date-time column\
DATE_PART: pulling a specific portion of a date

## SQL commands

DDL(Data Definition Language), DQl(Data Query Language), DML(Data Manipulation Language), DCL(Data Control Language), TCL(transaction Control Language)

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190826175059/Types-of-SQL-Commands.jpg)

#### Examples of DDL commands:

CREATE – create the database or its objects (like table, index, function, views, store procedure and triggers)\
DROP – delete objects from the database\
ALTER – alter the structure of the database\
TRUNCATE – remove all records from a table, including all spaces allocated for the records are removed\
COMMENT – add comments to the data dictionary\
RENAME – rename an object existing in the database

#### Example of DQL:

SELECT – retrieve data from the a database.

#### Examples of DML:

INSERT – insert data into a table\
UPDATE – update existing data within a table\
DELETE – delete records from a database table

#### Examples of DCL commands:

GRANT – gives user’s access privileges to database\
REVOKE – withdraw user’s access privileges given by using the GRANT command

#### Examples of TCL commands:

COMMIT – commits a Transaction\
ROLLBACK – rollbacks a transaction in case of any error occurs\
SAVEPOINT – sets a savepoint within a transaction\
SET TRANSACTION – specify characteristics for the transaction
