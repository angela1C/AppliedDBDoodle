- MySQL is  a database management system that manages many different database systems. 
- One of the functions of a DBMS is to backup a database to a file which can be **imported**. When a database is imported it is recreated.
- MySQLWorkbench is a GUI for interfacing with the database.
- can also use the Command line interface to work with a database
- the workbench is basically a GUI for showing the commands that are run in the background.

- `Show Databases` will show the names of the different databases currently managed by Mysql

on MySQLWorkbench: 
- `Server` > `data import` > `import from Self contained file` > browse to the location.

Windows has an app called MySQL 8.0 Command Line Client that can be used instead of the MySQLWorkbench. On a Mac, the commands can be entered at the `mysql` prompt. 

- Command line: 
- Windows using the windows command prompt. 
- Mac using the Terminal application: `cd /bin`

Go go folder where mysql is installed which is usually the programs directory if MySQL has been installed in the standard way. 

Navigate to  `c:/Program Files/MySQL/MySQL Server 8.0 /bin` (windows)  or `cd /bin` on Mac terminal using the `cd` change directory command.

- on command line `mysql -u root -p` then enter password when prompted.

- use `\c` to get out when stuck in a prompt

- `mysql -u root -p` to access mysql on command line in terminal


***

#### `SHOW TABLES;`

 Tables_in_school 

 subject          
 teacher          

2 rows in set (0.01 sec)

#### `DESCRIBE <table>`

```sql
describe subject;
```


| Field         | Type        | Null | Key | Default | Extra |
 ---| ---| ---| ---| ---| --|
| Name          | varchar(15) | NO   | PRI | NULL    |       |
| Teacher       | varchar(20) | YES  |     | NULL    |       |
| OnLeavingCert | tinyint(1)  | YES  |     | NULL    |       |
 

```sql
describe teacher;
```

| Field      | Type          | Null | Key | Default | Extra          |
 ---| ---| ---| ---| ---| --|
| tid        | int(11)       | NO   | PRI | NULL    | auto_increment |
| Name       | varchar(20)   | YES  |     | NULL    |                |
| level      | enum('J','L') | YES  |     | NULL    |                |
| experience | int(11)       | YES  |     | NULL    |                |
| dob        | date          | YES  |     | NULL    |                |

5 rows in set (0.00 sec)

### `DESCRIBE <table>;`
- The `Type` shows the type of data for each Field as well as the maximum number of characters allowed.

- The `Key` column shows which field(s) is the primary key





### `SELECT * FROM;` 

- `select * from teacher` to show all  data in the teacher table
- `select * from subject` to show all data in the subject table

```sql
SELECT * FROM teacher;
```

| tid | Name         | level | experience | dob        |
 ---| ---| ---| ---| ---| 
|   1 | Mr. Pasteur  | L     |         15 | 1960-02-02 |
|   2 | Ms. Dubois   | L     |         22 | 1967-09-02 |
|   3 | Ms. Smith    | J     |          4 | 1980-03-23 |
|   4 | Mr. Hawking  | L     |         40 | 1951-02-19 |
|   5 | Mr. Kavanagh | J     |         50 | 1949-11-01 |
|   6 | Mr. Picasso  | J     |         42 | 1939-03-30 |
|   7 | Fr. Lynch    | L     |         55 | 1939-03-31 |




### Select * from

  
```sql
SELECT * FROM subject;
```


| Name      | Teacher      | OnLeavingCert |
 ---| ---| ---|
| Biology   | Mr. Pasteur  |             1 |
| Colouring | Mr. Picasso  |             0 |
| English   | Mr. Kavanagh |             1 |
| French    | Ms. Dubois   |             1 |
| Maths     | Mr. Hawking  |             1 |
| Religion  | Fr. Lynch    |             1 |
| Spelling  | Ms. Smith    |             0 |


### WHERE

```sql
select name 
from subject 
where onleavingcert =1;
```
gets all subjects on the leaving cert


| name     |
 ---| 
| Biology  |
| English  |
| French   |
| Maths    |
| Religion |


### select * from ... where condition;

```sql
select name, experience 
from teacher 
where level ="L";
```

| name        | experience |
---| ---
| Mr. Pasteur |         15 |
| Ms. Dubois  |         22 |
| Mr. Hawking |         40 |
| Fr. Lynch   |         55 |


This query shows the details of all teachers qualified to teach to leaving cert.

#### SELECT ... FROM ... WHERE .. NOT LIKE " ";

```sql
select * from subject 
where teacher NOT LIKE "Mr.%";
```

Shows details of all subjects taught by teachers whose title is not "Mr."

| Name     | Teacher    | OnLeavingCert |
 ---| ---| ---| 
| French   | Ms. Dubois |             1 |
| Religion | Fr. Lynch  |             1 |
| Spelling | Ms. Smith  |             0 |

#### SELECT ... FROM ... WHERE ... AND ...


```sql
select * from teacher
where month(dob) IN(1,2,3) 
AND level = "J";
```
This shows all teachers born in the specified months and that can teach to junior cert only.

| tid | Name        | level | experience | dob        |
 ---| ---| ---| ---| ---| 
|   3 | Ms. Smith   | J     |          4 | 1980-03-23 |
|   6 | Mr. Picasso | J     |         42 | 1939-03-30 |

which gives the same results as:

```sql
select * from teacher 
where month(dob) between 1 and 3 
AND level = "J";
```
### DISTINCT

#### SELECT DISTINCT ... FROM ...

```sql
select distinct monthname(dob)
from teacher;
```
Shows all **unique** month names that teachers were born in

| monthname(dob) |
--- |
| February       |
| September      |
| March          |
| November       |

### ORDER BY
#### SELECT ... FROM ... ORDER BY...

```sql
select * from teacher
order by experience desc, level;
```
Shows all details of teachers sorted by experience first, then level.

| tid | Name         | level | experience | dob        |
 ---| ---| ---| ---| ---| 
|   7 | Fr. Lynch    | L     |         55 | 1939-03-31 |
|   5 | Mr. Kavanagh | J     |         50 | 1949-11-01 |
|   6 | Mr. Picasso  | J     |         42 | 1939-03-30 |
|   4 | Mr. Hawking  | L     |         40 | 1951-02-19 |
|   2 | Ms. Dubois   | L     |         22 | 1967-09-02 |
|   1 | Mr. Pasteur  | L     |         15 | 1960-02-02 |
|   3 | Ms. Smith    | J     |          4 | 1980-03-23 |

#### SELECT ... FROM ... WHERE... ORDER BY...;

```sql
select * from subject 
where name like "__l%" or name like"___l%" 
order by name;
```
Shows all details of all subjects whose 3rd or 4th letter is “l”, sorted by name. 

| Name      | Teacher      | OnLeavingCert |
 ---| ---| ---| 
| Biology   | Mr. Pasteur  |             1 |
| Colouring | Mr. Picasso  |             0 |
| English   | Mr. Kavanagh |             1 |
| Religion  | Fr. Lynch    |             1 |
| Spelling  | Ms. Smith    |             0 |


### SELECT ... FROM ... WHERE ... IN ( , , , ) ORDER BY ... ;

```sql
select * from teacher 
where experience in (10,15,20,25,30,35,40,45,50,55,60)
order by dob;
```
Shows the names of all teachers with the mentioned number of years experience, sorted from youngest to oldest.


| tid | Name         | level | experience | dob        |
 ---| ---| ---| ---| ---| 
|   7 | Fr. Lynch    | L     |         55 | 1939-03-31 |
|   5 | Mr. Kavanagh | J     |         50 | 1949-11-01 |
|   4 | Mr. Hawking  | L     |         40 | 1951-02-19 |
|   1 | Mr. Pasteur  | L     |         15 | 1960-02-02 |


***

```sql
select * from car;
```

| registration | make               | model   | colour | mileage | engineSize |
 ---| ---| ---| ---| ---| --|
| 10-G-2334    | Toyota             | Corolla | Green  |  123389 |        1.3 |
| 10-WH-17931  | Toyota             | Corolla | Silver |  130389 |        1.4 |
| 11-MO-23431  | Toyota             | Corolla | Black  | 1234123 |        1.3 |
| 12-WH-123    | Ford Motor Company | Ka      | Black  |  125882 |        1.0 |
| 132-MO-19323 | Ford Motor Company | Galaxy  | Silver |    2343 |        1.5 |
| 171-G-39532  | Toyota             | Corolla | Silver |   55882 |        1.3 |
| 171-MO-12533 | Ford Motor Company | Fiesta  | Black  |   25882 |        1.0 |


#### SELECT ... FROM ... WHERE ... AND ( ...OR...);



```sql
select registration, mileage from car 
where mileage > 130000 AND (colour= "Silver" or colour ="Black");
```

| registration | mileage |
 ---| ---| 
| 10-WH-17931  |  130389 |
| 11-MO-23431  | 1234123 |

Shows details for all cars  with mileage greater than 130000 and colour is silver or black.

```sql
 select * from person;
 ```

| personID | name  | age  | sex  | dob        | isStudent |
 ---| ---| ---| ---| ---| --|
|        1 | John  |   24 | M    | 2000-01-01 |         1 |
|        2 | Tom   |   65 | M    | 1958-03-11 |         0 |
|        3 | Mary  |   13 | F    | 2005-04-11 |         1 |
|        4 | Alan  |   13 | M    | 2005-11-21 |         1 |

