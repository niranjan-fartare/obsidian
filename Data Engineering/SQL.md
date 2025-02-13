Structured Query Language (SQL) is a programming language used to communicate with databases, such as MySQL, to perform various operations like storing, retrieving, updating, and deleting data.
# Table Of Contents

- [Data](#data)
	- [Types Of Data](#types-of-data)
	- [Units Of Data](#units-of-data)
- [DBMS](#DBMS)
- [ACID Properties](#acid-properties)
- [ER Diagram](#er-diagram)
	- [Relations / Cardinality](#relations--cardinality)
- [DDL](#ddl)
	- [ALTER](#alter)
	- [CREATE](#create)
	- [DROP](#drop)
	- [TRUNCATE](#truncate)
- [DML](#dml)
	- [INSERT](#insert)
	- [UPDATE](#update)
	- [DELETE](#delete)
- [DRL](#drl)
	- [SELECT](#select)
- [Constraints](#Constraints)
- [BETWEEN](#BETWEEN--AND)
# Data 

- Data : Facts, Figures, Statistics
- Information : Meaningful data
## Types of Data

- Structured : Tables, CSV
- Semi Structured : JSON, XML, HTML
- Unstructured : Text, PDF, Images, Videos
## Units Of Data 

- Bit : 0/1
- Byte : 8 Bits
- Kilobyte : 1024 Bytes
- Megabyte : 1024 Kilobytes
- Gigabyte : 1024 Megabytes
- Terabyte : 1024 Gigabytes
- Petabyte : 1024 Terabytes
- Exabyte : 1024 Petabytes 
# DBMS

- Database Management System is a software which is used to store, manage and retrieve data. 
- RDMBS is a type of DBMS that organizes data INTo tables that can be connected based on common fields. Examples, MySQL, MariaDB, Oracle, MS Server, PostgreSQL etc.
- Data is stored in the form of rows and columns within tables. 
- Each row represents a unique record, while each column represents a specific attribute of that record.
# ER Diagram

- Entity Relationship Diagram
- **Entity** : An entity is a object or thing in the real world that can be identified. It can be a physical object (like a car) or a concept (like a course).
- **Attributes** : Attributes are the properties or characteristics of an entity.
- **Relationships** : Relationships describe how entities are related to one another.
## Relations / Cardinality 

- **One-to-One (1:1)**: One instance of an entity is related to one instance of another entity.
- **One-to-Many (1:N)**: One instance of an entity is related to multiple instances of another entity.
- **Many-to-One (N:1)**: Multiple instances of one entity are related to one instance of another entity.
- **Many-to-Many (M:N)**: Multiple instances of one entity are related to multiple instances of another entity.
# ACID Properties

ACID properties ensure that database Transactions are processed reliably, maINTaining the INTegrity and consistency of the data throughout their life-cycle.

- **Atomicity** : A transaction should either be successful or it should not happen at all. If any part of the transaction fails, the entire transaction should be rolled back.
- **Consistency** : The Data should be consistent across transactions.
- **Isolation** : A transaction should not affect other transactions.
- **Durability** : Once a transaction is committed, changes are permanent, even in the event of a failure.

# DDL

- DDL is used to define and manage all database objects.
- Data Definition Language
- DDL statements are Auto-Commit
- [`ALTER`](#alter)
- [`CREATE`](#create)
- [`DROP`](#drop)
- [`truncate`](#truncate)
# DML

- Data Manipulation Language
- DML is used for managing data within existing database objects.
- [`INSERT`](#insert)
- [`UPDATE`](#update)
- [`DELETE`](#delete)
# DRL

- Data Retrieval
- DRL is a subset of DML focused specifically on retrieving data from the database.
- [`SELECT`](#select)
# Misc

- `show databases;` : Show all databases
- `use database;` : Use given database
- `desc table;` :  Show table structure
- `show tables;` : Show all tables in current database

# CREATE

- It is used to CREATE new database objects, such as tables, views, indexes, and databases.
- Database : 
	- Syntax : `CREATE DATABASE database_name;`
	- Eg, `CREATE DATABASE CompanyDB;`
- Table : 
	- `CREATE TABLE <table_name> (column datatype, column datatyoe(length/size));`
	- Eg. `CREATE TABLE student (roll INT, name VARCHAR(50));`
	- Eg. `CREATE TABLE emp (eid INT, ename VARCHAR(50), city VARCHAR(40), doj date);`
- View : 
	- `CREATE VIEW view_name AS SELECT * FROM table_name WHERE condition;`
	- Eg., `CREATE VIEW EmployeeView AS SELECT FirstName, LastName, DepartmentID FROM Employees WHERE Salary > 50000;`
- Index : 
	- `CREATE INDEX index_name ON table_name (column1, column2, ...);`
	- Eg. `CREATE INDEX idx_lastname ON Employees (LastName);`

# INSERT

- `INSERT` is used to add new records (rows) to a table.
- Syntax : 
	- `INSERT INTO <table_name> VALUES(value, value);`
	- `INSERT INTO <table_name> (col1, col2, col3) VALUES(val1, val2, val3);`
- Without Specifying Columns :
	- `INSERT INTO student VALUES(1, "Niranjan");`
	- `INSERT INTO emp VALUES(1, "Peter", "Pune", "2020-01-01");`
- Specifying Columns : 
	- `INSERT INTO emp (roll, name, city, doj) VALUES(1, "Peter", "Pune", "2020-01-01");` //(YYYY-MM-DD);
- Multiple Values : 
	- `INSERT INTO Employees (EmployeeID, FirstName, LastName, DateOfBirth, HireDate, Salary, DepartmentID) VALUES(2, 'Jane', 'Smith', '1990-03-22', '2021-05-15', 65000.00, 1), (3, 'Alice', 'Johnson', '1988-11-30', '2019-07-20', 70000.00, 3);`
- Inserting Data from Another Table :
	- `INSERT INTO Employees(EmployeeID, FirstName, LastName) SELECT EmployeeID, FirstName, LastName FROM TempEmployees;`
- The `VALUES` should match the actual columns
# UPDATE

UPDATE existing records

- Single Column : `UPDATE <table_name> SET <col_name>=<new_value> WHERE <condition_>;`
- Multiple Columns : `UPDATE <table_name> SET <col_name>=<new_value>, <col_name>=<new_value> WHERE <condition_>;`
- Eg. `UPDATE student SET roll = 4 WHERE name='Niranjan';`
# DELETE

Delete exiting records.

- `DELETE FROM <table_name> WHERE <condition>;`
- Eg. `DELETE FROM student WHERE roll=1;`
- `DELETE FROM <table_name>;` : Deletes all records from given table.
# TRUNCATE

MaINTain table structure and Delete all data.

- `TRUNCATE TABLE <table_name>;`
- Eg. `TRUNCATE TABLE emp;`
# DROP

Delete the whole table.

- `DROP TABLE <table_name>;`
- Eg. `DROP TABLE emp;`
# ALTER

- Adding new columns : 
	- `ALTER TABLE <table_name> ADD COLUMN <column_name> <data_type>`
	- `ALTER TABLE subscriber ADD COLUMN samount long;`  
- Removing existing columns : 
	- `ALTER TABLE <table_name> DROP COLUMN <column_name>;`
	- `ALTER TABLE subscriber DROP COLUMN extra_column;`
- Rename tables : 
	- `ALTER TABLE <old_table_name> RENAME TO <new_table_name>;`
	- Eg. `ALTER TABLE subscriber RENAME TO subs;`
- Change data type :
	- Change Column Name & Datatype :
		- `ALTER TABLE <table_name> CHANGE COLUMN <old_column> <new_col_name> <new_data_type>;`
		- Eg. `ALTER TABLE subscriber CHANGE COLUMN samount amount double;`
	- Change Column Name : 
		- `ALTER TABLE <table_name> CHANGE COLUMN <old_column> <new_col_name> <old_data_type>;`
		- Eg. `ALTER TABLE subscriber CHANGE COLUMN cid sid INT;`
	- Change Data type : 
		- `ALTER TABLE <table_name> CHANGE COLUMN <old_column> <old_column> <new_datatype>;`
		- Eg. `ALTER TABLE subscriber CHANGE COLUMN sid sid VARCHAR(100);`

# Constraints

- Not Null : Does not all `null` values.
	- `CREATE TABLE student (roll INT NOT NULL, name VARCHAR(100));`
- Unique : Does not allow `duplicate` values.
	- `CREATE TABLE student (roll INT UNIQUE, name VARCHAR(100));`
- Primary Key : Does not allow `null` and `duplicate` values.
	- Single Column :`CREATE TABLE student (roll INT PRIMARY KEY, name VARCHAR(100));`
	- Multiple Column : `CREATE TABLE student (roll INT, name VARCHAR(100), PRIMARY KEY(roll, name));
- Foreign Key : Used to link two tables together

```sql
CREATE TABLE course (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
);

CREATE TABLE enrollment (
    student_roll INT,
    course_id INT,
    PRIMARY KEY (student_roll, course_id),
    FOREIGN KEY (student_roll) REFERENCES student(roll),
    FOREIGN KEY (course_id) REFERENCES course(course_id)
);
```

# BETWEEN .. AND

- `SELECT * FROM emp WHERE eid BETWEEN 0 AND 10;` : Range
# LIKE

- `SELECT * FROM emp WHERE ename LIKE 'A%';` : Starts with A
- `SELECT * FROM emp WHERE ename LIKE '%A;` : Ends with A
- `SELECT * FROM emp WHERE ename LIKE '%A%';` : Anything that contains  A
- `SELECT * FROM emp WHERE ename LIKE '_____';` :  wildcard

```sql
-- City does not start and end with a,e,i,o,u

SELECT DISTINCT city
FROM station
WHERE city NOT LIKE '[AEIOU]%[AEIOU]';
```
# ORDER BY

```sql
SELECT * FROM emp ORDER by ename ASC; -- List records in Ascending Order
SELECT * FROM emp ORDER by ename DESC; -- List records in Descending Order
SELECT * FROM emp ORDER by ename DESC, city ASC;` : List desc by `ename` first then by `city
```
# LIMIT

- `SELECT * FROM emp LIMIT 8;` : List the top 8 records
- `SELECT * FROM emp LIMIT 8,2;` : List the 2 records after the top 8 records
# CASE

```sql
SELECT ename, CASE WHEN city='Pune' THEN 1000 WHEN city='Mumbai' THEN 1500 WHEN city='Delhi' THEN 2000 ELSE 500 END bonus FROM emp;
```
# Joins

- A `JOIN` clause is used to combine rows from two or more tables, based on a related column between them.

## Inner Join 

- Returns Matching Records in both tables
- Does not match with `NULL`.

```sql
SELECT emp.*, dept.dname
FROM emp
JOIN dept ON emp.did = dept.did;
```

```sql
+------+--------+------------+------------+-------+------+-------+
| eid  | ename  | city       | doj        | sal   | did  | dname |
+------+--------+------------+------------+-------+------+-------+
|    8 | Gaurav | Ahmednagar | 2000-01-01 | 35000 |   10 | IT    |
|    9 | Pooja  | Pune       | 1998-01-01 | 65000 |   20 | RD    |
|   10 | Komal  | Bengaluru  | 1998-01-01 | 65000 |   10 | IT    |
|   11 | Xin    | China      | 1998-01-01 | 65000 |   10 | IT    |
+------+--------+------------+------------+-------+------+-------+
4 rows in set (0.001 sec)
```
## Left Join

- Returns **All Records from left** and matching from right
	- Return 

```sql
SELECT emp.*, dname 
FROM emp LEFT 
JOIN dept ON emp.did = dept.did;
```

```sql
+------+----------+------------+------------+-------+------+-------+
| eid  | ename    | city       | doj        | sal   | did  | dname |
+------+----------+------------+------------+-------+------+-------+
|    8 | Gaurav   | Ahmednagar | 2000-01-01 | 35000 |   10 | IT    |
|   10 | Komal    | Bengaluru  | 1998-01-01 | 65000 |   10 | IT    |
|   11 | Xin      | China      | 1998-01-01 | 65000 |   10 | IT    |
|    9 | Pooja    | Pune       | 1998-01-01 | 65000 |   20 | RD    |
|    1 | Vivek    | Pune       | 1999-01-01 | 20000 | NULL | NULL  |
|    2 | Abhishek | Mumbai     | 2000-01-01 | 30000 | NULL | NULL  |
|    3 | Shivam   | Delhi      | 1996-05-05 | 40000 | NULL | NULL  |
|    4 | Neha     | Kashmir    | 1999-05-01 | 50000 | NULL | NULL  |
|    5 | Akshay   | Nagpur     | 1994-06-03 | 80000 | NULL | NULL  |
|    6 | Omkar    | Savedi     | 2000-07-03 | 20000 | NULL | NULL  |
|    7 | Kavita   | Shirdi     | 1999-01-01 | 35000 | NULL | NULL  |
+------+----------+------------+------------+-------+------+-------+
```

## Right Join

- Returns **All records from right** and matching from left.

```sql
SELECT emp.*, dname 
FROM emp 
RIGHT JOIN dept ON emp.did = dept.did;
```

```sql
+------+--------+------------+------------+-------+------+-------+
| eid  | ename  | city       | doj        | sal   | did  | dname |
+------+--------+------------+------------+-------+------+-------+
|    8 | Gaurav | Ahmednagar | 2000-01-01 | 35000 |   10 | IT    |
|    9 | Pooja  | Pune       | 1998-01-01 | 65000 |   20 | RD    |
|   10 | Komal  | Bengaluru  | 1998-01-01 | 65000 |   10 | IT    |
|   11 | Xin    | China      | 1998-01-01 | 65000 |   10 | IT    |
| NULL | NULL   | NULL       | NULL       |  NULL | NULL | DM    |
+------+--------+------------+------------+-------+------+-------+
```

## Full Outer Join

- Matching and non matching records from tables

## Cross Join

- Match every row from both tables.

```sql
MariaDB [b16]> SELECT eid, ename, dname FROM emp CROSS JOIN dept;
+------+----------+-------+
| eid  | ename    | dname |
+------+----------+-------+
|    1 | Vivek    | IT    |
|    1 | Vivek    | RD    |
|    1 | Vivek    | DM    |
|    2 | Abhishek | IT    |
|    2 | Abhishek | RD    |
|    2 | Abhishek | DM    |
|    3 | Shivam   | IT    |
|    3 | Shivam   | RD    |
|    3 | Shivam   | DM    |
|    4 | Neha     | IT    |
|    4 | Neha     | RD    |
|    4 | Neha     | DM    |
|    5 | Akshay   | IT    |
|    5 | Akshay   | RD    |
|    5 | Akshay   | DM    |
|    6 | Omkar    | IT    |
|    6 | Omkar    | RD    |
|    6 | Omkar    | DM    |
|    7 | Kavita   | IT    |
|    7 | Kavita   | RD    |
|    7 | Kavita   | DM    |
|    8 | Gaurav   | IT    |
|    8 | Gaurav   | RD    |
|    8 | Gaurav   | DM    |
|    9 | Pooja    | IT    |
|    9 | Pooja    | RD    |
|    9 | Pooja    | DM    |
|   10 | Komal    | IT    |
|   10 | Komal    | RD    |
|   10 | Komal    | DM    |
|   11 | Xin      | IT    |
|   11 | Xin      | RD    |
|   11 | Xin      | DM    |
+------+----------+-------+
33 rows in set (0.006 sec)
``` 

## Self Join

- Join table with itself

```sql
MariaDB [b16]> SELECT * from emps;
+------+---------+-------+
| eid  | ename   | mgrid |
+------+---------+-------+
|    1 | Alice   |  NULL |
|    2 | Bob     |     1 |
|    3 | Charlie |     1 |
|    4 | Diana   |     2 |
|    5 | Eve     |     2 |
|    6 | Frank   |     3 |
|    7 | Grace   |     3 |
|    8 | Hank    |     4 |
|    9 | Ivy     |     4 |
|   10 | Jack    |     5 |
+------+---------+-------+
10 rows in set (0.001 sec)
```

Output :

```sql

MariaDB [b16]> SELECT e.eid, e.ename , m.ename as Manager from emps e left join emps m on e.mgrid = m.eid;
+------+---------+---------+
| eid  | ename   | Manager |
+------+---------+---------+
|    2 | Bob     | Alice   |
|    3 | Charlie | Alice   |
|    4 | Diana   | Bob     |
|    5 | Eve     | Bob     |
|    6 | Frank   | Charlie |
|    7 | Grace   | Charlie |
|    8 | Hank    | Diana   |
|    9 | Ivy     | Diana   |
|   10 | Jack    | Eve     |
|    1 | Alice   | NULL    |
+------+---------+---------+
10 rows in set (0.001 sec)
```

# Functions

- Scaler : Returns same number of records, n records : n output
- Group : Returns a single output, n records : 1 output


## Scaler Functions

### upper 

Convert String to Upper case

```sql
MariaDB [b16]> SELECT ename, upper(ename) from emp;
+----------+--------------+
| ename    | upper(ename) |
+----------+--------------+
| Vivek    | VIVEK        |
| Abhishek | ABHISHEK     |
| Shivam   | SHIVAM       |
| Neha     | NEHA         |
| Akshay   | AKSHAY       |
| Omkar    | OMKAR        |
| Kavita   | KAVITA       |
| Gaurav   | GAURAV       |
| Pooja    | POOJA        |
| Komal    | KOMAL        |
| Xin      | XIN          |
+----------+--------------+

MariaDB [b16]> SELECT upper('abcd');
+---------------+
| upper('abcd') |
+---------------+
| ABCD          |
+---------------+

MariaDB [b16]> SELECT * from emp where upper(city) = 'Pune';
+------+-------+------+------------+-------+------+
| eid  | ename | city | doj        | sal   | did  |
+------+-------+------+------------+-------+------+
|    1 | Vivek | Pune | 1999-01-01 | 20000 | NULL |
|    9 | Pooja | Pune | 1998-01-01 | 65000 |   20 |
+------+-------+------+------------+-------+------+
```

### lower 

Convert string to Lower Case

```sql
MariaDB [b16]> SELECT ename, lower(ename) from emp;
+----------+--------------+
| ename    | lower(ename) |
+----------+--------------+
| Vivek    | vivek        |
| Abhishek | abhishek     |
| Shivam   | shivam       |
| Neha     | neha         |
| Akshay   | akshay       |
| Omkar    | omkar        |
| Kavita   | kavita       |
| Gaurav   | gaurav       |
| Pooja    | pooja        |
| Komal    | komal        |
| Xin      | xin          |
+----------+--------------+

MariaDB [b16]> SELECT lower('ABCD');
+---------------+
| lower('ABCD') |
+---------------+
| abcd          |
+---------------+
```

### length

Counts characters in a string

```sql
MariaDB [b16]> SELECT length('  Hello World ');
+--------------------------+
| length('  Hello World ') |
+--------------------------+
|                       14 |
+--------------------------+
```

### trim 

Remove space from left and right side of the string

```sql
MariaDB [b16]> SELECT length(trim('  Hello World '));
+--------------------------------+
| length(trim('  Hello World ')) |
+--------------------------------+
|                             11 |
+--------------------------------+
```

### ltrim 

Remove space from left side of the string

```sql
MariaDB [b16]> SELECT length(ltrim('  Hello World '));
+---------------------------------+
| length(ltrim('  Hello World ')) |
+---------------------------------+
|                              12 |
+---------------------------------+
1 row in set (0.001 sec)
```

### rtrim

Remove space from right side of the string

```sql
MariaDB [b16]> SELECT length(rtrim('  Hello World '));
+---------------------------------+
| length(rtrim('  Hello World ')) |
+---------------------------------+
|                              13 |
+---------------------------------+
```

### repeat 

Repeats the SELECTed records n times

```sql
MariaDB [b16]> SELECT repeat(ename,2) from emp;
+------------------+
| repeat(ename,2)  |
+------------------+
| VivekVivek       |
| AbhishekAbhishek |
| ShivamShivam     |
| NehaNeha         |
| AkshayAkshay     |
| OmkarOmkar       |
| KavitaKavita     |
| GauravGaurav     |
| PoojaPooja       |
| KomalKomal       |
| XinXin           |
+------------------+
```

### reverse 

Reverses the SELECTed column

```sql
MariaDB [b16]> SELECT ename, reverse(ename) from emp;
+----------+----------------+
| ename    | reverse(ename) |apt install default-jre
+----------+----------------+
| Vivek    | keviV          |
| Abhishek | kehsihbA       |
| Shivam   | mavihS         |
| Neha     | aheN           |
| Akshay   | yahskA         |
| Omkar    | rakmO          |
| Kavita   | ativaK         |
| Gaurav   | varuaG         |
| Pooja    | ajooP          |
| Komal    | lamoK          |
| Xin      | niX            |
+----------+----------------+
```

### concat 

- Concatenates columns
- If one the value is null returns null

```sql
MariaDB [b16]> SELECT ename, city, concat(ename,'-',city) from emp;
+----------+------------+------------------------+
| ename    | city       | concat(ename,'-',city) |
+----------+------------+------------------------+
| Vivek    | Pune       | Vivek-Pune             |
| Abhishek | Mumbai     | Abhishek-Mumbai        |
| Shivam   | Delhi      | Shivam-Delhi           |
| Neha     | Kashmir    | Neha-Kashmir           |
| Akshay   | Nagpur     | Akshay-Nagpur          |
| Omkar    | Savedi     | Omkar-Savedi           |
| Kavita   | Shirdi     | Kavita-Shirdi          |
| Gaurav   | Ahmednagar | Gaurav-Ahmednagar      |
| Pooja    | Pune       | Pooja-Pune             |
| Komal    | Bengaluru  | Komal-Bengaluru        |
| Xin      | China      | Xin-China              |
+----------+------------+------------------------+
```

### replace 

replace char/string with given char/string

```sql
MariaDB [b16]> SELECT ename, replace(ename, 'a','x') from emp;
+----------+-------------------------+
| ename    | replace(ename, 'a','x') |
+----------+-------------------------+
| Vivek    | Vivek                   |
| Abhishek | Abhishek                |
| Shivam   | Shivxm                  |
| Neha     | Nehx                    |
| Akshay   | Akshxy                  |
| Omkar    | Omkxr                   |
| Kavita   | Kxvitx                  |
| Gaurav   | Gxurxv                  |
| Pooja    | Poojx                   |
| Komal    | Komxl                   |
| Xin      | Xin                     |
+----------+-------------------------+

MariaDB [b16]> SELECT ename, replace(ename, 'ek','x') from emp;
+----------+--------------------------+
| ename    | replace(ename, 'ek','x') |
+----------+--------------------------+
| Vivek    | Vivx                     |
| Abhishek | Abhishx                  |
| Shivam   | Shivam                   |
| Neha     | Neha                     |
| Akshay   | Akshay                   |
| Omkar    | Omkar                    |
| Kavita   | Kavita                   |
| Gaurav   | Gaurav                   |
| Pooja    | Pooja                    |
| Komal    | Komal                    |
| Xin      | Xin                      |
+----------+--------------------------+

```

### substr

Output the n char after given index (col, index, n )

```sql
MariaDB [b16]> SELECT city, substr(city, 1,3) from emp;
+------------+-------------------+
| city       | substr(city, 1,3) |
+------------+-------------------+
| Pune       | Pun               |
| Mumbai     | Mum               |
| Delhi      | Del               |
| Kashmir    | Kas               |
| Nagpur     | Nag               |
| Savedi     | Sav               |
| Shirdi     | Shi               |
| Ahmednagar | Ahm               |
| Pune       | Pun               |
| Bengaluru  | Ben               |
| China      | Chi               |
+------------+-------------------+
```


### substring_index 

Split using given pattern

```sql
MariaDB [b16]> SELECT email, substring_index(email, '@',1) from emp;
+--------------------+-------------------------------+
| email              | substring_index(email, '@',1) |
+--------------------+-------------------------------+
| vivek@gmail.com    | vivek                         |
| abhishek@gmail.com | abhishek                      |
| shivam@gmail.com   | shivam                        |
| neha@gmail.com     | neha                          |
| akshay@gmail.com   | akshay                        |
| omkar@gmail.com    | omkar                         |
| kavita@gmail.com   | kavita                        |
| gaurav@gmail.com   | gaurav                        |
| pooja@gmail.com    | pooja                         |
| komal@gmail.com    | komal                         |
| xin@gmail.com      | xin                           |
+--------------------+-------------------------------+
```

## 10 Nov

### round

Rounds up to nearest INTeger

```sql
MariaDB [b16]> SELECT round(190.12323);
+------------------+
| round(190.12323) |
+------------------+
|              190 |
+------------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT round(190.92323);
+------------------+
| round(190.92323) |
+------------------+
|              191 |
+------------------+
1 row in set (0.001 sec)
```

### format

Rounds up and make the value precise

```sql
MariaDB [b16]> SELECT format(190.1232, 2);
+---------------------+
| format(190.1232, 2) |
+---------------------+
| 190.12              |
+---------------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT format(190.9232, 2);
+---------------------+
| format(190.9232, 2) |
+---------------------+
| 190.92              |
+---------------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT format(190.9232, 3);
+---------------------+
| format(190.9232, 3) |
+---------------------+
| 190.923             |
+---------------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT format(190.9632, 1);
+---------------------+
| format(190.9632, 1) |
+---------------------+
| 191.0               |
+---------------------+
1 row in set (0.001 sec)
```

### coalesce

Returns the first non-NULL value in a list of arguments

```sql
MariaDB [b16]> SELECT *, coalesce(ccity,pcity,'Not Present') as City from cust;
+------+-------+--------+-------------+
| id   | ccity | pcity  | City        |
+------+-------+--------+-------------+
|    1 | Pune  | Mumbai | Pune        |
|    2 | Delhi | NULL   | Delhi       |
|    3 | NULL  | Surat  | Surat       |
|    4 | NULL  | NULL   | Not Present |
+------+-------+--------+-------------+
```

### now

Current date & time

```sql
MariaDB [b16]> SELECT now();
+---------------------+
| now()               |
+---------------------+
| 2024-11-10 09:14:33 |
+---------------------+
1 row in set (0.001 sec)
```

### current_date 

Returns Current Date

```sql
MariaDB [b16]> SELECT current_date();
+----------------+
| current_date() |
+----------------+
| 2024-11-10     |
+----------------+
1 row in set (0.001 sec)
```

### current_time 

Return Current Time

```sql
MariaDB [b16]> SELECT current_time();
+----------------+
| current_time() |
+----------------+
| 09:21:13       |
+----------------+
```

### year, month, monthname, day, dayname, hour, minute, second 

```sql
MariaDB [b16]> SELECT year(now());
+-------------+
| year(now()) |
+-------------+
|        2024 |
+-------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT month(now());
+--------------+
| month(now()) |
+--------------+
|           11 |
+--------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT monthname(now());
+------------------+
| monthname(now()) |
+------------------+
| November         |
+------------------+


MariaDB [b16]> SELECT day(now());
+------------+
| day(now()) |
+------------+
|         10 |
+------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT dayname(now());
+----------------+
| dayname(now()) |
+----------------+
| Sunday         |
+----------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT hour(now());
+-------------+
| hour(now()) |
+-------------+
|           9 |
+-------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT minute(now());
+---------------+
| minute(now()) |
+---------------+
|            31 |
+---------------+
1 row in set (0.000 sec)

MariaDB [b16]> SELECT second(now());
+---------------+
| second(now()) |
+---------------+
|            19 |
+---------------+
1 row in set (0.001 sec)
```


### dateformat(col, format)

Change format of given col

```sql
SELECT date_format(now(), '%Y');
```

| Specifier    | Description                                                          | Example Output      |
| ------------ | -------------------------------------------------------------------- | ------------------- |
| `%Y`         | Year as a four-digit number                                          | `2023`              |
| `%y`         | Year as a two-digit number                                           | `23`                |
| `%m`         | Month as a numeric (01-12)                                           | `04`                |
| `%M`         | Month as a full name                                                 | `April`             |
| `%b`         | Month as a short name                                                | `Apr`               |
| `%d`         | Day of the month (01-31)                                             | `05`                |
| `%H`         | Hour (00-23)                                                         | `14`                |
| `%h` or `%I` | Hour (01-12)                                                         | `02`                |
| `%i`         | Minutes (00-59)                                                      | `30`                |
| `%s`         | Seconds (00-59)                                                      | `45`                |
| `%p`         | AM or PM                                                             | `PM`                |
| `%W`         | Weekday name (full)                                                  | `Wednesday`         |
| `%w`         | Day of the week (0=Sunday, 6=Saturday)                               | `3` (for Wednesday) |
| `%j`         | Day of the year (001-366)                                            | `095`               |
| `%U`         | Week number of the year (00-53, Sunday as the first day of the week) | `14`                |
| `%V`         | Week number of the year (01-53, Monday as the first day of the week) | `14`                |
| `%X`         | Year for the week (same as `%Y` if the week belongs to that year)    | `2023`              |
### date_add(col, INTerval n day/month/year) 

Add n days/month/year to the given date

```sql
MariaDB [b16]> SELECT date_add(now(), INTerval 2 day);
+---------------------------------+
| date_add(now(), INTerval 2 day) |
+---------------------------------+
| 2024-11-12 09:58:19             |
+---------------------------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT date_add(now(), INTerval 2 month);
+-----------------------------------+
| date_add(now(), INTerval 2 month) |
+-----------------------------------+
| 2025-01-10 09:58:22               |
+-----------------------------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT date_add(now(), INTerval 2 year);
+----------------------------------+
| date_add(now(), INTerval 2 year) |
+----------------------------------+
| 2026-11-10 09:58:25              |
+----------------------------------+
1 row in set (0.001 sec)

MariaDB [b16]> SELECT date_format(date_add(now(), INTerval 1 month), '%Y/%M/%D');
+------------------------------------------------------------+
| date_format(date_add(now(), INTerval 1 month), '%Y/%M/%D') |
+------------------------------------------------------------+
| 2024/December/10th                                         |
+------------------------------------------------------------+
1 row in set (0.001 sec)
```

### sub_date(col, INTerval n) 

Reduces the given INTerval 

```sql
MariaDB [b16]> SELECT date_format(now(), '%Y/%M/%D') as Current, date_format(date_sub(now(), INTerval 2 day), '%Y/%M/%D') as 'sub_date()';
+--------------------+-------------------+
| Current            | sub_date()        |
+--------------------+-------------------+
| 2024/November/10th | 2024/November/8th |
+--------------------+-------------------+
1 row in set (0.001 sec)
```

### datediff(current_date, col)

Returns remaining days from the given date

```sql
MariaDB [b16]> SELECT sub_date, current_date(), datediff(now(), sub_date) as Expiry from subscriber;
+---------------------+----------------+--------+
| sub_date            | current_date() | Expiry |
+---------------------+----------------+--------+
| 2023-11-10 09:15:00 | 2024-11-10     |    366 |
| 2023-12-05 14:45:00 | 2024-11-10     |    341 |
| 2023-01-10 08:00:00 | 2024-11-10     |    670 |
| 2023-02-15 12:30:00 | 2024-11-10     |    634 |
| 2023-03-20 15:00:00 | 2024-11-10     |    601 |
| 2023-01-15 10:00:00 | 2024-11-10     |    665 |
| 2023-02-20 11:30:00 | 2024-11-10     |    629 |
| 2023-03-10 09:15:00 | 2024-11-10     |    611 |
| 2023-04-05 14:45:00 | 2024-11-10     |    585 |
| 2023-05-15 08:00:00 | 2024-11-10     |    545 |
| 2023-06-20 12:30:00 | 2024-11-10     |    509 |
| 2023-07-10 15:00:00 | 2024-11-10     |    489 |
| 2023-08-05 16:30:00 | 2024-11-10     |    463 |
| 2023-09-15 10:00:00 | 2024-11-10     |    422 |
| 2023-10-20 11:30:00 | 2024-11-10     |    387 |
+---------------------+----------------+--------+
```

## Group Functions

### max(col)

```sql
MariaDB [b16]> SELECT max(sal) from emp;
+----------+
| max(sal) |
+----------+
|    80000 |
+----------+
1 row in set (0.001 sec)
```

### min(col)

```sql
MariaDB [b16]> SELECT min(sal) from emp;
+----------+
| min(sal) |
+----------+
|    20000 |
+----------+
1 row in set (0.001 sec)
```

### sum(col)

```sql
MariaDB [b16]> SELECT sum(sal) from emp;
+----------+
| sum(sal) |
+----------+
|   505000 |
+----------+
1 row in set (0.001 sec)
```

### avg(sal)

```sql
MariaDB [b16]> SELECT avg(sal) from emp;
+------------+
| avg(sal)   |
+------------+
| 45909.0909 |
+------------+
1 row in set (0.001 sec)
```

### count(col)

- count(col) : Does not count Null columns
- count(1) : Counts all records including Null

```sql
MariaDB [b16]> SELECT count(sal) from emp;
+------------+
| count(sal) |
+------------+
|         11 |
+------------+
```

### distinct 

```sql
MariaDB [b16]> SELECT * from emp;
+------+----------+------------+------------+-------+------+--------------------+
| eid  | ename    | city       | doj        | sal   | did  | email              |
+------+----------+------------+------------+-------+------+--------------------+
|    1 | Vivek    | Pune       | 1999-01-01 | 20000 | NULL | vivek@gmail.com    |
|    2 | Abhishek | Mumbai     | 2000-01-01 | 30000 | NULL | abhishek@gmail.com |
|    3 | Shivam   | Delhi      | 1996-05-05 | 40000 | NULL | shivam@gmail.com   |
|    4 | Neha     | Kashmir    | 1999-05-01 | 50000 | NULL | neha@gmail.com     |
|    5 | Akshay   | Nagpur     | 1994-06-03 | 80000 | NULL | akshay@gmail.com   |
|    6 | Omkar    | Savedi     | 2000-07-03 | 20000 | NULL | omkar@gmail.com    |
|    7 | Kavita   | Shirdi     | 1999-01-01 | 35000 | NULL | kavita@gmail.com   |
|    8 | Gaurav   | Ahmednagar | 2000-01-01 | 35000 |   10 | gaurav@gmail.com   |
|    9 | Pooja    | Pune       | 1998-01-01 | 65000 |   20 | pooja@gmail.com    |
|   10 | Komal    | Bengaluru  | 1998-01-01 | 65000 |   10 | komal@gmail.com    |
|   11 | Xin      | China      | 1998-01-01 | 65000 |   10 | xin@gmail.com      |
|    1 | Vivek    | Pune       | 1999-01-01 | 20000 | NULL | vivek@gmail.com    |
|    2 | Abhishek | Mumbai     | 2000-01-01 | 30000 | NULL | abhishek@gmail.com |
|    3 | Shivam   | Delhi      | 1996-05-05 | 40000 | NULL | shivam@gmail.com   |
|    4 | Neha     | Kashmir    | 1999-05-01 | 50000 | NULL | neha@gmail.com     |
|    5 | Akshay   | Nagpur     | 1994-06-03 | 80000 | NULL | akshay@gmail.com   |
|    6 | Omkar    | Savedi     | 2000-07-03 | 20000 | NULL | omkar@gmail.com    |
|    7 | Kavita   | Shirdi     | 1999-01-01 | 35000 | NULL | kavita@gmail.com   |
|    8 | Gaurav   | Ahmednagar | 2000-01-01 | 35000 |   10 | gaurav@gmail.com   |
|    9 | Pooja    | Pune       | 1998-01-01 | 65000 |   20 | pooja@gmail.com    |
|   10 | Komal    | Bengaluru  | 1998-01-01 | 65000 |   10 | komal@gmail.com    |
|   11 | Xin      | China      | 1998-01-01 | 65000 |   10 | xin@gmail.com      |
+------+----------+------------+------------+-------+------+--------------------+
22 rows in set (0.001 sec)

MariaDB [b16]> SELECT distinct * from emp;
+------+----------+------------+------------+-------+------+--------------------+
| eid  | ename    | city       | doj        | sal   | did  | email              |
+------+----------+------------+------------+-------+------+--------------------+
|    1 | Vivek    | Pune       | 1999-01-01 | 20000 | NULL | vivek@gmail.com    |
|    2 | Abhishek | Mumbai     | 2000-01-01 | 30000 | NULL | abhishek@gmail.com |
|    3 | Shivam   | Delhi      | 1996-05-05 | 40000 | NULL | shivam@gmail.com   |
|    4 | Neha     | Kashmir    | 1999-05-01 | 50000 | NULL | neha@gmail.com     |
|    5 | Akshay   | Nagpur     | 1994-06-03 | 80000 | NULL | akshay@gmail.com   |
|    6 | Omkar    | Savedi     | 2000-07-03 | 20000 | NULL | omkar@gmail.com    |
|    7 | Kavita   | Shirdi     | 1999-01-01 | 35000 | NULL | kavita@gmail.com   |
|    8 | Gaurav   | Ahmednagar | 2000-01-01 | 35000 |   10 | gaurav@gmail.com   |
|    9 | Pooja    | Pune       | 1998-01-01 | 65000 |   20 | pooja@gmail.com    |
|   10 | Komal    | Bengaluru  | 1998-01-01 | 65000 |   10 | komal@gmail.com    |
|   11 | Xin      | China      | 1998-01-01 | 65000 |   10 | xin@gmail.com      |
+------+----------+------------+------------+-------+------+--------------------+
11 rows in set (0.001 sec)

MariaDB [b16]> SELECT distinct sal from emp;
+-------+
| sal   |
+-------+
| 20000 |
| 30000 |
| 40000 |
| 50000 |
| 80000 |
| 35000 |
| 65000 |
+-------+
7 rows in set (0.001 sec)
```


## 16 Nov
# Group By

Used to perform group functions on group of records based on given column


```sql
MariaDB [b16]> SELECT did, avg(sal) from emp group by did;
+------+------------+
| did  | avg(sal)   |
+------+------------+
| NULL | 39285.7143 |
|   10 | 55000.0000 |
|   20 | 65000.0000 |
|   30 | 10000.0000 |
+------+------------+
4 rows in set (0.001 sec)
```

# Having

Use to filter output of Group By

```sql
MariaDB [b16]> SELECT did, sum(sal)from emp group by did having sum(sal) > 50000;
+------+----------+
| did  | sum(sal) |
+------+----------+
|   10 |   330000 |
|   20 |   130000 |
|   38 |   115000 |
|   92 |    80000 |
|   97 |    70000 |
+------+----------+
5 rows in set (0.001 sec)
```


# Set Operators

- UNION : Combines both returns unique records
- UNION ALL : Combines both tables including duplicate records
- INTERSECT : Returns matching unique records from both 
- MINUS/EXCEPT : Non Matching records from first table

```sql
MariaDB [b16]> SELECT * from pune;
+------+--------+
| id   | ename  |
+------+--------+
|    1 | akash  |
|    2 | ganesh |
+------+--------+
2 rows in set (0.000 sec)

MariaDB [b16]> SELECT * from mumbai;
+------+---------+
| id   | ename   |
+------+---------+
|    1 | sandesh |
|    1 | akash   |
+------+---------+
2 rows in set (0.000 sec)
```

## Union

```sql
MariaDB [b16]> SELECT * from pune UNION SELECT * from mumbai;
+------+---------+
| id   | ename   |
+------+---------+
|    1 | akash   |
|    2 | ganesh  |
|    1 | sandesh |
+------+---------+
3 rows in set (0.000 sec)
```

## Union All

```sql
MariaDB [b16]> SELECT * from pune UNION ALL SELECT * from mumbai;
+------+---------+
| id   | ename   |
+------+---------+
|    1 | akash   |
|    2 | ganesh  |
|    1 | sandesh |
|    1 | akash   |
+------+---------+
4 rows in set (0.000 sec)
```
## INTersect

```sql
MariaDB [b16]> SELECT * from pune INTERSECT SELECT * from mumbai;
+------+-------+
| id   | ename |
+------+-------+
|    1 | akash |
+------+-------+
1 row in set (0.000 sec)
```

## EXCEPT / MINUS

```sql
MariaDB [b16]> SELECT * from pune EXCEPT SELECT * from mumbai;
+------+--------+
| id   | ename  |
+------+--------+
|    2 | ganesh |
+------+--------+
1 row in set (0.000 sec)

MariaDB [b16]> SELECT * from mumbai EXCEPT SELECT * from pune;
+------+---------+
| id   | ename   |
+------+---------+
|    1 | sandesh |
+------+---------+
1 row in set (0.000 sec)

```


## 17 Nov

# Sub Queries

```sql
MariaDB [b16]> SELECT * from emp where sal = (SELECT max(sal)from emp);
+------+--------+--------+------------+-------+------+------------------+
| eid  | ename  | city   | doj        | sal   | did  | email            |
+------+--------+--------+------------+-------+------+------------------+
|    5 | Akshay | Nagpur | 1994-06-03 | 80000 |   92 | akshay@gmail.com |
|    5 | Akshay | Nagpur | 1994-06-03 | 80000 |   38 | akshay@gmail.com |
+------+--------+--------+------------+-------+------+------------------+
2 rows in set (0.007 sec)

MariaDB [b16]> SELECT * from (SELECT *, sal * 12 as 'AnnualSalary'  from emp)A where AnnualSalary >= 300000;
+------+----------+------------+------------+-------+------+--------------------+--------------+
| eid  | ename    | city       | doj        | sal   | did  | email              | AnnualSalary |
+------+----------+------------+------------+-------+------+--------------------+--------------+
|    2 | Abhishek | Mumbai     | 2000-01-01 | 30000 |   39 | abhishek@gmail.com |       360000 |
|    3 | Shivam   | Delhi      | 1996-05-05 | 40000 |   46 | shivam@gmail.com   |       480000 |
|    4 | Neha     | Kashmir    | 1999-05-01 | 50000 |   11 | neha@gmail.com     |       600000 |
|    5 | Akshay   | Nagpur     | 1994-06-03 | 80000 |   92 | akshay@gmail.com   |       960000 |
|    7 | Kavita   | Shirdi     | 1999-01-01 | 35000 |   71 | kavita@gmail.com   |       420000 |
|    8 | Gaurav   | Ahmednagar | 2000-01-01 | 35000 |   10 | gaurav@gmail.com   |       420000 |
|    9 | Pooja    | Pune       | 1998-01-01 | 65000 |   20 | pooja@gmail.com    |       780000 |
|   10 | Komal    | Bengaluru  | 1998-01-01 | 65000 |   10 | komal@gmail.com    |       780000 |
|   11 | Xin      | China      | 1998-01-01 | 65000 |   10 | xin@gmail.com      |       780000 |
|    2 | Abhishek | Mumbai     | 2000-01-01 | 30000 |   77 | abhishek@gmail.com |       360000 |
|    3 | Shivam   | Delhi      | 1996-05-05 | 40000 |   86 | shivam@gmail.com   |       480000 |
|    4 | Neha     | Kashmir    | 1999-05-01 | 50000 |   97 | neha@gmail.com     |       600000 |
|    5 | Akshay   | Nagpur     | 1994-06-03 | 80000 |   38 | akshay@gmail.com   |       960000 |
|    7 | Kavita   | Shirdi     | 1999-01-01 | 35000 |   38 | kavita@gmail.com   |       420000 |
|    8 | Gaurav   | Ahmednagar | 2000-01-01 | 35000 |   10 | gaurav@gmail.com   |       420000 |
|    9 | Pooja    | Pune       | 1998-01-01 | 65000 |   20 | pooja@gmail.com    |       780000 |
|   10 | Komal    | Bengaluru  | 1998-01-01 | 65000 |   10 | komal@gmail.com    |       780000 |
|   11 | Xin      | China      | 1998-01-01 | 65000 |   10 | xin@gmail.com      |       780000 |
+------+----------+------------+------------+-------+------+--------------------

MariaDB [b16]> SELECT * from emp where did in (SELECT did from dept);
+------+-----------+------------+------------+-------+------+-------------------+
| eid  | ename     | city       | doj        | sal   | did  | email             |
+------+-----------+------------+------------+-------+------+-------------------+
|    8 | Gaurav    | Ahmednagar | 2000-01-01 | 35000 |   10 | gaurav@gmail.com  |
|   10 | Komal     | Bengaluru  | 1998-01-01 | 65000 |   10 | komal@gmail.com   |
|   11 | Xin       | China      | 1998-01-01 | 65000 |   10 | xin@gmail.com     |
|    8 | Gaurav    | Ahmednagar | 2000-01-01 | 35000 |   10 | gaurav@gmail.com  |
|   10 | Komal     | Bengaluru  | 1998-01-01 | 65000 |   10 | komal@gmail.com   |
|   11 | Xin       | China      | 1998-01-01 | 65000 |   10 | xin@gmail.com     |
|    9 | Pooja     | Pune       | 1998-01-01 | 65000 |   20 | pooja@gmail.com   |
|    9 | Pooja     | Pune       | 1998-01-01 | 65000 |   20 | pooja@gmail.com   |
|   12 | Mr. Beast | Texas      | 2024-11-16 | 10000 |   30 | mrbeast@gmail.com |
+------+-----------+------------+------------+-------+------+-------------------+
9 rows in set (0.001 sec)

MariaDB [b16]> SELECT temp_cust.*, temp_orders.order_date from (SELECT * from customer where state='TX') temp_cust inner join (SELECT * from orders where order_date between '2023-01-01' and '2023-12-31') temp_orders on temp_cust.cid = temp_orders.cid;
+------+-------------------+-------------+-------+------------+-------------------------------+---------------------+
| cid  | cname             | city        | state | mobile     | email                         | order_date          |
+------+-------------------+-------------+-------+------------+-------------------------------+---------------------+
| 107  | Robert Thompson   | San Antonio | TX    | 4444444444 | robert.thompson@example.com   | 2023-04-07 15:10:00 |
| 109  | William Hernandez | Dallas      | TX    | 7777777777 | william.hernandez@example.com | 2023-04-09 14:40:15 |
+------+-------------------+-------------+-------+------------+-------------------------------+---------------------+
2 rows in set (0.001 sec)

```

# CTE (Common Table Expression)

```sql 
MariaDB [b16]> with temp_cust AS (SELECT * from customer where state='TX'), temp_orders AS (SELECT * from orders where order_date between '2023-01-01' and '2023-12-31')  SELECT temp_cust.*, temp_orders.order_date from temp_cust   inner join temp_orders  on temp_cust.cid = temp_orders.cid;
+------+-------------------+-------------+-------+------------+-------------------------------+---------------------+
| cid  | cname             | city        | state | mobile     | email                         | order_date          |
+------+-------------------+-------------+-------+------------+-------------------------------+---------------------+
| 107  | Robert Thompson   | San Antonio | TX    | 4444444444 | robert.thompson@example.com   | 2023-04-07 15:10:00 |
| 109  | William Hernandez | Dallas      | TX    | 7777777777 | william.hernandez@example.com | 2023-04-09 14:40:15 |
+------+-------------------+-------------+-------+------------+-------------------------------+---------------------+
2 rows in set (0.001 sec)

```

# Window Functions

- row_number : Assigns row number sequentially
- rank : Returns same rank if value is same but skips ranks
- dense rank : Returns same rank if value is same but does not skips ranks
- lead : Next record
- lag : Previous record
## row_number

```sql
MariaDB [b16]> SELECT eid, sal, row_number() over(order by sal ) as 'Row Number' from emp;
+------+-------+------------+
| eid  | sal   | Row Number |
+------+-------+------------+
|   12 | 10000 |          1 |
|    6 | 20000 |          2 |
|    6 | 20000 |          3 |
|    1 | 20000 |          4 |
|    1 | 20000 |          5 |
|    2 | 30000 |          6 |
|    2 | 30000 |          7 |
|    7 | 35000 |          8 |
|    7 | 35000 |          9 |
|    8 | 35000 |         10 |
|    8 | 35000 |         11 |
|    3 | 40000 |         12 |
|    3 | 40000 |         13 |
|    4 | 50000 |         14 |
|    4 | 50000 |         15 |
|    9 | 65000 |         16 |
|    9 | 65000 |         17 |
|   10 | 65000 |         18 |
|   10 | 65000 |         19 |
|   11 | 65000 |         20 |
|   11 | 65000 |         21 |
|    5 | 80000 |         22 |
|    5 | 80000 |         23 |
+------+-------+------------+
23 rows in set (0.001 sec)

MariaDB [b16]> SELECT eid, sal, row_number() over(order by sal desc) as 'Row Number' from emp;
+------+-------+------------+
| eid  | sal   | Row Number |
+------+-------+------------+
|    5 | 80000 |          1 |
|    5 | 80000 |          2 |
|    9 | 65000 |          3 |
|    9 | 65000 |          4 |
|   10 | 65000 |          5 |
|   10 | 65000 |          6 |
|   11 | 65000 |          7 |
|   11 | 65000 |          8 |
|    4 | 50000 |          9 |
|    4 | 50000 |         10 |
|    3 | 40000 |         11 |
|    3 | 40000 |         12 |
|    7 | 35000 |         13 |
|    7 | 35000 |         14 |
|    8 | 35000 |         15 |
|    8 | 35000 |         16 |
|    2 | 30000 |         17 |
|    2 | 30000 |         18 |
|    6 | 20000 |         19 |
|    6 | 20000 |         20 |
|    1 | 20000 |         21 |
|    1 | 20000 |         22 |
|   12 | 10000 |         23 |
+------+-------+------------+
23 rows in set (0.001 sec)
```

## rank

```sql
MariaDB [b16]> SELECT eid, sal, rank() over(order by sal) as 'Rank' from emp;
+------+-------+------------+
| eid  | sal   | Rank |
+------+-------+------------+
|   12 | 10000 |          1 |
|    1 | 20000 |          2 |
|    1 | 20000 |          2 |
|    6 | 20000 |          2 |
|    6 | 20000 |          2 |
|    2 | 30000 |          6 |
|    2 | 30000 |          6 |
|    8 | 35000 |          8 |
|    8 | 35000 |          8 |
|    7 | 35000 |          8 |
|    7 | 35000 |          8 |
|    3 | 40000 |         12 |
|    3 | 40000 |         12 |
|    4 | 50000 |         14 |
|    4 | 50000 |         14 |
|    9 | 65000 |         16 |
|    9 | 65000 |         16 |
|   10 | 65000 |         16 |
|   10 | 65000 |         16 |
|   11 | 65000 |         16 |
|   11 | 65000 |         16 |
|    5 | 80000 |         22 |
|    5 | 80000 |         22 |
+------+-------+------------+
23 rows in set (0.001 sec)

MariaDB [b16]> SELECT eid, sal, rank() over(order by sal desc) as 'Rank' from emp;
+------+-------+------------+
| eid  | sal   | Rank |
+------+-------+------------+
|    5 | 80000 |          1 |
|    5 | 80000 |          1 |
|    9 | 65000 |          3 |
|    9 | 65000 |          3 |
|   10 | 65000 |          3 |
|   10 | 65000 |          3 |
|   11 | 65000 |          3 |
|   11 | 65000 |          3 |
|    4 | 50000 |          9 |
|    4 | 50000 |          9 |
|    3 | 40000 |         11 |
|    3 | 40000 |         11 |
|    7 | 35000 |         13 |
|    7 | 35000 |         13 |
|    8 | 35000 |         13 |
|    8 | 35000 |         13 |
|    2 | 30000 |         17 |
|    2 | 30000 |         17 |
|    6 | 20000 |         19 |
|    6 | 20000 |         19 |
|    1 | 20000 |         19 |
|    1 | 20000 |         19 |
|   12 | 10000 |         23 |
+------+-------+------------+
23 rows in set (0.001 sec)
```

## Dense Rank

```sql
MariaDB [b16]> SELECT eid, sal, dense_rank() over(order by sal) as 'Dense Rank' from emp;
+------+-------+------------+
| eid  | sal   | Dense Rank |
+------+-------+------------+
|   12 | 10000 |          1 |
|    6 | 20000 |          2 |
|    6 | 20000 |          2 |
|    1 | 20000 |          2 |
|    1 | 20000 |          2 |
|    2 | 30000 |          3 |
|    2 | 30000 |          3 |
|    7 | 35000 |          4 |
|    7 | 35000 |          4 |
|    8 | 35000 |          4 |
|    8 | 35000 |          4 |
|    3 | 40000 |          5 |
|    3 | 40000 |          5 |
|    4 | 50000 |          6 |
|    4 | 50000 |          6 |
|    9 | 65000 |          7 |
|    9 | 65000 |          7 |
|   10 | 65000 |          7 |
|   10 | 65000 |          7 |
|   11 | 65000 |          7 |
|   11 | 65000 |          7 |
|    5 | 80000 |          8 |
|    5 | 80000 |          8 |
+------+-------+------------+
23 rows in set (0.001 sec)

MariaDB [b16]> SELECT eid, sal, dense_rank() over(order by sal desc) as 'Dense Rank' from emp;
+------+-------+------------+
| eid  | sal   | Dense Rank |
+------+-------+------------+
|    5 | 80000 |          1 |
|    5 | 80000 |          1 |
|    9 | 65000 |          2 |
|    9 | 65000 |          2 |
|   10 | 65000 |          2 |
|   10 | 65000 |          2 |
|   11 | 65000 |          2 |
|   11 | 65000 |          2 |
|    4 | 50000 |          3 |
|    4 | 50000 |          3 |
|    3 | 40000 |          4 |
|    3 | 40000 |          4 |
|    7 | 35000 |          5 |
|    7 | 35000 |          5 |
|    8 | 35000 |          5 |
|    8 | 35000 |          5 |
|    2 | 30000 |          6 |
|    2 | 30000 |          6 |
|    6 | 20000 |          7 |
|    6 | 20000 |          7 |
|    1 | 20000 |          7 |
|    1 | 20000 |          7 |
|   12 | 10000 |          8 |
+------+-------+------------+
23 rows in set (0.001 sec)
```

## Lag(col, n) 

```sql
MariaDB [b16]> SELECT eid, ename, sal, did, lag(sal,3) over(order by eid asc) as total_sal from emp;
+------+-----------+-------+------+-----------+
| eid  | ename     | sal   | did  | total_sal |
+------+-----------+-------+------+-----------+
|    1 | Vivek     | 20000 |   97 |      NULL |
|    1 | Vivek     | 20000 |   77 |      NULL |
|    2 | Abhishek  | 30000 |   77 |      NULL |
|    2 | Abhishek  | 30000 |   39 |     20000 |
|    3 | Shivam    | 40000 |   46 |     20000 |
|    3 | Shivam    | 40000 |   86 |     30000 |
|    4 | Neha      | 50000 |   11 |     30000 |
|    4 | Neha      | 50000 |   97 |     40000 |
|    5 | Akshay    | 80000 |   92 |     40000 |
|    5 | Akshay    | 80000 |   38 |     50000 |
|    6 | Omkar     | 20000 |   68 |     50000 |
|    6 | Omkar     | 20000 |   53 |     80000 |
|    7 | Kavita    | 35000 |   38 |     80000 |
|    7 | Kavita    | 35000 |   71 |     20000 |
|    8 | Gaurav    | 35000 |   10 |     20000 |
|    8 | Gaurav    | 35000 |   10 |     35000 |
|    9 | Pooja     | 65000 |   20 |     35000 |
|    9 | Pooja     | 65000 |   20 |     35000 |
|   10 | Komal     | 65000 |   10 |     35000 |
|   10 | Komal     | 65000 |   10 |     65000 |
|   11 | Xin       | 65000 |   10 |     65000 |
|   11 | Xin       | 65000 |   10 |     65000 |
|   12 | Mr. Beast | 10000 |   30 |     65000 |
+------+-----------+-------+------+-----------+
23 rows in set (0.001 sec)
```

## Lead(col,n)

```sql
MariaDB [b16]> SELECT eid, ename, sal, did, lead(sal,3) over(order by eid asc) as total_sal from emp;
+------+-----------+-------+------+-----------+
| eid  | ename     | sal   | did  | total_sal |
+------+-----------+-------+------+-----------+
|    1 | Vivek     | 20000 |   97 |     30000 |
|    1 | Vivek     | 20000 |   77 |     40000 |
|    2 | Abhishek  | 30000 |   77 |     40000 |
|    2 | Abhishek  | 30000 |   39 |     50000 |
|    3 | Shivam    | 40000 |   86 |     50000 |
|    3 | Shivam    | 40000 |   46 |     80000 |
|    4 | Neha      | 50000 |   97 |     80000 |
|    4 | Neha      | 50000 |   11 |     20000 |
|    5 | Akshay    | 80000 |   92 |     20000 |
|    5 | Akshay    | 80000 |   38 |     35000 |
|    6 | Omkar     | 20000 |   53 |     35000 |
|    6 | Omkar     | 20000 |   68 |     35000 |
|    7 | Kavita    | 35000 |   71 |     35000 |
|    7 | Kavita    | 35000 |   38 |     65000 |
|    8 | Gaurav    | 35000 |   10 |     65000 |
|    8 | Gaurav    | 35000 |   10 |     65000 |
|    9 | Pooja     | 65000 |   20 |     65000 |
|    9 | Pooja     | 65000 |   20 |     65000 |
|   10 | Komal     | 65000 |   10 |     65000 |
|   10 | Komal     | 65000 |   10 |     10000 |
|   11 | Xin       | 65000 |   10 |      NULL |
|   11 | Xin       | 65000 |   10 |      NULL |
|   12 | Mr. Beast | 10000 |   30 |      NULL |
+------+-----------+-------+------+-----------+
23 rows in set (0.001 sec)
```

### 23 Nov

## View

- CREATEd virtual table
- CREATE view view_name as SELECT_query;
- replace : 
- Types:
	- Simple : Uses simple statements like 'where', supports CRUD
	- Complex : Uses Joins, Group By, Window Functions, Set Operators
	- Materialized : Saved view on HDD

```sql
MariaDB [b16]> CREATE view ac_mumbai as SELECT * from account where city='Mumbai'; //Simple View


MariaDB [b16]> SELECT * from ac_pune;
+------+--------------+------+------------+-------+
| id   | name         | city | mob        | bal   |
+------+--------------+------+------------+-------+
|    7 | Anjali Mehta | Pune | 9234567890 | 17000 |
+------+--------------+------+------------+-------+

MariaDB [b16]> drop view ac_mumbai;
Query OK, 0 rows affected (0.004 sec)
```


## Indexing 

```sql
CREATE index idx_name on table_name(col_name);
```

- Clustered : Arranges records in order
- Non Clustered : MaINTains a reference table
- Show indexes : 
	- `show index from table_name;`

# Duplicate table with data

```sql
CREATE table emp_bak as SELECT * from emp;
```

# Duplicate table structure only

```sql
CREATE table emp_test as SELECT * from emp where 1 = 0;
```

# INSERT from another table

```sql
INSERT INTo emp_test SELECT * from emp where eid < 5;
```

# Run .sql files

```sql
source .sql_file_ocation
```

# Misc

- `if not exists` : only if the target does not already exist
- `if exists` : only if the target exists
# Normalization & DeNormalization

Process of organizing data INTo multiple related tables to eliminate redundancy and dependency.

## Goals

- Minimize redundancy.
- Avoid data anomalies (INSERTion, UPDATE, and deletion).
- 1NF (First Normal Form)
	- Ensures that each column contains atomic values (no repeating groups or arrays).
- 2NF (Second Normal Form):
    - Satisfies 1NF and removes partial dependencies (dependencies on part of a composite primary key).
- 3NF (Third Normal Form):
    - Satisfies 2NF and removes transitive dependencies (non-key columns depending on other non-key columns).
- BCNF (Boyce-Codd Normal Form):
	- A stricter version of 3NF where every determinant is a candidate key.



