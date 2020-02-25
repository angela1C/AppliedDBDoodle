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

on command line `mysql -u root -p` then enter password when prompted.

***
## School database.
The `school.sql` is a database with two tables `subject` and `teacher` .

**Subject table** with 3 attributes
- Name
- Teacher
- OnLeavingCert (0-false, 1-True)

**Teacher table** with 5 attributes:
- Tid
- Name
- Level
- Experience
- dob

### `show tables;`
------------------
| Tables_in_school |
------------------
| subject          |
| teacher          |
------------------
2 rows in set (0.01 sec)

### `describe subject;`


| Field         | Type        | Null | Key | Default | Extra |
 ---| ---| ---| ---| ---| --|
| Name          | varchar(15) | NO   | PRI | NULL    |       |
| Teacher       | varchar(20) | YES  |     | NULL    |       |
| OnLeavingCert | tinyint(1)  | YES  |     | NULL    |       |
 

### `describe teacher;`

| Field      | Type          | Null | Key | Default | Extra          |
 ---| ---| ---| ---| ---| --|
| tid        | int(11)       | NO   | PRI | NULL    | auto_increment |
| Name       | varchar(20)   | YES  |     | NULL    |                |
| level      | enum('J','L') | YES  |     | NULL    |                |
| experience | int(11)       | YES  |     | NULL    |                |
| dob        | date          | YES  |     | NULL    |                |

5 rows in set (0.00 sec)

## `DESCRIBE <table>;`
- The `Type` shows the type of data for each Field as well as the maximum number of characters allowed.

- The `Key` column shows which field(s) is the primary key

## `SELECT * FROM <table>;` 

- `select * from teacher` to show all  data in the teacher table
- `select * from subject` to show all data in the subject table

### select * from teacher;

| tid | Name         | level | experience | dob        |
 ---| ---| ---| ---| ---| --|
|   1 | Mr. Pasteur  | L     |         15 | 1960-02-02 |
|   2 | Ms. Dubois   | L     |         22 | 1967-09-02 |
|   3 | Ms. Smith    | J     |          4 | 1980-03-23 |
|   4 | Mr. Hawking  | L     |         40 | 1951-02-19 |
|   5 | Mr. Kavanagh | J     |         50 | 1949-11-01 |
|   6 | Mr. Picasso  | J     |         42 | 1939-03-30 |
|   7 | Fr. Lynch    | L     |         55 | 1939-03-31 |

7 rows in set (0.01 sec)

### select * from subject;

| Name      | Teacher      | OnLeavingCert |
 ---| ---| ---| ---| ---| --|
| Biology   | Mr. Pasteur  |             1 |
| Colouring | Mr. Picasso  |             0 |
| English   | Mr. Kavanagh |             1 |
| French    | Ms. Dubois   |             1 |
| Maths     | Mr. Hawking  |             1 |
| Religion  | Fr. Lynch    |             1 |
| Spelling  | Ms. Smith    |             0 |

7 rows in set (0.01 sec)


### Show all names of all subjects that are on the leaving cert.

| name     |
+----------+
| Biology  |
| English  |
| French   |
| Maths    |
| Religion |

5 rows in set (0.00 sec)
```sql
select name from subject 
where onleavingcert =1;
```



| name     |
 ---| 
| Biology  |
| English  |
| French   |
| Maths    |
| Religion |

5 rows in set (0.00 sec)

### Show all name and experience of all teachers who are qualified to teach to Leaving Cert.
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

4 rows in set (0.01 sec)

### Show all details of all subjects who are taught by teachers whose title is not “Mr.” 
```sql
select * from subject 
where teacher NOT LIKE "Mr.%";
```


| Name     | Teacher    | OnLeavingCert |
 ---| ---| ---| ---| ---| --|
| French   | Ms. Dubois |             1 |
| Religion | Fr. Lynch  |             1 |
| Spelling | Ms. Smith  |             0 |

3 rows in set (0.01 sec)

### Show all details of all teachers who were born in January, February or March, and who can teach as far as Junior Cert only

```sql
select * from teacher
where month(dob) IN(1,2,3) 
AND level = "J";
```

| tid | Name        | level | experience | dob        |
 ---| ---| ---| ---| ---| --|
|   3 | Ms. Smith   | J     |          4 | 1980-03-23 |
|   6 | Mr. Picasso | J     |         42 | 1939-03-30 |

2 rows in set (0.00 sec)

gives the same results as
```sql
select * from teacher 
where month(dob) between 1 and 3 
AND level = "J";
```

### Show all unique month names that teachers were born in

```sql
select distinct monthname(dob)
from teacher;
```

| monthname(dob) |
--- |
| February       |
| September      |
| March          |
| November       |

4 rows in set (0.00 sec)

###  Show all details of all teachers, sorted by first by experience, then level. 

```sql
select * from teacher
order by experience desc, level;
```

| tid | Name         | level | experience | dob        |
 ---| ---| ---| ---| ---| --|
|   7 | Fr. Lynch    | L     |         55 | 1939-03-31 |
|   5 | Mr. Kavanagh | J     |         50 | 1949-11-01 |
|   6 | Mr. Picasso  | J     |         42 | 1939-03-30 |
|   4 | Mr. Hawking  | L     |         40 | 1951-02-19 |
|   2 | Ms. Dubois   | L     |         22 | 1967-09-02 |
|   1 | Mr. Pasteur  | L     |         15 | 1960-02-02 |
|   3 | Ms. Smith    | J     |          4 | 1980-03-23 |

