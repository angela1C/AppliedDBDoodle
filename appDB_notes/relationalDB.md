## Introductory notes for applied databases module at GMIT.

Based on lecture notes, [the MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/), [W3schools SQL tutorial](https://www.w3schools.com/sql/sql_ref_mysql.asp) and [tutorialspoint.com DBMS tutorial](https://www.tutorialspoint.com/dbms/index.htm).

## Data
- **datum**: a single piece of information / fact / statistic
- **data**: a series of facts or statistics
- Types of data:
    - non-digital data
    - digital data
        * active digital footprint
        * passive digital footprint.

There is an ever increasing data. Every minute linked in, tweets, google searches, YouTube videos, weather forecasts...


## Database
A database is a collection of related data organised so data can be easily accessed, managed and updated.   
A **relational** database (such as Microsoft SQL Server, Oracle, MySql, IBM DB2) consists of a set of tables for storing data where a table is a collection of related data where a **table** is a collection of related data. Each table has a **unique name** and may relate to one or more other tables in the database through common values.

There are also non-relational (**NoSQL**) databases such as mongoDB, casandra, neo4j and redis.

## Relational Databases

A table in a database is a collection of rows (**records** or **tuples**) and columns (**fields** or **attributes**.). Tables are also known as **entities** or **relations**.
A column contains data representing a specific characteristics of the records in the table.

## Database Schema
A database schema represents the **logical configuation** of a database and defines how the data and relationships between data is stored. 
There are two types of schema, the 
**physical schema** which defines how data is physically stored on a storage system in terms of 
files and indices while the **logical schema** 
defines the logical constraints that apply to  the stored data, the tables in the database and the relationships between them. 

The **logical schema** is designed before the database is created and does not contain any data.




## Database Management System (DMBS)
A DMBS is software for creating and managing databases.
- interacts with user, databases and other systems to store, retreive and process data
- provides a centralised view of data that can be accessed by multiple users from multiple locations in a controlled manner
- can limit data the user sees and how that end user can view the data. 
- provides many views of a single database schema for different users
- provides data independance so users and application programs don't need to know where or how data is stored
- complete transparency over changes in data storage
- **CRUD** functions:
    - **C**REATE
    - **R**EAD
    - **U**PDATE
    - **D**ELETE
- Data Storage management functions
- Security functions
- Backup and recovery functions
- Transaction management (such as debiting a customer a/c, updating the shipping table, updating the product table and crediting the store a/c.)
- Data Integrity (such as not being able to add a doctorID for a patient in the patient table where the doctor id that doesn't already exist in the doctor table. )
- Concurrency



### Advantages of DBMS:
- data integrity
- Enforcement of standards
- Backup and Recovery   
- Controls redundancy - a centralised DBMS eliminates duplication. Data need only be stored once and cane be accessed by many users.
    

### Disadvantages of DBMS:
- Complexity
- Size
- Performance
- Impact of failure

- MySQL is a database management system 
- [Database Management System Tutorial](https://www.tutorialspoint.com/dbms/index.htm)


***

# Relational Database Tables


## SQL 
- Structured Query Language
- standard Relational Database Language.
- ANSI/ISO standard but different databases may use their own proprietary extensions on top of the standard SQL.

### What SQL can do:
- Create a new databases
- create tables in a database
- CRUD functions:
    -  `Insert` data into a database
    -  `Read` data from a database
    -  `Update` data in a database
    -  `Delete`  data from a database
- Manage transactions
- Manage concurrency
- Backup and Recovery
- Manage Users

Note that SQL is a language while MySQL is a database management system.

# MySQL - a database management system
- manages many different database systems.

- [Download MySQL](https://dev.mysql.com/downloads/)
- [MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/)
- [MySQL Tutorial - Tutorialspoint](https://www.tutorialspoint.com/mysql/index.htm)
  
## Using MySQL Workbench
- Open `MYSQL Workbench`

MySQL Workbench is a **GUI** for interfacing with the database.  The **command line interface** can also be used to work with a database.
The MySQL Workbench shows the commands run in the background.
On Windows you can use ``MySQL 8.0 Command Line Client` app instead of MySQL Workbench.
On Mac, commands can be entered at the `mysql` prompt.

(In MySQL Workbench, the Lightning icon to run all commands and the Lightning icon with a I to just execute the statement under the cursor.)

- `Database` menu > `Connect to Database`
Stored connection: Local Instance
Username: Root

## Using the command line interface

- Go to the folder where MySQL is installed.
- Use Terminal on Mac or Command Prompt in Windows
- MySQL usually installed in program files on Windows:
The path in windows is c:/Program Files/MySQL/MySQL Server 8.0 /bin

In Macbook go back to the root directory using `cd ~` or `cd ..`, then `cd bin` to get to bin folder then `mysql -u root -p` and enter password for root user. 
(-u for username, -p for password)

Note the prompt changes to `mysql` 

(Can use the up arrow to go through the previously entered commands)

### Creating a Database:

- `CREATE DATABASE <database>;'`


- `SHOW DATABASES;` to see what databases currently exist on the server
shows all the databases currently managed by MySQL


- `USE <database>;`


### IMPORTING DATABASES:

One function of a DBMS is to backup a database to a file. A database that was previously exported to a file can be imported. When a database in imported, it is recreated.

### DROP database, USE database.

In In MySQL Workbench, `Server` menu > `Data Import` > `Import from Self-contained file` and browse to the location.

- `DROP database <database>` to remove a database.

- `USE <database>` to actually use a database so that any commands are sent to this database.

`SHOW TABLES`. 




## Creating Tables using SQL
- [3.3.2 Creating a Table](https://dev.mysql.com/doc/refman/8.0/en/creating-tables.html)

```sql

    CREATE TABLE pet (name VARCHAR(20), owner VARCHAR(20),
    species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);
```

## MySQL data types:
    - [data-types](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
    - [Numeric data types](https://dev.mysql.com/doc/refman/8.0/en/numeric-types.html)


See [MySQL Reference Manual Chapter 11 Data Types](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
Here are some. 
### Numeric Data Type Syntax
See [Section 11.1.1 Numeric Data Type Syntax](https://dev.mysql.com/doc/refman/8.0/en/numeric-type-syntax.html)
- Integer Types (Exact Value) - INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT
- Fixed-Point Types (Exact Value) - DECIMAL, NUMERIC
- Floating-Point Types (Approximate Value) - FLOAT, DOUBLE
- Bit-Value Type - BIT
- Numeric Type Attributes
- Out-of-Range and Overflow Handling

### Date and Time Data Types

See [Section 11.2 for Date and Time Data Type Syntax](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html)
- The DATE, DATETIME, and TIMESTAMP Types
- The TIME Type
- The YEAR Type
- Automatic Initialization and Updating for TIMESTAMP and DATETIME
- Fractional Seconds in Time Values
- Conversion Between Date and Time Types
- 2-Digit Years in Dates



### String Data Types

See [Section 11.3.1 for String Data Type Syntax](https://dev.mysql.com/doc/refman/8.0/en/string-type-syntax.html)
- The CHAR and VARCHAR Types
- The BINARY and VARBINARY Types
- The BLOB and TEXT Types
- The ENUM Type
- The SET Type

[The ENUM type](https://dev.mysql.com/doc/refman/8.0/en/enum.html) is a string object with a value chosen from a list of permitted values that are enumerated explicitly in the column specification at table creation time.


Also covered in chapter 11 are [Spatial Data Types](https://dev.mysql.com/doc/refman/8.0/en/spatial-types.html) and  [JSON data types](https://dev.mysql.com/doc/refman/8.0/en/json.html).
This chapter also covers default values for data types.

## Creating Tables

- `CREATE TABLE <table> (
    <column1><datatype>
    <column2><datatype>
    <column3><datatype>
    );`

- Decide what tables you need and what columns should be in each table.
- Specify the layout of each table

- `CREATE TABLE <table>;`
(see also `ALTER TABLE` statement)


## Primary Keys: Uniquely identifying rows in a table.

- A  **primary key constraint** is used to uniquely identify each row / record in a table.
- A primary key must contain unique, non-NULL values
- Only one primary key per table
- A primary key can be a single or multiple fields

## Describing Tables

- `DESCRIBE <table>;'`
- 

[Describe](https://dev.mysql.com/doc/refman/5.7/en/show-columns.html) describes the table structure. The `show columns` statement provides information similar to the `describe` statement. See section [Show Columns statement](https://dev.mysql.com/doc/refman/5.7/en/show-columns.html). 

- **Field**: the column name
- **Type**: the column data type
- **Null**: yes or no
- **Key**: whether the column is indexed.
    - PRI: if the column is a primary key or one of the columns in a mult-index  primary key
    - UNI: If the column is the first column of a UNIQUE index. (A UNIQUE index permits multiple NULL values as shown in the Null field.)
    - MUL: if the column is the first column of a nonunique index in which multiple occurrences of a given value are permitted within the column
- **Default**: The default value for the column. This is NULL if the column has an explicit default of NULL, or if the column definition includes no DEFAULT clause.
- **Extra**: 
    - often blank if no additional information about a given column
    - auto_increment for columns that have the AUTO_INCREMENT attribute.
    - on update CURRENT_TIMESTAMP for TIMESTAMP or DATETIME columns that have the ON UPDATE CURRENT_TIMESTAMP attribute


## Getting data from a Table: 
[section 13.2.10 SELECT statement](https://dev.mysql.com/doc/refman/8.0/en/select.html)

To get information from a database use the `SELECT` commands.
- To get all attributes use `SELECT * FROM <table>;`


```sql
    SELECT <columns> 
    FROM <table>;
```          
- `SELECT` for getting information `FROM` a table `WHERE` ...

###  `WHERE` operators
-  equal to:        `=` 
-  not equal to:    `<>` or `!=`
-  greater than `>`, 
- less than `<`
-  greater than or equal to ` >=`,
-  less than or equal to `<=`, 
- `BETWEEN` an inclusive range
- `LIKE` to search for a pattern
- `IN` result is in a set of multiple specified values

### LIKE
`WHERE age >= 20 AND age <= 30;` 
is same as 
`WHERE age BETWEEN 20 and 30;`

-  `LIKE` to search for a specified pattern
-  `%` represents 0 or more characters
-  `_` a single character

### IN
The `IN` operator can be used instead of multiple `OR`s. Can use IN to determine if a specified value matches any value in a set of values, or returned by a sub-query.

`WHERE age in (12,13,14,15)` 
is same as

```sql
    WHERE age = 12
    OR age = 13
    OR age = 14
    OR age =15`
```
## OPERATOR PRECEDENCE!
- Note operator precendence and be careful when using `AND` and `OR` statements.
- Use parentheses when combining AND, OR operators for [Section 12.3.1 Operator Precedence](https://dev.mysql.com/doc/refman/8.0/en/operator-precedence.html).
- 
```sql
SELECT name, age FROM person 
WHERE sex="m" AND (name LIKE "S%" OR name LIKE "A%");
```

### The `LIMIT` clause.

- use `LIMIT` clause to constrain number of rows returned by SELECT statement.
Can use a single number, for example `LIMIT 3` returns the first three matching results or two numbers to specify the starting point and the number of results to return. For example `LIMIT 0,3;` returns the first 3 results matching while `LIMIT 3,3;` returns the three results starting from the 4th result.

### DISTINCT
- `SELECT DISTINCT` statement to return only distinct values

See [Distinct Optimization](https://dev.mysql.com/doc/refman/8.0/en/distinct-optimization.html)


### ORDER BY
See [ORDER BY optimization](https://dev.mysql.com/doc/refman/8.0/en/order-by-optimization.html) in Chapter 8 Optimization.
- `ASC` for ascending
- `DESC` for descending
- `YEAR()` get year from date
- `DAY()` get day from date
- `MONTH()` get month from date.



### DATE AND TIME FUNCTIONS
[DATE and TIME FUNCTIONS](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)


`MONTH()` – Get Month from date
`DAY()` – Get Day from date
`YEAR()`: get year from data
`MONTHNAME();`

***

# MySQL FUNCTIONS AND PROCEDURES

MySQL can also **manipulate data** before storing or retrieving  it.
A  **function** is a piece of code that performs an operation and returns a result.
Some functions accept parameters while others don't.

## Why use functions?
- Functions can be used to maintain business logic ,for example a mobile app and Web sites can use the same business logic when working with the same database, or regional websites that work from the same database.

## BUILT IN FUNCTIONS
See [Chapter 12 Functions and Operators](https://dev.mysql.com/doc/refman/8.0/en/functions.html)
- [String Functions](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)
- [Numeric Functions](https://dev.mysql.com/doc/refman/8.0/en/numeric-functions.html)
- [Date & Time functions](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)
- [Aggregate Functions](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)
- [MySQL Information functions](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html)
- [MySQL Control flow functions](https://dev.mysql.com/doc/refman/8.0/en/control-flow-functions.html)


## STRING FUNCTIONS
[Section 12.7 String Functions and Operators](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)

- `UPPER()`: convert to uppercase
- `STRCMP()`: compare two strings. Returns 0 if 2 strings match, -1 if string1 < string2, returns 1 of string1 is > string 2.

- `ASCII()`:  Return numeric value of left-most character, the **first** character in the string
- `REPLACE(string, from_string, to_string)`: Replace all occurences of a specified substring(from_string) within a string with a new substring (to_string)
- `SUBST(string, start, length)`: return the substring as specified from a string, starting at the start position within the string, the number of characters extracted being the length.

- `CHAR_LENGTH()` returns the number of characters in an argument
- `CONCAT()` return concatenated string
and many more. See 

## NUMERIC FUNCTIONS

- `SQRT()` returns the square root of a number
- `ROUND(number, decimals)` rounds a number to  the number of decimals specified.
- `ABS()` Return the absolute value
- `POWER()` Return the argument raised to the specified power
- `TRUNCATE()` Truncate to specified number of decimal places

See Section 12.5 of Reference Manual for [numeric functions](https://dev.mysql.com/doc/refman/8.0/en/numeric-functions.html) including arithmetic operators and mathematical functions.

## DATE FUNCTIONS

- `DATEDIFF()` : subtract two dates to get the number of days between them
- `DATE_FORMAT()`: format date as specified such as "%m%d%y"
- `DAYNAME()`
- `DAYOFMONTH()`
- `DAYOFYEAR()`
- `DAYOFWEEK()`
- `MAKEDATE()`
- `MINUTE()`
- `MONTH()`
- `MONTHNAME()`
- `NOW()`

See section 12.6 of the MySQL reference manual for more [Date and Time functions](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)

## AGGREGATE FUNCTIONS 
See [12.20 Aggregate (GROUP BY) Functions](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions-and-modifiers.html)
An aggregate function performs  a calculation on a set of values and returns a single value.

### GROUP BY
The `GROUP BY` statement is often used with aggregate functions to group the results by one or more columns.


```sql
    SELECT student_name, AVG(test_score)
       FROM student
       GROUP BY student_name
```
### HAVING and WHERE clauses

- The `HAVING` clause can be used with `GROUP BY` to filter groups based on certain conditions
- without including the `GROUP BY` clause, the `HAVING` clause behaves like the `WHERE` clause
- The `HAVING` clause applies a filter condition to each group of rows
- The `WHERE` clause applies the filter condition to each individual row

- `AVG()`
- `MIN()`
- `MAX()`
- `SUM()`
- `COUNT()`

Also STD, VARIANCE and more. 
See section 12.20.1  (https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)

*** 
## MYSQL INFORMATION FUNCTIONS

See [Section 12.15 Information Functions](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html)

- `DATABASE()`: return the default(current) database name
- `USER()`: the user name and host provided by the client

## MYSQL CONTROL FLOW FUNCTIONS
See [See Section 12.4 Control Flow Functions](https://dev.mysql.com/doc/refman/8.0/en/control-flow-functions.html)

- CASE
- IF()
- IFNULL()
- NULLIF()


### IF

See Section 12.4 [Control Flow Functions](https://dev.mysql.com/doc/refman/8.0/en/control-flow-functions.html)  

`SELECT.. IF.. FROM..`
- `IF(condition, value_if_true, value_if_false)`
where the condition is the value to test. 

### CASE WHEN

`SELECT ..CASE WHEN... FROM..` 

- `CASE WHEN condition 1 THEN result 1
        WHEN condition 2 THEN result 2
        WHEN condition 3 THEN result 3
        ELSE result
    END`

`CASE value WHEN [compare_value] THEN result [WHEN [compare_value] THEN result ...] [ELSE result] END`

`CASE WHEN [condition] THEN result [WHEN [condition] THEN result ...] [ELSE result] END`

The return type of a CASE expression result is the aggregated type of all result values. See Section 12.4 [Control Flow Functions](https://dev.mysql.com/doc/refman/8.0/en/control-flow-functions.html).

*** 


# MySQL Stored routines.

- A stored routine is a user-written code that extends the functionality of MySQL.
- can be used to perform the same database operations across multiple client applications in different languages or on different platforms.
- ensures security as applications can only access stored routines and not tables

Stored routines keep business rules consistent.
Stored routines ensure security by having the applications access to the routines only and not the tables. This way all transactions can be logged. 
Reduction of duplication.

### Advantages of Stored Routines:
- **Speed**: performance of application accessing the database is increased as stored procedures are compiled and stored in the database
- **Traffic**: no need to send multiple lengthy SQL statements - the application has to send just the name and parameters of the stored routine.

### Disadvantages:
- **Complexity**: not designed for complex business logic like other languages.
- **Difficult to debug**. (MySQL does not allow you debug  stored procedures)
- **performance** (a DBMS **not well-desgined for logical operations**)

While they can increase the performance of an application accessing the database, moving too much from the application side to the database side can impact the database performance. 


## MySQL Stored Functions:
- A stored function is a special type of stored routine that returns a single value.
- used to encapsulate common formulae or business rules that are reusable among sql staements or stored routines.
- Functions take 0 or more input parameters and return a single value


See [Section 13.1.17 CREATE PROCEDURE and CREATE FUNCTION Statements](https://dev.mysql.com/doc/refman/8.0/en/create-procedure.html)

Example:


`CREATE FUNCTION <function name> (<num1 integer, num2 integer>)`

`RETURNS integer`
`DETERMINISTIC`
`BEGIN`
    `RETURN num1 + num2`
`END`
You must give the function a **function name**. Specify the **parameters** and their **type**.
A function always has a **return value** so you need to specify that.
Specify if the function is **deterministic** or **non-deterministic**.
- Non-deterministic modify data and have update, insert or delete statements. 
- Deterministic functions do not.

The **actual code** for the function is written between **BEGIN** and **END** statements.

```sql
CREATE FUNCTION add2Nums (num1 integer, num2 integer)

RETURNS integer
DETERMINISTIC
BEGIN
    RETURN num1 + num2
END
```

Example:
```sql
CREATE FUNCTION discount(age INT(11))
RETURNS VARCHAR(3)
DETERMINISTIC
BEGIN
    IF age < 16 THEN
        RETURN "0%";
    ELSEIF age < 26 THEN
        RETURN "10%";    
    ELSEIF age < 40 THEN
        RETURN "20%"; 
    ELSEIF age < 60 THEN
        RETURN "30%";   
    ELSE 
        RETURN "40%";
    END IF;
END
  
```

To call the function, do so using **`select`** and the **function  name**.


```SQL
SELECT name, age, discount(age) "Discount"
FROM person;

```

Something that is done over and over can be put into a function.

Functions can be used on relations. pass in the field from the table.
`SELECT name, age, discount(age) "Discount"`
`FROM person`

## STORED PROCEDURES.
Another type of stored routine is a stored procedure. A stored procedure is similar to function as it allow reuse of code, both stored functions and stored procedures can hide details where the logic can be encapsulated into the function and therefore doesn't need to be rewritten each time the same query arises.
Both stored functions and stored procedures implement business logic as the code is updated in one place. 

## Stored Function vs Stored Procedure.

### Functions
- return a single value
- only SELECT statement
- cannot use stored procedures
- does not support transactions 


### Procedures 
- return 0 or more values,
- and can manipulate the data using CRUD functions ( SELECT, INSERT, UPDATE and DELETE), 
- procedures can use stored functions
- procedures supports transactions.
  
- Procedures are created similarly to functions using the *keyword* `procedure`.
- To call the procedure use the `call` keyword and pass in the required parameters.

See [CREATE PROCEDURE and CREATE FUNCTION Statements](https://dev.mysql.com/doc/refman/8.0/en/create-procedure.html)

- Both functions and procedures are used to store logic that is repeatedly use and avoids inconsistencies.
- Instead of having to write out a potentially complex query, a procedure can be called. 


- The delimiter must be changed before writing a function or procedure by entering `delimiter //` before writing the function. `//` after the `END` statement.  
- The delimiter must be changed back to a semi-colon after the function is written by entering `delimiter ;`
- `DETERMINISTIC` means the table is not changed.
- use `select` statement with functions even when not applying to a table.



```sql
delimiter //
CREATE PROCEDURE  make_milage(mk VARCHAR(20), ml(INT(11))
DETERMINISTIC
BEGIN
    SELECT * FROM CAR
    WHERE make LIKE mk
    AND milage < ml
    ORDER BY milage;
END
//
delimiter ;
```
**To call the procedure:**

```sql

call make_milage("Toyota", 200000);
```

### Finding Functions and Procedures

Functions and procedures can be found in the **routines** table in the **information schema** database.
  
```sql
select routine_name, routine_type from information_schema.routines
    WHERE routine_name IN ("add2Nums","discount","make_milage");
```

### To see what is in a Function or a Procedure 

```sql
SHOW CREATE FUNCTION <function-name>;
```
To see the code of a function or a procedure use the show create function or show create procedure commands. Gives a non-user friendly view of the code.   

#### To make changes or delete a function:
To delete a function or procedure, use the `DROP` command.  To make a change to a stored procedure or function, you should first drop it and create it again with the updated code.

```sql
DROP FUNCTION  <function-name>;
```
See Section 13.7.4.1 CREATE FUNCTION Syntax for User-Defined Functions:

[CREATE FUNCTION](https://dev.mysql.com/doc/refman/8.0/en/create-function-udf.html)

***

# Normalisation


# Normalisation - how to have many connected tables in a database,

## What is Normalisation:
Normalization is the process of organizing the columns (attributes) and tables (relations) of a relational database to minimize data redundancy.

- A large table (with a large number of attributes rather than a large number of rows) is basically broken down into several smaller tables. 
- A database is defined as a collection of related data organised in a way where the data can be easily accessed managed and updated.
- Normalisation takes place when the database is being set up. 
- Normalisation makes it easier to update a database and makes it less prone to anomalies.
- A database that is not normalised cannot be easily managed and result in update or deletion anomalies.
- A normalised database would have more than one table with links between the tables instead of all the data stored in a single table.
- reference data from another table rather than duplicating the same data.

## Foreign Keys

When creating tables, the link between the tables is defined by the  **foreign key**. 
- A foreign key is a constraint on the table, on what can be inserted into a table.
- ensures **referential integrity** and keeps the database **consistent**
- `SHOW CREATE TABLE` command will show the foreign keys.
- Tables are joined using the foreign keys.

In the doctor patient example, only values that exist in the doctorID column of the doctor table can be added as a foreign key to the patient table. This is called **Referential integrity** and ensures that the database is consistent. 

## Joining data from tables using foreign keys.

- **`SELECT`** from one table, then **`JOIN`** to another table using the foreign key.
- **`SHOW CREATE TABLE`** will show any foreign keys referencing another table.
- rows are joined based on the foreign key.
- `SELECT` clause contains the fields that will be displayed.
- `FROM`: select from one table only, not both table
- `JOIN` to another table.
- use **alias** names instead of the full table name to make the query less verbose.

Note although the `SELECT` clause is at the start of the query, it is really the last part of the query as it just prints out what you want to have returned and the query starts at the `FROM` clause.

### INNER JOIN

- returns rows from two tables **only** where the `JOIN` condition is met
- if the `JOIN` condition is not met, then nothing is returned from either table.
- with an inner join, it does not matter which table you join to which
- only join tables on the foreign keys.

- to get data from two tables that are not directly joined to each other, look for the foreign keys in the database. Then you can join tables that are not directly connected.

- tables can be joined either way on the foreign key constraint but always join tables on the keys.




### LEFT JOIN
- Returns rows from two tables when the `JOIN` condition is met
- If the `JOIN` condition is **not** met
    - rows from the left (first) table are returned and
    - NULL is returned instead of the rows from the second table

For example an `inner join` will join each row in the doctor table to patient table but only where the doctor id is the same as the doctor id in the doctor table.

- with a left join, the order of tables does matter as all rows from the first table will be returned and therefore if a different table is first, the results will be different.

Normalisation is a more realistic database structure where there are many inter-related tables. A Normalised database reduces the potential for anomalies in the data.
The `SHOW CREATE TABLE` command will show the foreign keys that link to other tables. Information which is stored over several tables can be retrieved by joining the tables using the left or inner join commands.


***

### SHOW CREATE TABLE
The `show create table` shows the same information that the `describe table` command shows but with some more information. It also shows the exact code used for the creation of that table.

`show create table` shows the **foreign key constraint** which is not shown in the `describe` command.
With foreign key constraints we can only reference something if it already exists.

`show create table salaries;`

  PRIMARY KEY (`emp_no`,`from_date`),
  KEY `emp_no` (`emp_no`),
  CONSTRAINT `salaries_ibfk_1` FOREIGN KEY (`emp_no`) REFERENCES `employees` (`emp_no`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 |
+--------------------------------------------------------

### CONSTRAINT `salaries_ibfk_1` FOREIGN KEY (`emp_no`) REFERENCES `employees` (`emp_no`)
This foreign key constraint in the salaries table means that an employee number (emp_no) cannot be put into the salaries table if it doesn’t already exist in the employees table. This ensures the tables are consistent and preserves **referential integrity**. When referencing something, it must already exists.

- The data is separated into different tables to **prevent deletion anomalies**. 
- The constraint means you cannot add a new employee to salaries table unless their emp_no exists in the employees table.
- The `Show create table` command shows these constraints better than the `describe tables` command.
- You can also use the `reverse engineer` functionality in MySQLWorkbench to see if tables are connected. It will show if there is a **foreign key** coming from a table to see if they are connected.
- A primary key can be a composite key

- Note that the foreign keys do not have to have the exact same name. 

- MySQLWorkbench > Database > ReverseEngineer to see a diagram.


- it is best practice to use a short **alias** name for a table name when selecting data from more than one table. This is necessary when the tables have the same column name as otherwise mysql would not know which table is being referred to. Therefore always prefix the column name with the table it comes from. Define the abbreviation for the table the first time it is mentioned directly.

- when joining tables, if a table is not joined on a foreign key as it should be and the query returns something, what is returned might not make any sense so always join on the foreign key.

- The `select` clause goes at the start of the query to state which columns are to be returned.
- the query really only starts after the `from` clause.
- the alias can be used in the select clause even before the table it refers to is first mentioned.

```sql
select pt.*, dt.* from patient_table pt 
inner join doctor_table dt
on pt.doctorID = dt.doctorid; 
```

- If there is a field in both tables with the same name, then you need to use the prefix aliases for the tables so that mysql knows which table you are referring to.
- use left join to show every row from the first table even if there is no associated entry in the second table.

- to show all details of all doctors from one table with the details of their patients from the patients_table, use a left join as this will return all rows from the first table with a null value for rows in the second table where the condition is not met.
- an inner join would omit the rows where the condition is not met

- A table may not have a foreign key pointing out but there may be a foreign key pointing in from another table which can be used for joining tables.

- (in some cases a left-join will return the same results as an inner join, depending on the data in the table)

- if you only want to see rows from one table that have related data in another table use an `inner join`

- if you want to see everything from one table, whether or not there is related data in another table use a left join. This will return  NULL value for rows from the second table where the conditions are not met.

- a query with joins can be used in a stored function or procedure.


***

# CRUD (Create, Insert, Read, Update Delete)

## INSERT

See [Section 13.2.6: INSERT](https://dev.mysql.com/doc/refman/8.0/en/insert.html)
`INSERT` inserts new rows into an existing table.
Inserting into a table requires the INSERT privilege for the table

`INSERT INTO <table> VALUES (value1, value2, valueN);`

If inserting a value for all fields, then the values must be supplied in the correct order of the columns in the table.

`INSERT INTO <table> (column1, column2, column) VALUES (value1, value2, valueN);`

- If you are inserting data into a table where not all fields are being supplied, then the fields and corresponding values must be supplied.  Default values are given to the missing columns.

- Provide a parenthesized list of comma-separated column names following the table name. The number of columns in the source table must match the number of columns to be inserted.

- The values entered must be in the correct order.
- A primary key may be set to auto-increment.
- There may be default values for some fields.
- If there are default values for fields not being supplied with a value, this will be taken care of by MySQL. 

- The `DESCRIBE` function will show the order of the columns in the table as well as details of all columns, including the type of dat for each field, the default values if any, whether a primary key is auto_increment, whether NULL values are allowed or not.
- However just because a default is set to NULL does not mean the missing field will be updated. The NULL column shows whether null is allowed or not. If not the NULL field for this column will be set to NO, even where the default value is NULL. 

- an error  (**Cannot add or update a child row: a foreign key constraint fails**) will result if you try to insert a row with a foreign key in a table if the value for the foreign key does not exist in the other table. (Cannot add a bus registration number into the driver table if the bus reg doesn't exist on the bus table.)


```sql
 describe person;
 ```

| Field     | Type          | Null | Key | Default | Extra          |
| --- | --- | --- | --- | --- | --- | --- |
| personID  | int(11)       | NO   | PRI | NULL    | auto_increment |
| name      | varchar(20)   | NO   |     | NULL    |                |
| age       | int(11)       | YES  |     | NULL    |                |
| sex       | enum('M','F') | YES  |     | M       |                |
| dob       | date          | YES  |     | NULL    |                |
| isStudent | tinyint(1)    | YES  |     | NULL    |                |

For this table, a value must always be supplied for the name field as Null is set to NO.

The primary key (personID) is set to auto_increment.



## UPDATE

### UPDATE ... SET ...
See [section 13.2.13 UPDATE statement](https://dev.mysql.com/doc/refman/8.0/en/update.html)
Update mondifies rows in a table.

```sql
UPDATE <table> SET column1 = value1, columnN, valueN;
```

```sql
UPDATE <table> SET column1 = value1, columnN, valueN 
WHERE condition;
```

- `UPDATE` updates columns of existing rows in the named table with new values. The `SET` clause indicates which columns to modify and the values they should be given.
- Each value can be given as an expression, or the keyword DEFAULT to set a column explicitly to its default value. 
- Without a `WHERE` clause, all rows are updated.
- A `WHERE` clause specifies the conditions that identify which rows to update.  
- The `ORDER BY` the order in which the rows should be updated.
- The `LIMIT` clause places a limit on the number of rows that can be updated.




```sql
update person
set age =30
where personID =9;
``` 

Without the `WHERE` clause, all rows would be updated with the new value for the age field.


### Functions and operators can be applied when updating
```sql
update person set age = age +1;
```
This updates the age fields in all row to the current age plus 1.

### UPDATING based on IF conditions

```sql
UPDATE person SET name=concat(if(sex="M","Mr.","Ms."),name);
```

### UPDATING based on CASE

- a `CASE` allows many updates in one statement instead of several smaller queries.

Sometimes it is better to break the query into smaller queries but often better to use a single query. `case` allows you to do updates in one go instead of doing smaller queries.

```sql
update person
set age = 
case
    when age is null then 18
    else age +1
end;
```



## DELETE

See [section 13.2.2 DELETE](https://dev.mysql.com/doc/refman/8.0/en/delete.html).

- DELETE removes rows from a table.
- The DELETE statement deletes rows and returns the number of deleted rows.
- A DELETE statement can start with a WITH clause 
- DELETE privilege on a table are needed to delete rows from it
- Even if all the rows are deleted, the table still exists.
- A row can be deleted if no other table is referencing the field.
- a row cannot be deleted if a field is referenced elsewhere.


```sql
DELETE FROM <table>;
```

```sql
DELETE FROM <table>; 
WHERE condition;
```

`DELETE FROM <TABLE>;` without a where clause would delete all rows.

`delete from person where sex="M" and isStudent AND age >20;` would only delete rows matching the where condition.

### SHOW CREATE TABLE

The `SHOW CREATE TABLE` command will show if there are any restrictions on delete.

`CONSTRAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus` (`reg`) ON DELETE CASCADE`

ON DELETE CASCADE

` CONSTRAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus` (`reg`) ON DELETE SET NULL`
ON DELETE SET NULL

`CONSTRAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus` (`reg`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 |`

Note that the default constraint is `ON DELETE RESTRICT` if it doesn't say  `ON DELETE CASCADE` or `ON DELETE SET NULL`.

### REFERENTIAL INTEGRITY

- The `bus` table does not have a foreign key, but you cannot delete a row from this table if it is referenced in another table which links to it by a foreign key. The `driver` table has a foreign key that references the `bus` table.

- The delete command will result in an error such as `Cannot delete or update a parent row: a foreign key constraint fails ...` as you cannot associate a driver with a bus if the bus is not in the bus table already. 

- You cannot insert a row with a busReg into the driver table if the bus does not already exist on the bus table. 
This will result in an error "Cannot add or update a child row: a foreign key constraint fails"


If a table's foreign key references a column in another table, and the foreign key constraint is set to `ON DELETE CASCADE`, this means that if a row in the first table is deleted and the value of the field is used in the other table, then this row should also be deleted from the other table.

`ON DELETE RESTRICT` means that if a row in the first table is deleted and the value of the  field is used in the other table, that this row should **not** be deleted from the table as the other table is restricting the delete.

`ON DELETE SET NULL` means that if a row in the table is deleted and the value of the  field is used in the other table, that the foreign in the other table which was referencing the field to be deleted from the other table should be set to NULL, so now the field is no longer referenced and therefore can be deleted from the bus table.

If deleting a row from a table which isn't referenced by any other table, the row will simply be deleted.






















### How are tables in a database related?

The `SHOW CREATE TABlE` query will show any foreign keys that exist in a table. While one table may not contain any foreign keys itself, another table may have a foreign key which points in to that table.

Can also use the Reverse Engineer EER diagram which will show any connections between tables and the direction. 


## SubQueries
- another way to read data from a table
- Instead of taking the result of a query and putting the actual values into another query, instead use a subquery that returns the value to the outer query. 
- whenever data comes from more than one table, the tables must be joined somehow on the foreign key.
- another way to get the information from tables is using a sub-query which is a query within a query.
- subqueries can be used instead of doing an inner join in some cases.
- As brackets take precedence over other operators, a query within brackets will be done first and then the result returned from the subquery used in the outer query. 
- It is better to do a query dynamically like this instead of hardcoding values into the query. Therefore the query can be used again even if the data has changed.
- The result of the inner query gets replaced as the argument in the outer query
- Sometimes a subquery is better than using an inner join
- there can be more than one query nested within another query. The innermost query is run first. The subquery gets replaced with the results of the subquery and so on out to the outer most query.
- The result of the inner query gets replaced as the argument in the outer query.

