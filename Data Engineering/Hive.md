- Data Warehouse tool
- Store data from multiple sources (EMR, RDBMS, CSV files)
- Used for Data Analysis
- SQL like operations can be performed
- Provides HQL(Hive Query Language)
- OLAP (Online Analytical Processing) tool

# Create External Table

- Managed by the user
- Stored on User Managed location on HDFS
- Does not support truncate
- Drop deletes tables, does not delete data on HDFS

```sql
hive> create external table cust(cid int, name string) 
      row format delimited fields terminated by ','
      location '/cust';
```

# Create Internal Table

- Managed by Hive
- Stored on Hive Managed location on HDFS
- Supports truncate
- Default Hive Location -> `HDFS/user/hive/warehouse/db_name.db/table_name`
- Drop deletes tables + delete data from HDFS

```sql
hive> create table empin(eid int, ename string, ecity string) 
      row format delimited fields terminated by '|';     
```

# Load Data to Hive

### from Local

```sql 
hive> load data local inpath '/path/to/local/file' into table db_name.table_name;
```

### from HDFS

```sql
hive> load data inpath '/path/on/hadoop/to/file' into table db_name.table_name;
```


# Optimization Techniques

## 1. Hive Partitioning 

- Sub division of table
- Stored data as per column in HDFS
- Separate folders for unique values 

```sql
hive> create table cust(cid int, name string) 
	  partitioned by (city string) 
	  row format delimited fields terminated by ',';
```
### Static Partitioning 

- Explicitly define   

```sql
hive> load data local inpath '/home/hadoop/pune.txt' into table cust partition(city="Pune");
```

### Dynamic Partitioning

- Create a temporary table to load data
- Then load data from temporary table to partitioned table

```sql
hive> create table tmp ( cid int, cname string, city string) row format delimited fields terminated by ',';
OK
Time taken: 0.086 seconds

hive> load data local inpath '/home/hadoop/data.txt' into table tmp;
Loading data to table default.tmp
OK
Time taken: 0.266 seconds

hive> create table cust(cid int, name string) 
	  partitioned by (city string) 
	  row format delimited fields terminated by ',';
	  
hive> insert into cust_dp partition(city) select * from tmp;
```

- Multi column partition

```sql
hive> create table tmp ( cid int, cname string, city string) row format delimited fields terminated by ',';
OK
Time taken: 0.086 seconds

hive> load data local inpath '/home/hadoop/data.txt' into table tmp;
Loading data to table default.tmp
OK
Time taken: 0.266 seconds

hive> create table cust(cid int, name string) 
	  partitioned by (state string, city string) 
	  row format delimited fields terminated by ',';

hive> insert into cust_dp partition(state, city) select * from tmp;
```

## 2. Bucketing

- Used when unequal

```sql
hive> create table emp_b (eid int,ename string,city string)
	  CLUSTERED by (eid) into 4 buckets
	  row format delimited
	  fields terminated by ',';

hive> insert into emp_b select * from tmpemp;
```

##  3. Execution Engine

- Map Reduce
- Tez
##  4. File Formats

- Text File
- Sequence File
- RCFile
- ORC (Recommended)
- Parquet
- Avro

```sql
hive> create table std_p (roll int,name string,marks array<int>)
	> row format delimited
	> fields terminated by ','
	> collection items terminated by '|'
	> STORED AS PARQUET;

hive> create table std_p (roll int,name string,marks array<int>)
	> row format delimited
	> fields terminated by ','
	> collection items terminated by '|'
	> STORED AS ORC;
	
	
hive> create table std_p (roll int,name string,marks array<int>)
	> row format delimited
	> fields terminated by ','
	> collection items terminated by '|'
	> STORED AS AVRO;
	
hive> create table std_p (roll int,name string,marks array<int>)
	> row format delimited
	> fields terminated by ','
	> collection items terminated by '|'
	> STORED AS RCFILE;
	
	hive> create table std_p (roll int,name string,marks array<int>)
	> row format delimited
	> fields terminated by ','
	> collection items terminated by '|'
	> STORED AS SEQUENCEFILE;
	
	hive> create table std_p (roll int,name string,marks array<int>)
	> row format delimited
	> fields terminated by ','
	> collection items terminated by '|'
	> STORED AS TEXTFILE;
```


# 5. Map Join / Broadcast Join

In Map Join where smaller table is loaded into memory and the join

# 6.  SMB Join

- Sort Merge Bucket Join
- 

# 7.  Vectorization

# 8. Indexing

- Bitmap -> Duplicate Values
- Compact Indexing -> Unique Values

```sql
hive> create index <idx_name> on table <table_name>(column_name) as 'Type_Of_Idx'
	with DEFERRED rebuild;
hive> create index cust_idx on table cust(cid) as 'COMPACT' with DEFERRED
	> rebuild;
```

# Complex Data Types

## Array

- Stores similar types of data

```sql
hive> create table student(roll int, name string, marks array<int>)
	> row format delimited fields terminated by ','
	> collection items terminated by '|';
```

## Struct

```sql
hive> create table student(roll int, name string, marks struct<area:string,city:string,state:string,pin:int>)
	> row format delimited fields terminated by ','
	> collection items terminated by '|';
```

## Map

```sql
hive> create table student(roll int, name string, cert map<string, string>)
	> row format delimited fields terminated by ','
	> collection items terminated by '|'
	> map keys terminated by ':';
```

# Skip Header when loading data

```sql
hive> create table emp (eid int,ename string,city string)
	> row format delimited
	> fields terminated by ','
	> tblproperties("skip.header.line.count"="1");
```

# Run hive queries from the Linux Terminal

```bash
 $ hive -e "show databases;"
```

# Drop non empty database

```sql
hive> drop database niranjan cascade;
```

# Duplicate table with structure

```sql
hive> create table student like std;
```
# Duplicate data

```sql

# Create table and duplicate
hive> create table student_bkp as select * from student;

# 

```
# Lateral View

```sql
hive> SELECT author, tmp_book_name FROM dtls LATERAL VIEW EXPLODE(books)
	> tmp_view AS tmp_book_name;
```

# Hive Query Language (HQL)

```bash
$ hive -f script_name.hql
```

```sql
-- Owner : Niranjan Fartare
-- Script Name : MyScript.hql
-- Run Command : hive -f MyScript.hql
-- Purpose : Create Table
-- Creation Date : 29/12/2024
-- Modification Date : NA
-- Version : 1.0

set dbname=dev;

create database if not exists ${hiveconf:dbname};

use ${hiveconf:dbname};

create table if not exists dtls (author string,books array<string>)
row format delimited fields terminated by ','
collection items terminated by '|';

load data local inpath '/home/hadoop/dtl.txt' into table dtls;

create table if not exists ${hiveconf:dbname}.dtls_bkp as select * from dtls;

create table if not exists ${hiveconf:dbname}.dtls1 like dtls;

insert into dtls1 select * from dtls;
```


# IMP

- What is Data Warehouse?
- Difference between OLTP & OLAP?
- Difference between Database, Data Warehouse, Data Lake?
- Difference between Internal & External table?
- Optimization Techniques
- Explode & Lateral View
- Complex Data Structures
- HQL Scripting


