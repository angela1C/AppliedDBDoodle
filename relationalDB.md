## Introductory notes for applied databases module at GMIT.

Based on lecture notes, [the MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/), [W3schools SQL tutorial](https://www.w3schools.com/sql/sql_ref_mysql.asp) and [tutorialspoint.com DBMS tutorial](https://www.tutorialspoint.com/dbms/index.htm).

# Part 1: Introduction to Applied Databases.

- what is data
- ever increasing data
- what is a database
- types of databases: Relational and Non-relational databases
- Relational databases
- comparison of relational database to spreadsheets
- Database schema :
    - logical schema
    - physical schema
- Database Management System (DBMS)
- DBMS CRUD functions
- DBMS functions
- Examples of DBMS functions
- Advantages and Disadvantages of DBMS.




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

# Part 2: Relational Database Tables


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

- `DROP <database>` to remove a database.

- `USE <database>` to actually use a database so that any commands are sent to this database.

`SHOW TABLES`. 




### Creating Tables using SQL
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


### Example.
Select name, age and birth where name doesn't start with A and born between 1st and 11th month, show in reverse name order

```sql
SELECT name, age, MONTHNAME(dob)    
    FROM person
    WHERE DAY(dob) BETWEEN 1 and 11
    AND name NOT LIKE "A%"
    ORDER BY name DESC;
```


### DATE AND TIME FUNCTIONS
[DATE and TIME FUNCTIONS](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)


`MONTH()` – Get Month from date
`DAY()` – Get Day from date
`YEAR()`: get year from data
`MONTHNAME();`

***
# 

#  Part 3: MySQL FUNCTIONS AND PROCEDURES

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


## MySQL Stored routines.

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

### Stored Function vs Stored Procedure.

#### Functions
- return a single value
- only SELECT statement
- cannot use stored procedures
- does not support transactions 


#### Procedures 
- return 0 or more values,
- and can manipulate the data using CRUD functions ( SELECT, INSERT, UPDATE and DELETE), 
- procedures can use stored functions
- procedures supports transactions.
  
- Procedures are created similarly to functions using the *keyword* `procedure`.
- To call the procedure use the `call` keyword and pass in the required parameters.

See [CREATE PROCEDURE and CREATE FUNCTION Statements](https://dev.mysql.com/doc/refman/8.0/en/create-procedure.html)

Both functions and procedures are used to store logic that is repeatedly use and avoids inconsistencies.


Instead of having to write out a potentially complex query, a procedure can be called. 
A cleverly designed procedure can help improve its use.

```sql
CREATE PROCEDURE  make_milage(mk VARCHAR(20), ml(INT(11))
DETERMINISTIC
BEGIN
    SELECT * FROM CAR
    WHERE make LIKE mk
    AND milage < ml
    ORDER BY milage;
END

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

#### To see what is in a Function or a Procedure 

```sql
SHOW CREATE FUNCTION <function-name>;
```
To see the code of a function or a procedure use the show create function or show create procedure commands. Gives a non-user friendly view of the code.   

#### To make changes or delete a function:
To delete a function or procedure, use the `DROP` command.  To make a change to a stored procedure or function, you should first drop it and create it again with the updated code.

```sql
DROP FUNCTION  <function-name>;
````
See Section 13.7.4.1 CREATE FUNCTION Syntax for User-Defined Functions:

[CREATE FUNCTION](https://dev.mysql.com/doc/refman/8.0/en/create-function-udf.html)