### AVERAGE

#### SELECT ... AVG() FROM ... WHERE ... AND ...;

Apply the average to the rows selected where the conditions are met.

```SQL
SELECT ROUND(AVG(AGE)) FROM PERSON WHERE SEX ="M" AND AGE <=24;
```

| ROUND(AVG(AGE)) |
--- |
|              17 |

```SQL
SELECT ROUND(AVG(AGE)) FROM PERSON WHERE SEX ="M" AND AGE >=24;
```


| ROUND(AVG(AGE)) |
--- |
|              40 |


#### SELECT ... FROM ... WHERE ... LIKE (' ');

```sql
select * from person where name like ('___');
```

| personID | name | age  | sex  | dob        | isStudent |
 ---| ---| ---| ---| ---| --|
|        2 | Tom  |   65 | M    | 1958-03-11 |         0 |
|        5 | Pat  |   30 | M    | 1993-03-17 |         0 |
|        9 | Pat  |   38 | F    | 1988-04-15 |         0 |

Shows details for persons with exactly 3 letters in their name.

#### SELECT DISTINCT ... FROM ...;


```sql
select distinct(make) from car;
```
| make               |
 ---| 
| Toyota             |
| Ford Motor Company |

#### SELECT ... FROM ... WHERE ... LIKE " " ORDER BY ...;


```sql
select * from car 
where registration like "%-G-%" 
order by mileage asc;

```
Shows all cars registered in Galway, sorted by mileage in ascending order


 registration | make   | model   | colour | mileage | engineSize |
 ---| ---| ---| ---| ---| --|
| 171-G-39532  | Toyota | Corolla | Silver |   55882 |        1.3 |
| 10-G-2334    | Toyota | Corolla | Green  |  123389 |        1.3 |

#### SELECT ... FROM ... WHERE ... NOT IN .. ORDER BY ... LIMIT;

##### Limit


```sql
select * from person 
where month(dob) not in(1,2,3) 
order by month(dob) 
limit 4;
```

Shows all people not born in first 3 months of year, sorted by month order. Only show the first few  records return

personID | name  | age  | sex  | dob        | isStudent |
--- | --- | --- | ---| --- |---|
|        3 | Mary  |   13 | F    | 2005-04-11 |         1 |
|        9 | Pat   |   38 | F    | 1988-04-15 |         0 |
|        7 | Shane |   15 | M    | 2003-06-01 |         1 |
|        6 | Shane |   41 | M    | 1988-07-21 |         0 

```sql
describe employees;
```

Field      | Type          | Null | Key | Default | Extra |
--- | --- | --- | ---| --- |---|
| emp_no     | int(11)       | NO   | PRI | NULL    |       |
| birth_date | date          | NO   |     | NULL    |       |
| first_name | varchar(14)   | NO   |     | NULL    |       |
| last_name  | varchar(16)   | NO   |     | NULL    |       |
| gender     | enum('M','F') | NO   |     | NULL    |       |
| hire_date  | date          | NO   |     | NULL    |       

```sql
describe salaries;
```
Field     | Type    | Null | Key | Default | Extra 
--- | --- | --- | ---| --- |---|
emp_no    | int(11) | NO   | PRI | NULL    |       |
| salary    | int(11) | NO   |     | NULL    |       |
| from_date | date    | NO   | PRI | NULL    |       |
| to_date   | date    | NO   |     | NULL    |       |


The primary key on the salaries table is made up of two composite keys as there could be multiple instances of the employee number and the from_date but you would only have one instance of each emp_no and from_date combination.

```sql
select * from employees
limit 5;
```

| emp_no | birth_date | first_name | last_name | gender | hire_date  |
--- | --- | --- | ---| --- |---| 
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 |
|  10002 | 1964-06-02 | Bezalel    | Simmel    | F      | 1985-11-21 |
|  10003 | 1959-12-03 | Parto      | Bamford   | M      | 1986-08-28 |
|  10004 | 1954-05-01 | Chirstian  | Koblick   | M      | 1986-12-01 |
|  10005 | 1955-01-21 | Kyoichi    | Maliniak  | M      | 1989-09-12 |



```sql
select emp_no, first_name, upper(last_name) as last_name from employees limit 5;
```

| emp_no | first_name | last_name |
| --- | --- | --- |
|  10001 | Georgi     | FACELLO   |
|  10002 | Bezalel    | SIMMEL    |
|  10003 | Parto      | BAMFORD   |
|  10004 | Chirstian  | KOBLICK   |
|  10005 | Kyoichi    | MALINIAK  |

***
### STRING FUNCTIONS: length(), substr(), concat(), format()

```sql
select * from employees 
order by length(last_name), last_name, length(first_name), first_name 
limit 10;
```
This sorts based on the length of last_name, Alphabetical order of last_name, length of first_name, alphabetical order of first name.

The **string function** [`char_length()`](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_char-length) returns the length of a string measured in characters where a multibyte character counts as a single character. 



| emp_no | birth_date | first_name | last_name | gender | hire_date  |
--- | --- | --- | ---| --- |---| 
|  10080 | 1957-12-03 | Premal     | Baek      | M      | 1985-11-19 |
|  10021 | 1960-02-20 | Ramzi      | Erde      | M      | 1988-02-10 |
|  10079 | 1961-10-05 | Kshitij    | Gils      | F      | 1986-03-27 |
|  10009 | 1952-04-19 | Sumant     | Peac      | F      | 1985-02-18 |
|  10018 | 1954-06-19 | Kazuhide   | Peha      | F      | 1987-04-03 |


Show all details of the first 10 employees returned from the database and an extra column called Initials that shows the employee’s initials. 

### concat(), substr()

```sql
select *, concat(substr(first_name,1,1), substr(last_name,1,1)) as Initials from employees limit 5;
```

The [`concat`](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_concat) and [`substr`](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substr) **string functions** are used here to display a new column with the initials of employees. An **alias** is used to name the new column Initials.


| emp_no | birth_date | first_name | last_name | gender | hire_date  | Initials |
--- | --- | --- | ---| --- |---| ---|
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 | GF       |
|  10002 | 1964-06-02 | Bezalel    | Simmel    | F      | 1985-11-21 | BS       |
|  10003 | 1959-12-03 | Parto      | Bamford   | M      | 1986-08-28 | PB       |
|  10004 | 1954-05-01 | Chirstian  | Koblick   | M      | 1986-12-01 | CK       |
|  10005 | 1955-01-21 | Kyoichi    | Maliniak  | M      | 1989-09-12 | KM       |

The `concat` function could be used to create an email address using the first name and last name.

```sql
 select concat(first_name, '.',last_name,"@company.com") as email 
 from employees limit 5;
 ```

| email                         |
--- |
| Georgi.Facello@company.com    |
| Bezalel.Simmel@company.com    |
| Parto.Bamford@company.com     |
| Chirstian.Koblick@company.com |
| Kyoichi.Maliniak@company.com  |



### Format function.
[format()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_format)
```sql
select format(max(mileage),0)
from car 
group by make;
```

| format(max(mileage),0) |
--- |
| 1,234,123              |
| 125,882                |









### Multiple ANDs
Using multiple ANDs here but as there are no ORs being used, brackets are not required for operator precedence .

```sql
select * from employees where gender = "F" 
and year(birth_date) between 1950 and 1959 
and hire_date >= "1988-09-1" 
and hire_date <="1991-02-28";
```


| emp_no | birth_date | first_name | last_name  | gender | hire_date  |
--- | --- | --- | ---| --- |---| 
|  10006 | 1953-04-20 | Anneke     | Preusig    | F      | 1989-06-02 |
|  10007 | 1957-05-23 | Tzvetan    | Zielinski  | F      | 1989-02-10 |
|  10011 | 1953-11-07 | Mary       | Sluis      | F      | 1990-01-22 |
|  10023 | 1953-09-29 | Bojan      | Montemayor | F      | 1989-12-17 |
|  10041 | 1959-08-27 | Uri        | Lenart     | F      | 1989-11-12 |

***
### [Aggregate GROUP BY functions](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)

#### GROUP BY
#### AVG(), MAX()

```sql
select * from person;
```
| personID | name  | age  | sex  | dob        | isStudent |
--- | --- | --- | ---| --- |---|
|        1 | John  |   24 | M    | 2000-01-01 |         1 |
|        2 | Tom   |   65 | M    | 1958-03-11 |         0 |

```sql
select round(avg(age)) from person where sex="M";
```

| round(avg(age)) |
--- |
|              31 |

### Count, group by.

#### SELECT ... , COUNT(*) FROM ... GROUP BY ...;
Does a count based on the group by

```sql
select monthname(dob), count(*)from person 
group by monthname(dob);
```
Shows the number of people born in each month

| monthname(dob) | count(*) |
--- |  ---
| January        |        1 |
| March          |        3 |
| April          |        2 |
| November       |        1 |
| July           |        1 |
| June           |        1 |


#### SELECT AVG() AS ... FROM ... GROUP BY ... LIMIT... 
```sql
select emp_no, round(avg(salary),2) as average_salary from salaries group by emp_no limit 5;

select emp_no, round(max(salary),2) as average_salary from salaries group by emp_no limit 5;
```

| emp_no | average_salary |
--- | ---
|  10001 |          88958 |
|  10002 |          72527 |


| emp_no | average_salary |
--- | ---
|  10001 |       75388.94 |
|  10002 |       68854.50 |