7 rows in set (0.00 sec)

### Show all details of all subjects whose 3rd or 4th letter is “l”. Sort them by name. 

```sql
select * from subject 
where name like "__l%" or name like"___l%" 
order by name;
```

| Name      | Teacher      | OnLeavingCert |
 ---| ---| ---| ---| ---| --|
| Biology   | Mr. Pasteur  |             1 |
| Colouring | Mr. Picasso  |             0 |
| English   | Mr. Kavanagh |             1 |
| Religion  | Fr. Lynch    |             1 |
| Spelling  | Ms. Smith    |             0 |

5 rows in set (0.00 sec)

### Show the name of all teachers who have 10, 15, 20, 25, 30, 35, 40, 45, 50, 55 or 60 years experience. Sort from youngest to oldest. 

```sql
select * from teacher 
where experience in (10,15,20,25,30,35,40,45,50,55,60)
order by dob;
```

| tid | Name         | level | experience | dob        |
 ---| ---| ---| ---| ---| --|
|   7 | Fr. Lynch    | L     |         55 | 1939-03-31 |
|   5 | Mr. Kavanagh | J     |         50 | 1949-11-01 |
|   4 | Mr. Hawking  | L     |         40 | 1951-02-19 |
|   1 | Mr. Pasteur  | L     |         15 | 1960-02-02 |

4 rows in set (0.00 sec)

***


## car table.


select * from car;

| registration | make               | model   | colour | mileage | engineSize |
 ---| ---| ---| ---| ---| --|
| 10-G-2334    | Toyota             | Corolla | Green  |  123389 |        1.3 |
| 10-WH-17931  | Toyota             | Corolla | Silver |  130389 |        1.4 |
| 11-MO-23431  | Toyota             | Corolla | Black  | 1234123 |        1.3 |
| 12-WH-123    | Ford Motor Company | Ka      | Black  |  125882 |        1.0 |
| 132-MO-19323 | Ford Motor Company | Galaxy  | Silver |    2343 |        1.5 |
| 171-G-39532  | Toyota             | Corolla | Silver |   55882 |        1.3 |
| 171-MO-12533 | Ford Motor Company | Fiesta  | Black  |   25882 |        1.0 |


### Show the registration and mileage for all cars where the mileage is greater than 130000 and the colour is silver or black.

```sql
select registration, mileage from car where mileage > 130000 AND (colour= "Silver" or colour ="Black");
```



| registration | mileage |
 ---| ---| ---| ---| ---| --|
| 10-WH-17931  |  130389 |
| 11-MO-23431  | 1234123 |

2 rows in set (0.00 sec)


```sql
 select * from person;
 ```

| personID | name  | age  | sex  | dob        | isStudent |
 ---| ---| ---| ---| ---| --|
|        1 | John  |   24 | M    | 2000-01-01 |         1 |
|        2 | Tom   |   65 | M    | 1958-03-11 |         0 |
|        3 | Mary  |   13 | F    | 2005-04-11 |         1 |
|        4 | Alan  |   13 | M    | 2005-11-21 |         1 |
|        5 | Pat   |   30 | M    | 1993-03-17 |         0 |
|        6 | Shane |   41 | M    | 1988-07-21 |         0 |
|        7 | Shane |   15 | M    | 2003-06-01 |         1 |
|        8 | Alice |   25 | F    | 1999-03-01 |         1 |
|        9 | Pat   |   38 | F    | 1988-04-15 |         0 |

9 rows in set (0.01 sec)

### Show all details for all persons with exactly 3 letters in their name.

```sql
select * from person where name like ('___');
```


| personID | name | age  | sex  | dob        | isStudent |
 ---| ---| ---| ---| ---| --|
|        2 | Tom  |   65 | M    | 1958-03-11 |         0 |
|        5 | Pat  |   30 | M    | 1993-03-17 |         0 |
|        9 | Pat  |   38 | F    | 1988-04-15 |         0 |


### Show the distinct makes of car


```sql
select distinct(make) from car;
```


| make               |
 ---| ---| ---| ---| ---| --|
| Toyota             |
| Ford Motor Company |

2 rows in set (0.01 sec)


### Show all details of all cars registered in Galway. display the results from lowest to highest mileage


```sql
select * from car 
where registration like "%-G-%" 
order by mileage asc;

```

 registration | make   | model   | colour | mileage | engineSize |
 ---| ---| ---| ---| ---| --|
| 171-G-39532  | Toyota | Corolla | Silver |   55882 |        1.3 |
| 10-G-2334    | Toyota | Corolla | Green  |  123389 |        1.3 |

### Show all details of all people who were not born in Jan, Feb or march. Display the results in month order, but only show the first4  records returned.

```sql
select * from person 
where month(dob) not in(1,2,3) 
order by month(dob) 
limit 4;
```
personID | name  | age  | sex  | dob        | isStudent |
--- | --- | --- | ---| --- |---|
|        3 | Mary  |   13 | F    | 2005-04-11 |         1 |
|        9 | Pat   |   38 | F    | 1988-04-15 |         0 |
|        7 | Shane |   15 | M    | 2003-06-01 |         1 |
|        6 | Shane |   41 | M    | 1988-07-21 |         0 

***

## employees database

`show tables;`  

| Tables_in_employees |
---
| employees           |
| salaries            |

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