### WHERE 

#### SELECT ... FROM ... WHERE ... AND ... GROUP BY...
```sql
 select emp_no,round(avg(salary),2) from salaries 
 where emp_no in (10001, 10021, 10033, 10087) 
 and salary > 80000 
 group by emp_no;
 ```

| emp_no | round(avg(salary),2) |
--- | ---
|  10001 |             83745.57 |
|  10021 |             83232.00 |
|  10087 |             99015.25 |

This shows the average salaries for these 4 employees, but only including salaries > 80,000 in the average salary calculation.


### HAVING

#### SELECT ... FROM ... GROUP BY ... HAVING AVG()>...`
```sql
SELECT EMP_NO, ROUND(AVG(SALARY) )
FROM SALARIES 
GROUP BY EMP_NO
HAVING AVG(SALARY) >90000;
```
+--------+-------------+
| EMP_NO | AVG(SALARY) |
--- | ---
|  10024 |  90572 |
|  10068 | 101224 |
|  10087 |  99015|

This query shows the average salaries for employees but only showing the average salaries which are over 90000.

```sql
select monthname(birth_date), count(*) 
from employees
 group by monthname(birth_date);
 ```

| monthname(birth_date) | count(*) |
--- | ---
| September             |       13 |
| June                  |        8 |
| December              |        7 |
| May                   |       10 |
| January               |        6 |

***
## CONTROL FLOW FUNCTIONS.

[CONTROL FLOW FUNCTIONS](https://dev.mysql.com/doc/refman/8.0/en/control-flow-functions.html)
**Name**	*Description*

- `CASE`        :	Case operator
- `IF()`        :	If/else construct
- `IFNULL()`    :	Null if/else construct
- `NULLIF()`    :	Return NULL if expr1 = expr2

### IF
```sql
select *,IF(salary>50000,"big","small") as salary_type 
from salaries 
order by from_date 
limit 5;
```

| emp_no | salary | from_date  | to_date    | salary_type |
--- | --- | --- | --- | --- 
|  10009 |  60929 | 1985-02-18 | 1986-02-18 | big         |
|  10048 |  40000 | 1985-02-24 | 1986-02-24 | small       |
|  10098 |  40000 | 1985-05-13 | 1986-05-13 | small       |
|  10070 |  55999 | 1985-10-14 | 1986-10-14 | big         |


A `CASE` statement allows for more options than an `IF` statement which only allows one.

An alias can be used for the names of the column for printing as otherwise the whole case when statement will show as the column name. However the alias does not change the actual table.



```sql
SELECT *, IF(MILEAGE>500000,"30%","") Discount 
FROM car;
```

| registration | make               | model   | colour | mileage | engineSize | Discount |
---| --- | --- | --- | --- | --- |---|
| 10-G-2334    | Toyota             | Corolla | Green  |  123389 |        1.3 |          |
| 10-WH-17931  | Toyota             | Corolla | Silver |  130389 |        1.4 |          |
| 11-MO-23431  | Toyota             | Corolla | Black  | 1234123 |        1.3 | 30%      |
| 12-WH-123    | Ford Motor Company | Ka      | Black  |  125882 |        1.0 |          |

Note `as` is not required when using an alias to rename a column that is returned.
It will not actually change the table. 

### IF 

```sql
select emp_no as ID, if (gender="M","Mr.","Ms.") as Title, first_name as Name, last_name as Surname, gender 
from employees 
order by emp_no limit 5;
```

| ID    | Title | Name      | Surname  | gender |
---| --- | --- | --- | --- 
| 10001 | Mr.   | Georgi    | Facello  | M      |
| 10002 | Ms.   | Bezalel   | Simmel   | F      |
| 10003 | Mr.   | Parto     | Bamford  | M      |
| 10004 | Mr.   | Chirstian | Koblick  | M      |
| 10005 | Mr.   | Kyoichi   | Maliniak | M      |


### CASE WHEN 


```sql
select emp_no, max(salary), 
case 
    when max(salary) < 40000 then "30%" 
    when max(salary) < 60000 then "40%" 
    when max(salary) < 80000 then "50%" 
    else "60%" 
END as "Tax bracket" 
from salaries 
group by emp_no 
order by max(salary) 
limit 10;
```

| emp_no | max(salary) | Tax bracket |
---| --- | --- |
|  10015 |       40000 | 40%         |
|  10048 |       40000 | 40%         |
|  10022 |       41348 | 40%         |

### CASE WHEN
```sql
select *, 
case 
    when engineSize <=1.0 then "Small" 
    when engineSize between 1.1 and 1.3 then "Medium" 
    when engineSize > 1.3 then "Large" 
END as size 
from car;
```

 registration | make        | model   | colour | mileage | engineSize | size
---| --- | --- | --- | --- |---| --- |
| 10-G-2334    | Toyota             | Corolla | Green  |  123389 |        1.3 | Medium |
| 10-WH-17931  | Toyota             | Corolla | Silver |  130389 |        1.4 | Large  |
| 11-MO-23431  | Toyota             | Corolla | Black  | 1234123 |        1.3 | Medium |
| 12-WH-123    | Ford Motor Company | Ka      | Black  |  125882 |        1.0 | Small  |

### CASE WHEN
```sql
select first_name,  birth_date, 
case 
    when month(birth_date)in(1,2,3) then "q1 baby" 
    when month(birth_date)in (4,5,6) then "q2 baby" 
    when month(birth_date) in (7,8,9) then "q3 baby" 
    else "q4 baby" 
end as birthQ 
from employees limit 5;
```

| first_name | birth_date | birthQ  |
--- | --- | ---
| Georgi     | 1953-09-02 | q3 baby |
| Bezalel    | 1964-06-02 | q2 baby |
| Parto      | 1959-12-03 | q4 baby |
| Chirstian  | 1954-05-01 | q2 baby |
| Kyoichi    | 1955-01-21 | q1 baby |


```sql
select name, isStudent,age, 
case  
    when isStudent=1 and age >23 then "mature student" 
    when isStudent=1 and age <=23 then "ordinary student"
    else "Not" 
    end as "student status" 
    from person limit 5;
```

| name | isStudent | age  | student status   |
---| --- | --- | --- |
| John |         1 |   24 | mature student   |
| Tom  |         0 |   65 | Not              |
| Mary |         1 |   13 | ordinary student |
| Alan |         1 |   13 | ordinary student |
| Pat  |         0 |   30 | Not              |

#### CASE WHEN

```sql
select *, 
case 
    when age < 20 then "under20" 
    when age < 30 then "under30" 
    when age < 40 then "under40" 
    else "over40" 
    end as "age-cat" 
    from person;
```
(use the correct order when writing the case when.)

personID | name     | age  | sex  | dob        | isStudent | age-cat |
| --- | --- | --- | --- | --- | --- | --- |
|        2 | Mr.Tom   |   66 | M    | 1958-03-11 |         0 | over40  |
|        3 | Ms.Mary  |   14 | F    | 2005-04-11 |         1 | under20 |
|        4 | Mr.Alan  |   14 | M    | 2005-11-21 |         1 | under20 |
|        5 | Mr.Pat   |   31 | M    | 1993-03-17 |         0 | under40 |
|        6 | Mr.Shane |   42 | M    | 1988-07-21 |         0 | over40  |
|        7 | Mr.Shane |   16 | M    | 2003-06-01 |         1 | under20 |
|        8 | Ms.Alice |   26 | F    | 1999-03-01 |         1 | under30 |
|        9 | Ms.Pat   |   32 | F    | 1988-04-15 |         0 | under40 |
|       10 | Johan    |   34 | M    | NULL       |      NULL | under40 |
|       11 | Jonh     |   23 | M    | NULL       |         1 | under30 






***

## DATE AND TIME FUNCTIONS.

[DATEDIFF()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_datediff)


### DATEDIFF

```SQL
SELECT *, if(DATEDIFF(to_DATE,from_DATE) <365, "under 1 year","over 1 year") as Time 
FROM SALARIES 
LIMIT 5;
```

| emp_no | salary | from_date  | to_date    | Time        |
--- | --- | --- | ---| --- |
|  10001 |  60117 | 1986-06-26 | 1987-06-26 | over 1 year |
|  10001 |  62102 | 1987-06-26 | 1988-06-25 | over 1 year |
|  10001 |  66074 | 1988-06-25 | 1989-06-25 | over 1 year |
|  10001 |  66596 | 1989-06-25 | 1990-06-25 | over 1 year |
|  10001 |  66961 | 1990-06-25 | 1991-06-25 | over 1 year |

### DATE AND TIME FORMAT FUNCTIONS
[DATE_FORMAT](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format)

`date_format(date, format)`

A sample of the specifiers here:


**Specifier**	*Description*
- `%a` :	Abbreviated weekday name (Sun..Sat)
- `%b` :	Abbreviated month name (Jan..Dec)
- `%c` :	Month, numeric (0..12)
- `%D` :	Day of the month with English suffix (0th, 1st, 2nd, 3rd, …)
- `%d` :	Day of the month, numeric (00..31)
- `%H` :	Hour (00..23)
- `%h`: 	Hour (01..12)
- `%M`: 	Month name (January..December)
- `%m`: 	Month, numeric (00..12)
- `%p`: 	AM or PM
- `%S`: 	Seconds (00..59)
- `%T`: 	Time, 24-hour (hh:mm:ss)
- `%W`: 	Weekday name (Sunday..Saturday)
- `%Y`: 	Year, numeric, four digits
- `%y`: 	Year, numeric (two digits)

The format strings should be in quotes.

```sql
select NAME, date_format(dob, "%a, %b %D %Y") FROM PERSON;
```

| NAME  | date_format(dob, "%a, %b %D %Y") |
--- | ---
| John  | Sat, Jan 1st 2000                |
| Tom   | Tue, Mar 11th 1958               |
| Mary  | Mon, Apr 11th 2005               |
| Alan  | Mon, Nov 21st 2005               |


```sql
select first_name as first, gender as G 
from employees limit 3;
```

| first   | G |
--- | ---
| Georgi  | M |
| Bezalel | F |
| Parto   | M |

***


### FUNCTIONS AND PROCEDURES

- When writing functions and procedures, the delimiter  must be changed to `//` before writing a function or procedure. This allows the `;` to be used as part of the code and not to signify the end of a statement.

- Before writing the function or procedure, write it as a query.
- A function is **deterministic** if it doesn't chanhe any data.

```sql
select *, round(datediff(hire_date, birth_date)/365,1) as age 
from employees limit 5;
```

Using a function show all columns from the employees table, and a column entitled “Age” which is the age the employee was when he or she was hired. The age should be rounded to 1 digit after the decimal place.

```sql 
DELIMITER //
CREATE FUNCTION getAges(hd date, bd date)
    -> RETURNS varchar(5)
    -> DETERMINISTIC
    -> BEGIN
    -> RETURN format(datediff(hd,bd)/365,1);
    -> END
    -> //
```
```SQL
delimiter ;
select *, getAges(hire_date, birth_date) as Age_at_hiring
from employees
limit 5;
```


| emp_no | birth_date | first_name | last_name | gender | hire_date  | Age_at_hiring |
--- | --- | --- | ---| --- |---| ---| 
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 | 32.8          |
|  10002 | 1964-06-02 | Bezalel    | Simmel    | F      | 1985-11-21 | 21.5          |
|  10003 | 1959-12-03 | Parto      | Bamford   | M      | 1986-08-28 | 26.8          |
|  10004 | 1954-05-01 | Chirstian  | Koblick   | M      | 1986-12-01 | 32.6          |
|  10005 | 1955-01-21 | Kyoichi    | Maliniak  | M      | 1989-09-12 | 34.7          |

This procedure takes two parameters, one for a year and the other a month and returns all employees hired in specified year and month. 

```sql
delimiter //
mysql> CREATE PROCEDURE hires(y integer, m integer)
    -> DETERMINISTIC
    -> BEGIN
    -> SELECT * FROM employees
    -> WHERE year(hire_date)=y AND month(hire_date)=m;
    -> END
    -> //
```

This procedure returns all employees hired in the specified year if the month parameter is NULL.
 
```sql
delimiter //
mysql> create procedure hires2(y integer, m integer)
    -> DETERMINISTIC 
    -> BEGIN
    -> IF m is NULL THEN
    -> SELECT * FROM EMPLOYEES WHERE YEAR(hire_date)=y;
    -> else
    -> select * from employees where year(hire_date) = y and month(hire_date)=m;
    -> end if;
    -> end
    -> //
```

```sql
mysql> delimiter ;
call hires2(1995,null);
```

 emp_no | birth_date | first_name | last_name   | gender | hire_date  |
--- | --- | --- | ---| --- |---|
|  10016 | 1961-05-02 | Kazuhito   | Cappelletti | M      | 1995-01-27 |
|  10022 | 1952-07-08 | Shahaf     | Famili      | M      | 1995-08-22 |
|  10026 | 1953-04-03 | Yongqiao   | Berztiss    | M      | 1995-03-20 |

 ```sql
 call hires2(1995,3);
 ```
+
| emp_no | birth_date | first_name | last_name | gender | hire_date  |
--- | --- | --- | ---| --- |---| 
|  10026 | 1953-04-03 | Yongqiao   | Berztiss  | M      | 1995-03-20 |
|  10054 | 1957-04-04 | Mayumi     | Schueller | M      | 1995-03-13 |


To check if a parameter is NULL  `IF M IS NULL THEN`
To check if a parameter is not NULL `IF M IS NOT NULL THEN`.

***
```sql
 select * from person;
 ```

| personID | name  | age  | sex  | dob        | isStudent |
--- | --- | --- | ---| --- |---| 
|        1 | John  |   24 | M    | 2000-01-01 |         1 |
|        2 | Tom   |   65 | M    | 1958-03-11 |         0 |
|        3 | Mary  |   13 | F    | 2005-04-11 |         1 |
|        4 | Alan  |   13 | M    | 2005-11-21 |         1 |
|        5 | Pat   |   30 | M    | 1993-03-17 |         0 |

### Function
```sql
describe person;
```

| Field     | Type          | Null | Key | Default | Extra          |
--- | --- | --- | ---| --- |---| 
| personID  | int(11)       | NO   | PRI | NULL    | auto_increment |
| name      | varchar(20)   | NO   |     | NULL    |                |
| age       | int(11)       | YES  |     | NULL    |                |
| sex       | enum('M','F') | YES  |     | M       |                |
| dob       | date          | YES  |     | NULL    |                |
| isStudent | tinyint(1)    | YES  |     | NULL    |                |

This function determines if a person is a student based on age and isStudent status.


```sql
delimiter //
create function st(a int(11) iss TINYINT(11))
RETURNS VARCHAR(10)
DETERMINISTIC
BEGIN
if iss and a< 23 then
    return "Ordinary";
elseif iss and     a >=23 then 
    return "Mature";
else 
    return "";
end if;
end
//

delimiter ;

```
To call the function, pass in the columns from the persons tables, which takes the values for each field and passes them as the parameters to the function.


```sql
select st(16,0);

select *, st(age, isStudent) as "Student Type" from person;
```

### CREATE PROCEDURE
Write a procedure that accepts two parameters. A comparison operator < > = and an Age.
If the comparison operator is >, the procedure returns all details of a person older than the age.

passing in a string of one or a varchar with the '>', '<. or '=' operator.
make age the same data type as the age in the table

Note that the `return` keyword is not allowed in a procedure. It is allowed in a function. Using `select`.
Can put the if statement in parentheses but not required.

```sql
delimiter //
create procedure comp(c varchar(1) , a int(11))
deterministic
begin   
    if (c = "<") then 
        select * from person where age < a;
    elseif (x = ">") then
        select * from person where age > a;
    else
        select * from person where age = a;
    end if;
end 
//

delimiter;
```
call comp("<",3);

Use `drop procedure  <procedure name>` to delete a procedure and create it again if a change to the code is required.

`drop procedure comp`
once the procedure is written, change the delimiter back to ;. Then the procedure can be called from memory to be used.
`call <procedure name>(arguments)`

***
### Normalisation
```sql
describe doctor_table;
```

| Field    | Type        | Null | Key | Default | Extra |
--- | --- | --- | ---| --- |---| 
| doctorID | int(11)     | NO   | PRI | NULL    |       |
| name     | varchar(50) | YES  |     | NULL    |       |
| phone    | int(11)     | YES  |     | NULL    |       |

```sql
describe patient_table;
```

| Field      | Type         | Null | Key | Default | Extra |
--- | --- | --- | ---| --- |---|
| ppsn       | varchar(10)  | NO   | PRI | NULL    |       |
| first_name | varchar(50)  | YES  |     | NULL    |       |
| surname    | varchar(50)  | YES  |     | NULL    |       |
| address    | varchar(200) | YES  |     | NULL    |       |
| doctorID   | int(11)      | YES  | MUL | NULL    |       |

```sql
show create table patient_table
```
```sql
CREATE TABLE `patient_table` (
  `ppsn` varchar(10) NOT NULL,
  `first_name` varchar(50) DEFAULT NULL,
  `surname` varchar(50) DEFAULT NULL,
  `address` varchar(200) DEFAULT NULL,
  `doctorID` int(11) DEFAULT NULL,
  PRIMARY KEY (`ppsn`),
  KEY `doctorID` (`doctorID`),
  CONSTRAINT `patient_table_ibfk_1` FOREIGN KEY (`doctorID`) REFERENCES `doctor_table` (`doctorid`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 
```



```sql
show create table doctor_table;
```

```sql
CREATE TABLE `doctor_table` (
  `doctorID` int(11) NOT NULL,
  `name` varchar(50) DEFAULT NULL,
  `phone` int(11) DEFAULT NULL,
  PRIMARY KEY (`doctorID`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1
```

The doctor id in the patient table is a foreign key referring the doctorid in the doctor table.
Therefore any integers we put in as doctor id in the patient table must already exist in the doctor table doctor id column.

```SQL
select * from doctor_table;
```


| doctorID | name       | phone |
--- | --- | --- |
|      100 | Dr. Jones  | 12345 |
|      101 | Dr. Murphy | 88335 |
|      102 | Dr. Rice   | 64727 |

```SQL
select * from patient_table;
```

| ppsn     | first_name | surname  | address   | doctorID |
--- | --- | --- | ---| --- |
| 2344234S | Mary       | Burke    | Galway    |     NULL |
| 7629913X | John       | Smyth    | Athlone   |      100 |
| 989333F  | Alan       | Mulligan | Galway    |      101 |
| 9898823W | Fred       | Collins  | Castlebar |      100 |


### String function.
#### SUBSTR()

```sql
select substr(name,5) 
from doctor_table;
```

Here the `substr` function selects from position 5 so strips out the title to return just the name.

```sql
select substr(name,5) 
from doctor_table;
```

### INNER JOIN
```sql
select pt.*, dt.* from patient_table pt 
inner join doctor_table dt
on pt.doctorID = dt.doctorid; 
```

This query shows all details of all patients with associated doctors.

 ppsn     | first_name | surname  | address   | doctorID | doctorID | name       | phone |
--- | --- | --- | ---| --- |---| ---| ---| 
| 7629913X | John       | Smyth    | Athlone   |      100 |      100 | Dr. Jones  | 12345 |
| 9898823W | Fred       | Collins  | Castlebar |      100 |      100 | Dr. Jones  | 12345 |
| 989333F  | Alan       | Mulligan | Galway    |      101 |      101 | Dr. Murphy | 88335 |


### INNER JOIN
#### SELECT ... FROM ... INNER JOIN  .. ON ...=... WHERE... ORDER BY...
```sql
SELECT dt.name, dt.phone, pt.ppsn, pt.first_name, pt.surname
FROM doctor_table dt
INNER JOIN patient_table pt
on pt.DoctorID = dt.Doctorid
where dt.name = "Dr. Jones"
order by pt.surname;
```

This query returns the details of patients treated by a particular doctor.


name      | phone | ppsn     | first_name | surname |
--- | --- | --- | ---| --- |
| Dr. Jones | 12345 | 9898823W | Fred       | Collins |
| Dr. Jones | 12345 | 7629913X | John       | Smyth   |


### DISTINCT

#### Select distinct() from ... inner join ... on  ... = ... ;
```sql
select distinct(dt.name)
from doctor_table dt
inner join patient_table pt
on dt.DoctorId = pt.Doctorid;
```
This query returns the unique names of doctors who are treating patients.

### LEFT JOIN

### NULL
```sql
 select pt.ppsn, pt.surname, pt.first_name, dt.name from patient_table pt  left join doctor_table dt on pt.Doctorid= dt.doctorid;
 ```
 This query returns null for the doctor name where a patient does not have a doctor. Where the doctorID is NULL, the patient isn't currently being treated by a doctor
 
| ppsn     | surname  | first_name | name       |
--- | --- | --- | ---| 
| 2344234S | Burke    | Mary       | NULL       |
| 7629913X | Smyth    | John       | Dr. Jones  |
| 989333F  | Mulligan | Alan       | Dr. Murphy |
| 9898823W | Collins  | Fred       | Dr. Jones  |

### LEFT JOIN vs INNER JOIN

INNER JOIN only returns rows where the condition is met while LEFT JOIN returns all rows from the first table with a NULL for the field where the condition is NOT met.
INNER JOIN excludes rows where the condition is not met.
- to show all details of all doctors from one table with the details of their patients from the patients_table, use a left join as this will return all rows from the first table with a null value for rows in the second table where the condition is not met.
- an inner join would omit the rows where the condition is not met

#### LEFT JOIN
```sql
select pt.first_name, pt.surname, dt.name 
from patient_table pt 
left join doctor_table dt 
on pt.doctorid = dt.doctorid;
```

| first_name | surname  | name       |
--- | --- | --- | 
| Mary       | Burke    | NULL       |
| John       | Smyth    | Dr. Jones  |
| Alan       | Mulligan | Dr. Murphy |
| Fred       | Collins  | Dr. Jones  |

#### INNER JOIN
```sql
select pt.first_name, pt.surname, dt.name 
from patient_table pt 
inner  join doctor_table dt 
on pt.doctorid = dt.doctorid;
```


| first_name | surname  | name       |
--- | --- | --- | 
| John       | Smyth    | Dr. Jones  |
| Fred       | Collins  | Dr. Jones  |
| Alan       | Mulligan | Dr. Murphy |


```sql
select dt.*, pt.surname 
from doctor_table as dt
left join patient_table pt
on dt.DoctorID = pt.DoctorID
order by dt.name, pt.surname;
```

| doctorID | name       | phone | surname  |
--- | --- | --- | ---| 
|      100 | Dr. Jones  | 12345 | Collins  |
|      100 | Dr. Jones  | 12345 | Smyth    |
|      101 | Dr. Murphy | 88335 | Mulligan |
|      102 | Dr. Rice   | 64727 | NULL     |


```sql
select pt.first_name, pt.surname, dt.name from patient_table pt
inner join doctor_table dt 
on pt.doctorid = dt.doctorid 
where pt.first_name ="Alan";
```


| first_name | surname  | name       |
--- | --- | --- |
| Alan       | Mulligan | Dr. Murphy |

### LEFT JOIN
#### left join to return every row from the patient_table even if no doctor associated.
```sql
select pt.ppsn, pt.first_name, pt.surname, dt.name, dt.phone 
from patient_table pt 
left join doctor_table dt 
on pt.doctorid = dt.doctorid;
```

returns all patients from the patient_table with details of doctor they are attending if any.

| ppsn     | first_name | surname  | name       | phone |
--- | --- | --- | ---| --- |
| 2344234S | Mary       | Burke    | NULL       |  NULL |
| 7629913X | John       | Smyth    | Dr. Jones  | 12345 |
| 989333F  | Alan       | Mulligan | Dr. Murphy | 88335 |
| 9898823W | Fred       | Collins  | Dr. Jones  | 12345 |


### SHOW CREATE TABLE;
```sql
show create table manufacturer;
```

```SQL
manufacturer CREATE TABLE `manufacturer` (  
    `manu_code` varchar(3) NOT NULL,
    `manu_name` varchar(200) NOT NULL,
    `manu_details` varchar(400) DEFAULT NULL,
    PRIMARY KEY (`manu_code`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 
```

```sql
show create table vehicles;
```

```SQL
vehicle CREATE TABLE `vehicle` (
  `reg` varchar(20) NOT NULL,
  `manu_code` varchar(3) NOT NULL,
  `mileage` int(11) DEFAULT NULL,
  `price` decimal(8,2) NOT NULL,
  `colour` varchar(20) NOT NULL,
  `fuel` enum('petrol','diesel') DEFAULT NULL,
  PRIMARY KEY (`reg`),
  KEY `vehicle_ibfk_1` (`manu_code`),
  CONSTRAINT `vehicle_ibfk_1` FOREIGN KEY (`manu_code`) REFERENCES `manufacturer` (`manu_code`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1 
```

### Relationships between tables through foreign key:

The `manfacturer` table and the `vehicles` table are related through the `manu_code` field in the `vehicles` table which is a foreign key that references the `manu_code` field in the `manufacturer` table.

```sql
 select * from manufacturer;
 ```

  manu_code | manu_name      | manu_details           
| --- |---| --
| FOR       | Ford           | The Ford Motor Company is an American multinational automaker headquartered in Dearborn, Michigan, a suburb of Detroit. It was founded in 1903  |
| GM        | General Motors | General Motors is an American multinational automaker headquartered in Detroit, Michigan. It was founded in 1908                                |
| NIS       | Nissan         | Nissan Motor Company Ltd is a Japanese multinational automobile manufacturer headquartered in Nishi-ku, Yokohama, Japan. It was founded in 1934 |
| TOY       | Toyota         | Toyota Motor Corporation is a Japanese automotive manufacturer headquartered in Toyota, Aichi, Japan. It was founded in 1937                    |
| VOL       | Volkswagen     | Volkswagen is a German automaker headquartered in Wolfsburg, Germany. It was founded in 1937                                                    |

```sql
select * from vehicle;

```

 reg          | manu_code | mileage | price    | colour | fuel   |
--- | --- | --- | ---| --- |---| 
| 2003-LM-201  | TOY       |  170000 |  3500.50 | Red    | petrol |
| 2009-RN-12   | FOR       |   98242 |  2500.00 | Red    | petrol |
| 2010-G-13345 | TOY       |   50000 |  8599.00 | Silver | petrol |
| 2011-G-995   | FOR       |   33500 |  8500.00 | Blue   | petrol |
| 2011-WH-2121 | FOR       |   55998 | 14000.00 | Black  | diesel |
| 2014-WH-2189 | FOR       |   12553 | 11000.00 | Blue   | diesel |
| 2016-D-12345 | TOY       |    3456 | 15000.00 | Red    | petrol 

### STRING FUNCTIONS:
### CONCAT(), SUBSRT()
```sql
select manu_code, manu_name, concat(substr(manu_details,1,10),"...")
from manufacturer;
``` 

manu_code | manu_name      | concat(substr(manu_details,1,10),"...") |
--- | --- | --- | 
| FOR       | Ford           | The Ford M...                           |
| GM        | General Motors | General Mo...                           |
| NIS       | Nissan         | Nissan Mot...                           |
| TOY       | Toyota         | Toyota Mot...                           |
| VOL       | Volkswagen     | Volkswagen...          

#### Length

```sql
select length(manu_details) 
from manufacturer;
```

| length(manu_details) |
| --- |
|                  142 |
|                  112 |
|                  143 |
|                  124 |
|                   92 |

 ```sql
 select avg(length(manu_details)) from manufacturer;
 ```

| avg(length(manu_details)) |
| --- |   
               122.6000 |

```sql
select format(avg(length(manu_details)),0) as "Length" 
from manufacturer;
```

This shows the average length of the manu_name formatted to 0 decimal places.

| Length |
| --- |
| 123    |

```sql
select *, if(fuel="petrol","1,45","1.30") as cost 
from vehicle;
```

This query includes a column called “cost” which has the value 1.45 if the fuel is petrol otherwise has the value 1.30.

### JOINING TABLES TO GET DATA FROM MULTIPLE TABLES


The `vehicle` table has a foreign key `manu_code` referencing the `manu_code` field in the `manafacturer` table.
```sql
 **KEY `vehicle_ibfk_1` (`manu_code`),**
  **CONSTRAINT `vehicle_ibfk_1` FOREIGN KEY (`manu_code`) REFERENCES `manufacturer` (`manu_code`)**
```


### INNER JOIN


```sql
select m.manu_code, m.manu_name, v.reg
    from manufacturer m
    inner join vehicle v
    on m.manu_code = v.manu_code;
```

This query only returns rows where the condition is met, so only returns rows from both tables which have matching manufacturer code.

| manu_code | manu_name | reg          |
 --- | --- | --- |
| FOR       | Ford      | 2009-RN-12   |
| FOR       | Ford      | 2011-G-995   |
| FOR       | Ford      | 2011-WH-2121 |
| FOR       | Ford      | 2014-WH-2189 |
| TOY       | Toyota    | 2003-LM-201  |
| TOY       | Toyota    | 2010-G-13345 |
| TOY       | Toyota    | 2016-D-12345 |

### LEFT JOIN

A left join will return all rows from the first table, whereas an inner join will only return rows from both tables where the conditions are met.
If the join condition isn't met then a left join will still return all rows from the first table but with null values for the second table fields.

```sql
select m.manu_code, m.manu_name, v.reg
from manufacturer m
left join vehicle v
on m.manu_code = v.manu_code;
```

This query returns all rows from the first table, with Null values for the fields from the second table where the conditions are not met.


| manu_code | manu_name      | reg          |
--- | --- | --- |
| FOR       | Ford           | 2009-RN-12   |
| FOR       | Ford           | 2011-G-995   |
| FOR       | Ford           | 2011-WH-2121 |
| FOR       | Ford           | 2014-WH-2189 |
| GM        | General Motors | NULL         |
| NIS       | Nissan         | NULL         |
| TOY       | Toyota         | 2003-LM-201  |
| TOY       | Toyota         | 2010-G-13345 |
| TOY       | Toyota         | 2016-D-12345 |
| VOL       | Volkswagen     | NULL         |

10 rows in set (0.01 sec)



### LEFT JOIN vs INNER JOIN 


```sql
SELECT m.manu_code, m.manu_name, v.reg from manufacturer m 
inner join vehicle v 
on m.manu_code = v.manu_code;
```
This query will return less rows that the same query using a left join as it excludes the rows where the condtions are not met.


| manu_code | manu_name | reg          |
--- | --- | --- |
| FOR       | Ford      | 2009-RN-12   |
| FOR       | Ford      | 2011-G-995   |
| FOR       | Ford      | 2011-WH-2121 |
| FOR       | Ford      | 2014-WH-2189 |
| TOY       | Toyota    | 2003-LM-201  |
| TOY       | Toyota    | 2010-G-13345 |
| TOY       | Toyota    | 2016-D-12345 |

***

### STORED PROCEDURE

The `show create table` on vehicles shows that the vehicles table has a foreign key referencing the manufacturer table. 

```sql
KEY `vehicle_ibfk_1` (`manu_code`),
  CONSTRAINT `vehicle_ibfk_1` FOREIGN KEY (`manu_code`) REFERENCES `manufacturer` (`manu_code`)
```


The manufacturer table has no foreign key constraint.

Write the code first for a query

```sql
 select v.reg, v.manu_code, m.manu_name, v.mileage, v.price
    -> from vehicle v
    -> inner join manufacturer m
    -> on v.manu_code = m.manu_code
    -> where v.price < 10000;
```

| reg          | manu_code | manu_name | mileage | price   |
--- | --- |--- | --- | --- |
| 2003-LM-201  | TOY       | Toyota    |  170000 | 3500.50 |
| 2009-RN-12   | FOR       | Ford      |   98242 | 2500.00 |
| 2010-G-13345 | TOY       | Toyota    |   50000 | 8599.00 |
| 2011-G-995   | FOR       | Ford      |   33500 | 8500.00 |

This query returns the registration, manufacturer code and name, mileage and price for each car with mileage where the codes match in both tables and where the price is less than 10000 

```sql
PROCEDURE `price_less_than`(p decimal(8,2))
    DETERMINISTIC
BEGIN
select v.reg, v.manu_code,m.manu_name,v.mileage, v.price
from vehicle v
inner join manufacturer m
on v.manu_code = m.manu_code
where v.price <p
order by v.price;
END
```

This procedure returns the specified details for all vehicles where the price is less than a particular price provided as an argument to the procedure.

### CALLING A PROCEDURE

```SQL
call price_less_than(10000);
```

| reg          | manu_code | manu_name | mileage | price   |
--- | --- |--- | --- | --- |
| 2009-RN-12   | FOR       | Ford      |   98242 | 2500.00 |
| 2003-LM-201  | TOY       | Toyota    |  170000 | 3500.50 |
| 2011-G-995   | FOR       | Ford      |   33500 | 8500.00 |
| 2010-G-13345 | TOY       | Toyota    |   50000 | 8599.00 |


***

# CRUD functions
- Create/Insert
- Read
- Update 
- Delete

```sql
describe bus
```

 Field         | Type                               | Null | Key | Default | Extra |
 --- | --- | --- | --- | --- | --- |
| reg           | varchar(15)                        | NO   | PRI | NULL    |       |
| maxPassengers | int(11)                            | YES  |     | NULL    |       |
| fuel          | enum('Diesel','Petrol','Electric') | YES  |     | Diesel  |    


```sql
SHOW create table bus
```

```sql
BUS   | CREATE TABLE `BUS` (
  `reg` varchar(15) NOT NULL,
  `maxPassengers` int(11) DEFAULT NULL,
  `fuel` enum('Diesel','Petrol','Electric') DEFAULT 'Diesel',
  PRIMARY KEY (`reg`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1
```

```sql
describe driver;

```
 Field     | Type        | Null | Key | Default | Extra |
 --- | --- | --- | --- | --- | --- |
| licenceNo | varchar(20) | NO   | PRI | NULL    |       |
| name      | varchar(30) | YES  |     | NULL    |       |
| busReg    | varchar(15) | YES  | MUL | NULL    |   


```sql
show create table driver
```

```sql
CREATE TABLE `driver` (
  `licenceNo` varchar(20) NOT NULL,
  `name` varchar(30) DEFAULT NULL,
  `busReg` varchar(15) DEFAULT NULL,
  PRIMARY KEY (`licenceNo`),
  KEY `busReg` (`busReg`),
  **CONSTRAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus` (`reg`) ON DELETE CASCADE**
) ENGINE=InnoDB DEFAULT CHARSET=latin1
```

`describe car;`

| Field        | Type        | Null | Key | Default | Extra |
 --- | --- | --- | --- | --- | --- |
| registration | varchar(15) | NO   | PRI | NULL    |       |
| make         | varchar(20) | YES  |     | NULL    |       |
| model        | varchar(20) | YES  |     | NULL    |       |
| colour       | varchar(10) | YES  |     | NULL    |       |
| mileage      | int(11)     | YES  |     | NULL    |       |
| engineSize   | float(2,1)  | YES  |     | NULL    |       |

```sql
show create table car;
```

```sql
CREATE TABLE `car` (
  `registration` varchar(15) NOT NULL,
  `make` varchar(20) DEFAULT NULL,
  `model` varchar(20) DEFAULT NULL,
  `colour` varchar(10) DEFAULT NULL,
  `mileage` int(11) DEFAULT NULL,
  `engineSize` float(2,1) DEFAULT NULL,
  PRIMARY KEY (`registration`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
```


```sql
describe person
```
Field     | Type          | Null | Key | Default | Extra          |
 --- | --- | --- | --- | --- | --- |
| personID  | int(11)       | NO   | PRI | NULL    | auto_increment |
| name      | varchar(20)   | NO   |     | NULL    |                |
| age       | int(11)       | YES  |     | NULL    |                |
| sex       | enum('M','F') | YES  |     | M       |                |
| dob       | date          | YES  |     | NULL    |                |
| isStudent | tinyint(1)    | YES  |     | NULL    

```sql
show create table person
```

```sql
CREATE TABLE `person` (
  `personID` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  `age` int(11) DEFAULT NULL,
  `sex` enum('M','F') DEFAULT 'M',
  `dob` date DEFAULT NULL,
  `isStudent` tinyint(1) DEFAULT NULL,
  PRIMARY KEY (`personID`)
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci 
```

***


### INSERT
When entering values for all the fields there is no need to specify the fields.

### INSERT into ...  values ()

### INSERT INTO TABLE (..,..,..,) VALUES (.., .. ,..);


```sql
INSERT into person values(“John”,23,”Male”, true);
```

This will result in an error as there are 5 columns and it will not know which values are for which columns. Specify the associated values.

*Column count doesn't match value count at row 1*


### INSERT -  error if no value supplied for a primary key which cannot be null (and it doesn't auto-increment)
```sql
insert into driver(name) values ("Mary");
```
results in an error:
`Error code:1364  Field 'LicenceNo` doesn't have a default value.`

The `describe driver` command shows thay `LicenceNo` is a **primary key** and it cannot be NULL.

`describe driver;` shows that `LicenceNo` is a primary key and it cannot be `NULL` therefore 


| Field     | Type        | Null | Key | Default | Extra |
| --- | --- | --- | --- | --- | --- |
| licenceNo | varchar(20) | NO   | PRI | NULL    |       |
| name      | varchar(30) | YES  |     | NULL    |       |
| age       | int(11)     | YES  |     | NULL    |       |
| busReg    | varchar(15) | YES  | MUL | NULL    |       |

.
```sql
insert into driver(name, licenceNo) values ("Bob","RN2423");
```
This adds a new row with for the two columns not supplied with values.

### INSERT - Error as foreign key constraint fails - when the foreign key doesn't exist on the other table
```sql
insert into driver(name, licenceNo, busReg) values ("Gillian","W12X45","201-G-123");
```
Results in an error as the bus reg does not already exist in the bus table.

*Cannot add or update a child row: a foreign key constraint fails (`bus`.`driver`, CONSTRAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus` (`reg`) ON DELETE CASCADE)*

### INSERT - Error  as duplicate entry for the primary key already used for another row.
Cannot have the same primary key  as another row.
```sql
insert into bus(reg, maxPassengers, fuel) values("12-G-1323",34, "Diesel");
```

**ERROR 1062 (23000): Duplicate entry '12-G-1323' for key 'PRIMARY'**

### INSERT - Error Data truncated ... 

```sql
insert into bus values("191-D-45890", 120, "Ethanol");
```
ERROR 1265 (01000): Data truncated for column 'fuel' at row 1

```sql
describe bus
```

| Field         | Type                               | Null | Key | Default | Extra |
| --- | --- | --- | --- | --- | --- |
| reg           | varchar(15)                        | NO   | PRI | NULL    |       |
| maxPassengers | int(11)                            | YES  |     | NULL    |       |
| fuel          | **enum('Diesel','Petrol','Electric')** | YES  |     | Diesel  | 

The Type for the `Fuel` field is **ENUM** which is a list of permitted values that are enumerated explicitly at the table creation time. See[Section 11.3.5  The Enum Type](https://dev.mysql.com/doc/refman/8.0/en/enum.html). There are only three possible values for fuel allowed which doesn't include ethanol. The fuel Field is of Type (enum("Diesel","Petrol","Electric")).



### UPDATE ...SET ... CASE WHEN
```sql
update person
set age = 
case
    when age is null then 18
    else age +1
end;
```
### UPDATE ... SET ... WHERE ... = ...;

```sql
update car 
set make = "Ford Motors" 
where make = "Ford";

```

```SQL
select * from car;
```

| registration | make        | model      | colour | mileage | engineSize |
 --- | --- | --- | --- | --- | --- |
| 05-MO-17931  | Toyota      | Highlander | Green  |  253789 |        1.6 |
| 10-G-2334    | Toyota      | Corolla    | Green  |  123389 |        1.3 |
| 10-WH-17931  | Toyota      | Corolla    | Silver |  130389 |        1.4 |
| 11-MO-23431  | Toyota      | Corolla    | Black  | 1234123 |        1.3 |
| 12-WH-123    | Ford Motors | Ka         | Black  |  125882 |        1.0 |
| 132-G-9923   | Ford Motors | Ka         | Silver |  325883 |        1.0 |
| 132-MO-19323 | Ford Motors | Galaxy     | Silver |    2343 |        1.5 |
| 171-G-39532  | Toyota      | Corolla    | Silver |   55882 |        1.3 |
| 171-MO-12533 | Ford Motors | Fiesta     | Black  |   25882 |        1.0 |
| 99-G-300     | Toyota      | Corolla    | Green  |  599339 |        1.3 |




### UPDATE ... SET ...=CONCAT() WHERE ... LIKE ... OR ... LIKE ...


The concat function joins two strings together which we want to do here on a condition.

```sql
update driver
set licenceNo = CONCAT("T-", licenceNo)
WHERE licenceNo like  "%F%"
OR licenceNo like "%R%";

```

This query updates the licenceNo for rows that meet the `where` condition. The `concat` function joins two strings together
```sql
select * from driver;
```

| licenceNo | name | busReg     |
| --- | --- | --- |
| L23423    | John | 12-G-1323  |
| T-F2233   | Alan | 191-G-123  |
| T-RN2423  | Bob  | NULL       |
| X98983    | Tom  | 161-D-1323 |


### DELETE  - FOREIGN KEY CONSTRAINTS


### FOREIGN KEY CONSTRAINT .. ON DELETE CASCADE


```sql
show create table driver
```

CREATE TABLE `driver` (
  `licenceNo` varchar(20) NOT NULL,
  `name` varchar(30) DEFAULT NULL,
  `busReg` varchar(15) DEFAULT NULL,
  PRIMARY KEY (`licenceNo`),
  KEY `busReg` (`busReg`),
  **CONSTRAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus` (`reg`) ON DELETE CASCADE**
) ENGINE=InnoDB DEFAULT CHARSET=latin1


The foreign key constraint `ON DELETE CASCADE` means that anytime a row is deleted from one table which has a foreign key referencing another table, the deletion will flow or cascade into another table.
In this case the `reg` in the `bus` table is being referenced by another table through a foreign key.The `bus` table itself does not have a foreign key but the `driver` table has a foreign key called `busreg` which has a foreign key constraint `ON DELETE CASCASE`. Therefore any rows deleted from the `bus` table which are referenced by the same `reg` in the `driver` table will be also deleted from the `driver` table. (`busReg`). The rows in the `driver` table with a foreign key `busReg` linking to the `reg` field in the `bus` table will also be deleted.

Note thay MySQL does not tell you that this has happened. It only lets you know that the bus table was affected `OK,1 row affected`. Because the constraint is set up as `on delete cascade` the delete flows or cascades from one table to the other table.

```sql
delete from bus where reg ="161-D-1323";
```
If the `driver` table 's foreign key `busReg` which references the `reg` column in the `bus` table is set to `ON DELETE CASCADE`, this means that if a row in the bus table is deleted and the value of the reg is used in the driver table, then this row should also be deleted from the driver table.

### FOREIGN KEY CONSTRAINT .. ON DELETE RESTRICT

`ON DELETE RESTRICT` means that if a row in the `bus` table is deleted and the value of the `reg` column is used in the `driver` table, that this row should **NOT** be deleted from the bus table as the driver table is restricting the delete.

### FOREIGN KEY CONSTRAINT .. ON DELETE SET NULL

`ON DELETE SET NULL` means that if a row in the bus table is deleted and the value of the `reg` column is used in the driver table, that the `busReg` in the driver table which was referencing the `reg` to be deleted from the driver table should be set to NULL, so now the `busReg` will no longer be referenced and can then be deleted from the bus table.

**CONSTRAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus` (`reg`) ON DELETE SET NULL**
) ENGINE=InnoDB DEFAULT CHARSET=latin

The foreign key from the driver table is pointing in to the bus table. If a row is deleted from the bus table which is referenced in the driver table, the foreign key in the driver table will first be set to 'NULL' and then the row can be deleted from the bus table. Unlike `on delete cascade`, the row referencing the reg will not be deleted from the `driver` table. The foreign key will just be updated to `NULL`.



***
### OPERATOR PRECEDENCE

```SQL
SELECT * FROM CAR 
WHERE mileage > 150000 AND (COLOUR = "Green" OR COLOUR ="SILVER");
```

| registration | make        | model      | colour | mileage | engineSize |
 --- | --- | --- | --- | --- | --- |
| 05-MO-17931  | Toyota      | Highlander | Green  |  253789 |        1.6 |
| 132-G-9923   | Ford Motors | Ka         | Silver |  325883 |        1.0 |
| 99-G-300     | Toyota      | Corolla    | Green  |  599339 |        1.3 |



Delete cars coloured green or silver  whose mileage is greater than 150000;
Be careful of operator precedence. 
***

# SUB-QUERIES

```sql
select * from bus;
```

| reg        | maxPassengers | fuel     |
| --- | --- | --- |
| 12-G-1323  |            34 | Petrol   |
| 161-D-1323 |            80 | Diesel   |
| 162-D-3433 |           120 | Electric |
| 191-G-123  |            56 | Diesel   |



```sql
select * from driver;
```


| licenceNo | name | age  | busReg     |
| --- | --- | --- | --- |
| L23423    | John |   32 | 12-G-1323  |
| X98983    | Tom  |   57 | 161-D-1323 |




```sql
select * from driver
where age=
(
	select max(age)
    from driver
)
;
```

The result of the inner query gets replaced as the argument in the outer query. In this way the query is written dynamically instead of hard-coding in a value. Therefore the same query can be used even if the results of the inner query has changed.


### Sub-query on one table

Can use a sub-query here instead of writing each part of the query separately and then passing the actual values to another query.

```sql
select * from driver
where age=
(
	select max(age)
    from driver
)
;
```
 licenceNo | name | age  | busReg     |
| --- | --- | --- | --- |
| X98983    | Tom  |   57 | 161-D-1323 |


The result of the inner query gets replaced as the argument in the outer query. This is better than running a query first to get the oldest driver's age and then writing another query where age = this value. This query shows the driver details for the oldest driver.


### Sub-query across more than one table.

### IN, MIN, MAX
Show all details of the bus driven by the youngest driver. When using minimum or maximum, can use IN instead of `=` in case there are more than one row with the minimum or maximum values for that column.


First find the youngest driver, then find the bus reg associated with the youngest driver. Then find all the details of the bus.

Return the results of the inner query to the outer query and use this in the outer query.


First find the age of the youngest driver and use the results of this in an outer query to find the busReg of the youngest driver. 
Using `IN` instead of `=` if there are more than one driver with the same minimum age.
Then once the busReg is returned, use this in an outer query again to get all the details of the bus.



```sql
select * from bus
where reg =
    (select busReg from driver
    where age in
        (
	    select min(age) from driver
        )
    )
;
```
This query finds the age of the youngest driver(s) and returns the results to the next outer query which then finds the busReg associated with the youngest driver(s). The results of this are returned to the outermost query.


 reg       | maxPassengers | fuel   |
| --- | --- | --- |
| 12-G-1323 |            34 | Petrol 

### Sub-query or Inner Join

```sql
select licenceNo from driver
	where busReg in (
		select reg from bus
		where fuel = "Diesel")
;
```
This query returns the reg from the bus table for diesel cars to the outer query which uses the result of the inner query to find the licenceNo from the driver table. The overall result is the license number of the driver who drives diesel buses.

licenceno |
| --- |
| X98983  

***
### Sub-query across two tables.

```sql
CREATE TABLE `salaries` (
  `emp_no` int(11) NOT NULL,
  `salary` int(11) NOT NULL,
  `from_date` date NOT NULL,
  `to_date` date NOT NULL,
  PRIMARY KEY (`emp_no`,`from_date`),
  KEY `emp_no` (`emp_no`),
CONSTRAINT `salaries_ibfk_1` FOREIGN KEY (`emp_no`) REFERENCES `employees` (`emp_no`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 |
```



```sql
show create table employees;
```

```sql
CREATE TABLE `employees` (
  `emp_no` int(11) NOT NULL,
  `birth_date` date NOT NULL,
  `first_name` varchar(14) NOT NULL,
  `last_name` varchar(16) NOT NULL,
  `gender` enum('M','F') NOT NULL,
  `hire_date` date NOT NULL,
  PRIMARY KEY (`emp_no`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 |
```

```sql
select e.emp_no, first_name, last_name
from employees e
where e.emp_no IN (
    select s.emp_no
    from salaries s
    where s.salary between 99000 and 99999
)
;
```

***
### INNER JOIN or SUB-QUERY.

Instead of using a sub-query here, an inner join could be used as there is a foreign key linking the two tables.
``` sql
select d.licenceNo 
from driver d
inner join bus b
on d.busReg = b.reg
where b.fuel ="Diesel";
```

licenceno |
| --- |
| X98983    |


### How are tables in a database related?

```sql
show create table bus;
show create table driver
```
Can see how the two tables are related using the `show create table` command. 
The `bus` table does not have a foreign key so it is not related to any other table but the `driver` table has a foreign key - the busReg column referencing the bus column in the bus table. 

```sql
show create table driver
```

KEY `busreg` (`busReg`)
CONSTAINT `driver_ibfk_1` FOREIGN KEY (`busReg`) REFERENCES `bus`(`reg`) ON DELETE CASCADE)


- The two tables are related on the `busReg` key in the `driver` table being a foreign key referencing the `reg` column in the `bus` table.
- The `driver` table has a column called `busReg` which is a foreign key referencing the `reg` column in the `bus` table. 

- The Reverse engineer EER diagram will show the connection from the `busReg` column (under Indexes)  with arrow pointing to the `reg` field in the `bus` table.

***
  
  

## SUB-QUERIES

 SELECT * FROM EMPLOYEES LIMIT 5;

| emp_no | birth_date | first_name | last_name | gender | hire_date  |
| --- | --- | --- | --- | --- | --- |
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 |
|  10002 | 1964-06-02 | Bezalel    | Simmel    | F      | 1985-11-21 |
|  10003 | 1959-12-03 | Parto      | Bamford   | M      | 1986-08-28 |
|  10004 | 1954-05-01 | Chirstian  | Koblick   | M      | 1986-12-01 |
|  10005 | 1955-01-21 | Kyoichi    | Maliniak  | M      | 1989-09-12 |

```sql
SELECT FLOOR(AVG(YEAR(BIRTH_DATE))) FROM EMPLOYEES;
```


| FLOOR(AVG(YEAR(BIRTH_DATE))) |
| -- |
|                         1957 |


This query shows the average birth year is 1957. Instead of hard-coding this value into another query to get the details of the employees born in that year using a sub-query. 

**`floor`** is used to round down instead of **round**. 

Show the emp_no, first_name and last_name of employees born in the average year.


```sql
select emp_no, first_name, last_name
from employees
where year(birth_date)=(
	select floor(avg(year(birth_date)))
	from employees
    )
;
```
This query returns details specified of employees born in the average year.

emp_no | first_name | last_name    |
| --- | --- | ---
|  10007 | Tzvetan    | Zielinski    |
|  10045 | Moss       | Shanbhogue   |
|  10054 | Mayumi     | Schueller    |
|  10080 | Premal     | Baek         |
|  10094 | Arumugam   | Ossenbruggen |

***

### Joining multiple tables to get data from two tables that are not directly connected.

In this database there are 3 tables. 
There are no foreign keys in the `dept` and `employees` tables but there are two foreign keys in the `salaries` table linking to each of these two tables. 
- The `emp_no` field in `salaries` is a foreign key referencing the `emp_no` field in the `employees` table.
- The `dept_no` field in `salaries` is a foreign key referencing the `dept_no` field in the `dept` table.


```sql
 select * from dept;
```

| dept_no | name                   |
| --- | --- |
| HR103   | Human Resources        |
| RD332   | Research & Development |
| S403    | Sales                  |


```sql
select * from employees;
```
| emp_no | birth_date | first_name | last_name | gender | hire_date  |
| --- | --- | --- | --- | --- | ---
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 |
|  10002 | 1964-06-02 | Bezalel    | Simmel    |  |F      | 1985-11-21 |


```sql
select * from salaries;
```
| emp_no | salary | from_date  | to_date    | dept_no |
| --- | --- | --- | --- | --- | --- |
|  10001 |  60117 | 1986-06-26 | 1987-06-26 | HR103   |
|  10001 |  62102 | 1987-06-26 | 1988-06-25 | HR103   |

`describe dept;`

| Field   | Type        | Null | Key | Default | Extra |
| --- | --- | --- | --- | --- | --- |
| dept_no | varchar(10) | NO   | PRI | NULL    |       |
| name    | varchar(50) | NO   |     | NULL    |       |

`describe employees;`

Field      | Type          | Null | Key | Default | Extra |
| --- | --- | --- | --- | --- | --- |
| emp_no     | int(11)       | NO   | PRI | NULL    |       |
| birth_date | date          | NO   |     | NULL    |       |
| first_name | varchar(14)   | NO   |     | NULL    |       |
| last_name  | varchar(16)   | NO   |     | NULL    |       |
| gender     | enum('M','F') | NO   |     | NULL    |       |
| hire_date  | date          | NO   |     | NULL    |     

`describe salaries;`

 Field     | Type        | Null | Key | Default | Extra |
| --- | --- | --- | --- | --- | --- |
| emp_no    | int(11)     | NO   | PRI | NULL    |       |
| salary    | int(11)     | NO   |     | NULL    |       |
| from_date | date        | NO   | PRI | NULL    |       |
| to_date   | date        | NO   |     | NULL    |       |
| dept_no   | varchar(10) | YES  | MUL | NULL    |      


```sql
CREATE TABLE `salaries` (
  `emp_no` int(11) NOT NULL,
  `salary` int(11) NOT NULL,
  `from_date` date NOT NULL,
  `to_date` date NOT NULL,
  `dept_no` varchar(10) DEFAULT NULL,
  PRIMARY KEY (`emp_no`,`from_date`),
  KEY `emp_no` (`emp_no`),
  KEY `dept_no` (`dept_no`),
  CONSTRAINT `salaries_ibfk_1` FOREIGN KEY (`emp_no`) REFERENCES `employees` (`emp_no`) ON DELETE CASCADE,
  CONSTRAINT `salaries_ibfk_2` FOREIGN KEY (`dept_no`) REFERENCES `dept` (`dept_no`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8
```


- **CONSTRAINT `salaries_ibfk_1` FOREIGN KEY (`emp_no`) REFERENCES `employees` (`emp_no`) ON DELETE CASCADE**,
- **CONSTRAINT `salaries_ibfk_2` FOREIGN KEY (`dept_no`) REFERENCES `dept` (`dept_no`) ON DELETE CASCADE**
) ENGINE=InnoDB DEFAULT CHARSET=utf8


```sql
select distinct e.emp_no, e.first_name, e.last_name, d.name 
from employees e 
inner join salaries s
on e.emp_no = s.emp_no 
inner join dept d 
on d.dept_no = s.dept_no;
```

This query joins together 3 tables even though no information is required from one table. 

emp_no | first_name  | last_name    | name                   |
| --- | --- | --- | --- |
|  10001 | Georgi      | Facello      | Human Resources        |
|  10002 | Bezalel     | Simmel       | Human Resources        |
|  10003 | Parto       | Bamford      | Human Resources        |
|  10004 | Chirstian   | Koblick      | Human Resources      