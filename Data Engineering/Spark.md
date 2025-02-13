- In Memory Processing
- 10x Faster than Map Reduce
- Process structured, semi structured and unstructured data
- Programming Module
- Computation Framework

# Questions

- Spark vs Map Reduce
- OLAP vs OLTP

# RDD - Resilient / Flexible Distributed Dataset
 
 - Object of Spark Core
 - Basic storage element in Spark Core
 - Data distributed on multiple partitions

## Ways to create RDD

- From Collections (List, Set, Dict)
- From External Source (HDFS, RDS, S3)
- From existing RDD

```python
from pyspark.sql import SparkSession  
  
spark = SparkSession.builder.appName("WordCount").getOrCreate()  
ls = ["Java", "Python", "Scala"] # Collection as input
rdd = spark.sparkContext.textFile("data.txt")  # File as input
rdd = spark.sparkContext.parallelize(ls)  

# print(rdd.collect()) # Get Data from RDD

# print(rdd.getNumPartitions()) # Get Number of Partitions

# Perform Operation on RDD
print(rdd.map(lambda x : x + " is a programming language.").collect()) 
rdd1.saveAsTextFile("sparkOutput1")
```

```python
from pyspark.sql import SparkSession  

spark = SparkSession.builder.appName("extractData").getOrCreate()  

rdd = spark.sparkContext.textFile("data.txt")  
rdd1 = rdd.filter(lambda x: ("Pune" in x))  

print(rdd1.collect())  
rdd1.saveAsTextFile("sparkOutput1")
```

## Operations on RDD

- Transformation : Get a RDD as a output when processing
	- `map`
	- `filter`
	- `reduce`
- Action : Get a Collection or Value as a output
	- `collect` : Collect result of transformations from partitions
	- `count` : Count number of items in RDD
	- `take(n)` : Output top `n` items
	- `saveAsTextFile()` : Save output as txt file

### Transformations

- Narrow Transformation : Perform operations on specific partitions, (Eg, `map`, `filter`)
- Wide Transformation : Perform operations on multiple partitions, (Wg, `reduceByKey`, `Joins`)

![[Screenshot 2025-02-02 at 11-49-31 Learning Spark Second Edition - LearningSpark2.0.pdf.png]]

## Lazy Evaluation

- `Transformations` are not called until `Actions` are performed.

# Optimization Techniques in Spark

## Re-partition and Coalesce

- Both are optimization techniques in Spark.
- `repartition()` is used increase or decrease the number of partitions.
- `repartition()` tries to create partitions of equal size.
- `coalesce()` is used to decrease the number of partitions.
- `repartition()` creates new partitions, while `coalesce()` uses existing partitions.
- More shuffling in `reparition()` as compared to `coalesce`.
- Syntax : `newRDD = rdd.repartition(n)`, `n` is the number of partitions.
- Syntax : `newRDD = rdd.coalesce(n)`, `n` is the number of partitions to decrease.

## Persist and Cache

- `persist()` is used to store the result of an Action into the memory.
- Syntax  : `rdd.persist()`
- `cahce()` is fault tolerent.
- Syntax : `rdd.cache()`

### Persist storage levels

- `rdd.persist()` 

# Lineage Graph

# DAG

# DAG Scheduler (Stages)

# Tasks

# Jobs

- For every `Action` a new Spark Job is created

# Deployment Mode

- Decided based on where the driver code is executed
- **Client Deployment Mode** : Driver Program is running on the client machine where client submits the code
- **Cluster Deployment Mode** : Driver Program is running on one of the machine in the Cluster.

## Client Deployment Mode 

- In this mode, the Spark driver program runs on the client machine (the machine where the Spark application is submitted)
  The client is responsible for the execution of the driver code, which includes the SparkContext and the logic for the application. 
- The driver communicates with the cluster manager (like YARN) to request resources and schedule tasks. 
- This mode is typically used for interactive applications or when the user wants to run Spark jobs from a local machine or a development environment.

### Advantages

- Easier to debug and develop applications since the driver runs locally.
- Suitable for small-scale applications or testing.
### Disadvantages

- Limited by the resources of the client machine.
- Network latency can be an issue, especially for large datasets.

## Cluster Deployment Mode

- In this mode, the Spark driver program runs on one of the machines in the cluster.
- The client submits the application to the cluster manager, which then allocates resources and runs the driver on one of the cluster nodes. 
- The driver handles the scheduling of tasks and the coordination of the application, while the actual data processing occurs on the worker nodes. 
- This mode is suitable for production environments and large-scale data processing tasks.

### Advantages

- Better resource utilization since the driver runs on a cluster node. 
- Can handle larger datasets and more complex applications. 
- Reduced network latency as the driver is closer to the data.     
### Disadvantages

- More complex to set up and manage. 
- Debugging can be more challenging since the driver is not running on the client machine.

# Paired RDD

- RDDs with Key Value pairs
# Spark Job Flow

1. **Job Submission**: User submits a Spark application.
2. **Driver Program**: Initializes SparkContext and builds the execution plan.
3. **DAG Creation**: Constructs a Directed Acyclic Graph representing the job.
4. **Job Scheduling**: DAG scheduler breaks the job into stages.
5. **Task Scheduling**: Task scheduler allocates tasks to executors.
6. **Task Execution**: Executors process data and execute tasks.
7. **Data Shuffling**: Redistributes data for wide transformations.
8. **Result Collection**: Driver collects results from tasks.
9. **Job Completion**: Job finishes, and resources are cleaned up.


# Spark SQL

# Catalyst Optimizer

# DF

- Data Frame
- `df.show()` : Shows top 20 records from the Data Frame
- `df.show(n)` : Shows top `n` records from the Data Frame
- `df.show(n, True/False)` : Shows top `n` records from the Data Frame and set truncated values `True/False`
- `df.createOrReplaceTempView("view")` : Create a `view` based on `df`

# Pure SQL Data Processing

## Read

```python
# emp.csv
#eid,ename,did,sal,city
#1,Karan,10,25000,Pune
#2,Rahul,20,30000,
#3,Sneha,10,,Pune
#4,Amit,30,35000,Mumbai
#5,Neha,20,30000,
#6,Rajesh,10,,Pune
#7,Pooja,30,40000,Delhi
#8,Sameer,,35000,Mumbai
#9,Ankita,10,30000,Hyderabad
#10,Vikram,30,40000,

from pyspark.sql import SparkSession  
spark = SparkSession.builder.appName("WordCount").getOrCreate()  
  
df=spark.read.format("CSV").option("header","true")
		.option("delimiter",",")
		.option("inferschema","true") # Identify correct datatype
	    .load("/home/niranjan/Documents/Sayu/emp.csv")  
print(df.show())  
df.printSchema()

# Output of print(df.show())

+---+------+----+-----+---------+
|eid| ename| did|  sal|     city|
+---+------+----+-----+---------+
|  1| Karan|  10|25000|     Pune|
|  2| Rahul|  20|30000|     NULL|
|  3| Sneha|  10| NULL|     Pune|
|  4|  Amit|  30|35000|   Mumbai|
|  5|  Neha|  20|30000|     NULL|
|  6|Rajesh|  10| NULL|     Pune|
|  7| Pooja|  30|40000|    Delhi|
|  8|Sameer|NULL|35000|   Mumbai|
|  9|Ankita|  10|30000|Hyderabad|
| 10|Vikram|  30|40000|     NULL|
+---+------+----+-----+---------+


# Output of df.printSchema()

root
 |-- eid: integer (nullable = true)
 |-- ename: string (nullable = true)
 |-- did: integer (nullable = true)
 |-- sal: integer (nullable = true)
 |-- city: string (nullable = true)
```

## Process

```python

from pyspark.sql import SparkSession  
spark = SparkSession.builder.appName("WordCount").getOrCreate()  
  
df=(spark.read.format("CSV").option("header","true")  
    .option("delimiter",",")  
    .option("inferschema","true")  
    .load("/home/niranjan/Documents/Sayu/emp.csv"))  
# print(df.show())  
# df.printSchema()  
  
df.createOrReplaceTempView("emp")  
df1 = spark.sql("""SELECT * FROM emp WHERE city = 'Pune' """)  
df1.show()  
  
df1.createOrReplaceTempView("emp1")  
df2 = spark.sql("""SELECT * FROM emp1 WHERE sal IS NULL """)  
df2.show()

# Output of df1.show()
+---+------+---+-----+----+
|eid| ename|did|  sal|city|
+---+------+---+-----+----+
|  1| Karan| 10|25000|Pune|
|  3| Sneha| 10| NULL|Pune|
|  6|Rajesh| 10| NULL|Pune|
+---+------+---+-----+----+

# Output of df2.show()

+---+------+---+----+----+
|eid| ename|did| sal|city|
+---+------+---+----+----+
|  3| Sneha| 10|NULL|Pune|
|  6|Rajesh| 10|NULL|Pune|
+---+------+---+----+----+
```

## Write

```python
from pyspark.sql import SparkSession  
spark = SparkSession.builder.appName("WordCount").getOrCreate()  
  
df=(spark.read.format("CSV").option("header","true")  
    .option("delimiter",",")  
    .option("inferschema","true")  
    .load("/home/niranjan/Documents/Sayu/emp.csv"))  
# print(df.show())  
# df.printSchema()  
  
df.createOrReplaceTempView("emp")
df1 = spark.sql("""SELECT * FROM emp""")  
  
# df1.show()  
  
df1.createOrReplaceTempView("emp1")
df2 = spark.sql("""SELECT * FROM emp1 WHERE sal > 20000 """)
  
# df2.show()  
# print(df2.rdd.getNumPartitions())  
  
df2.write.format("CSV").option("header","true").option("delimiter","|").save("/home/niranjan/Documents/Sayu/empop1")
```

```python
from pyspark.sql import SparkSession  
spark = SparkSession.builder.appName("WordCount").getOrCreate()  
  
df_emp = (spark.read.format("CSV")  
      .option("header","true")  
      .option("delimiter",",")  
      .option("inferschema","true")  
      .load("/home/niranjan/Documents/Sayu/emp.csv"))  
  
df_dept = (spark.read.format("CSV")  
      .option("header","true")  
      .option("delimiter",",")  
      .option("inferschema","true")  
      .load("/home/niranjan/Documents/Sayu/dept.csv"))  
  
df_emp.createTempView("emp")  
df_dept.createTempView("dept")  
  
df_res = spark.sql("""SELECT eid, ename, sal, dname FROM emp JOIN dept ON emp.did = dept.did""")  
  
df_res.show()  
  
(df_res.write.format("CSV")  
    .option("header","true")  
    .option("delimiter","|")  
    .save("/home/niranjan/Documents/Sayu/empop3"))

# Output

+---+------+-----+-------+
|eid| ename|  sal|  dname|
+---+------+-----+-------+
|  1| Karan|25000|     IT|
|  2| Rahul|30000|     HR|
|  3| Sneha| NULL|     IT|
|  4|  Amit|35000|Finance|
|  5|  Neha|30000|     HR|
|  6|Rajesh| NULL|     IT|
|  7| Pooja|40000|Finance|
|  9|Ankita|30000|     IT|
| 10|Vikram|40000|Finance|
+---+------+-----+-------+
```

## Data Frame API Functions

```python
from pyspark.sql import SparkSession  
spark = SparkSession.builder.appName("WordCount").getOrCreate()  

# READ

df_emp = (spark.read.format("CSV")  
      .option("header","true")  
      .option("delimiter",",")  
      .option("inferschema","true")  
      .load("/home/niranjan/Documents/Sayu/emp.csv"))  

# PROCESS

df1 = df_emp.where("sal > 10000")

# WRITE

(df1.write.format("CSV")  
    .option("header","true")  
    .option("delimiter","|")  
    .save("/home/niranjan/Documents/Sayu/empop3"))

# Output

+---+------+----+-----+---------+
|eid| ename| did|  sal|     city|
+---+------+----+-----+---------+
|  1| Karan|  10|25000|     Pune|
|  2| Rahul|  20|30000|     NULL|
|  4|  Amit|  30|35000|   Mumbai|
|  5|  Neha|  20|30000|     NULL|
|  7| Pooja|  30|40000|    Delhi|
|  8|Sameer|NULL|35000|   Mumbai|
|  9|Ankita|  10|30000|Hyderabad|
| 10|Vikram|  30|40000|     NULL|
+---+------+----+-----+---------+

```

### Select

- Syntax : `df.select("col")`
- Eg, : `df_emp.select("ename", "eid", "sal")`
- Eg, : `df_emp.select("*")`
- Eg, : `df_emp.select(col("ename"), col("sal"))`
- Eg, : `df_emp.select(df_emp['ename'], df_emp['sal'])`

### Alias

```python
df_emp.select(df_emp['ename'].alias("Employee Name"), df_emp['sal'].alias("Monthly Salary"), (df_emp['sal']*12).alias("Annual Salary")).show()

# Output

+-------------+--------------+-------------+
|Employee Name|Monthly Salary|Annual Salary|
+-------------+--------------+-------------+
|        Karan|         25000|       300000|
|        Rahul|         30000|       360000|
|        Sneha|          NULL|         NULL|
|         Amit|         35000|       420000|
|         Neha|         30000|       360000|
|       Rajesh|          NULL|         NULL|
|        Pooja|         40000|       480000|
|       Sameer|         35000|       420000|
|       Ankita|         30000|       360000|
|       Vikram|         40000|       480000|
+-------------+--------------+-------------+
```

### lit 



```python
df_emp.withColumn("Status",lit("Active")).show()

# Output 

+---+------+----+-----+---------+------+
|eid| ename| did|  sal|     city|Status|
+---+------+----+-----+---------+------+
|  1| Karan|  10|25000|     Pune|Active|
|  2| Rahul|  20|30000|     NULL|Active|
|  3| Sneha|  10| NULL|     Pune|Active|
|  4|  Amit|  30|35000|   Mumbai|Active|
|  5|  Neha|  20|30000|     NULL|Active|
|  6|Rajesh|  10| NULL|     Pune|Active|
|  7| Pooja|  30|40000|    Delhi|Active|
|  8|Sameer|NULL|35000|   Mumbai|Active|
|  9|Ankita|  10|30000|Hyderabad|Active|
| 10|Vikram|  30|40000|     NULL|Active|
+---+------+----+-----+---------+------+
```

### withColumn

- Used to add a new column in existing Data Frame

```python
df_emp.withColumn("Annual Salary", df_emp['sal']*12).show()

# Output 

+---+------+----+-----+---------+-------------+
|eid| ename| did|  sal|     city|Annual Salary|
+---+------+----+-----+---------+-------------+
|  1| Karan|  10|25000|     Pune|       300000|
|  2| Rahul|  20|30000|     NULL|       360000|
|  3| Sneha|  10| NULL|     Pune|         NULL|
|  4|  Amit|  30|35000|   Mumbai|       420000|
|  5|  Neha|  20|30000|     NULL|       360000|
|  6|Rajesh|  10| NULL|     Pune|         NULL|
|  7| Pooja|  30|40000|    Delhi|       480000|
|  8|Sameer|NULL|35000|   Mumbai|       420000|
|  9|Ankita|  10|30000|Hyderabad|       360000|
| 10|Vikram|  30|40000|     NULL|       480000|
+---+------+----+-----+---------+-------------+
```

### when..otherwise

```python
df_emp.withColumn("bonus", when(df_emp['city'] == 'Pune',lit(500)).when(df_emp['city'] == 'Mumbai',lit(1000)).otherwise(lit(200)) ).show()

# Output

+---+------+----+-----+---------+-----+
|eid| ename| did|  sal|     city|bonus|
+---+------+----+-----+---------+-----+
|  1| Karan|  10|25000|     Pune|  500|
|  2| Rahul|  20|30000|     NULL|  200|
|  3| Sneha|  10| NULL|     Pune|  500|
|  4|  Amit|  30|35000|   Mumbai| 1000|
|  5|  Neha|  20|30000|     NULL|  200|
|  6|Rajesh|  10| NULL|     Pune|  500|
|  7| Pooja|  30|40000|    Delhi|  200|
|  8|Sameer|NULL|35000|   Mumbai| 1000|
|  9|Ankita|  10|30000|Hyderabad|  200|
| 10|Vikram|  30|40000|     NULL|  200|
+---+------+----+-----+---------+-----+
```

### where

```python
df_emp.where(df_emp['city']=="Pune").show()

# Output

+---+------+---+-----+----+
|eid| ename|did|  sal|city|
+---+------+---+-----+----+
|  1| Karan| 10|25000|Pune|
|  3| Sneha| 10| NULL|Pune|
|  6|Rajesh| 10| NULL|Pune|
+---+------+---+-----+----+

df_emp.where((df_emp['city']=="Pune") & (df_emp['sal']>=20000)).show()

+---+-----+---+-----+----+
|eid|ename|did|  sal|city|
+---+-----+---+-----+----+
|  1|Karan| 10|25000|Pune|
+---+-----+---+-----+----+

```

### isNull & isNotNull

```python
df_emp.where(df_emp['sal'].isNull()).show()

# Output

+---+------+---+----+----+
|eid| ename|did| sal|city|
+---+------+---+----+----+
|  3| Sneha| 10|NULL|Pune|
|  6|Rajesh| 10|NULL|Pune|
+---+------+---+----+----+

df_emp.where(df_emp['sal'].isNotNull()).show()

# Output

+---+------+----+-----+---------+
|eid| ename| did|  sal|     city|
+---+------+----+-----+---------+
|  1| Karan|  10|25000|     Pune|
|  2| Rahul|  20|30000|     NULL|
|  4|  Amit|  30|35000|   Mumbai|
|  5|  Neha|  20|30000|     NULL|
|  7| Pooja|  30|40000|    Delhi|
|  8|Sameer|NULL|35000|   Mumbai|
|  9|Ankita|  10|30000|Hyderabad|
| 10|Vikram|  30|40000|     NULL|
+---+------+----+-----+---------+
```

### isin

```python
df_emp.where(df_emp['city'].isin('Pune','Mumbai')).show()

# Output

+---+------+----+-----+------+
|eid| ename| did|  sal|  city|
+---+------+----+-----+------+
|  1| Karan|  10|25000|  Pune|
|  3| Sneha|  10| NULL|  Pune|
|  4|  Amit|  30|35000|Mumbai|
|  6|Rajesh|  10| NULL|  Pune|
|  8|Sameer|NULL|35000|Mumbai|
+---+------+----+-----+------+
```

### isnotin

```python
df_emp.where(~(df_emp['city'].isin('Pune','Mumbai'))).show()

# Output

|eid| ename|did|  sal|     city|
+---+------+---+-----+---------+
|  7| Pooja| 30|40000|    Delhi|
|  9|Ankita| 10|30000|Hyderabad|
+---+------+---+-----+---------+
```
### filter

```python
df_emp.filter(df_emp['city'].isin('Pune','Mumbai')).show()

+---+------+----+-----+------+
|eid| ename| did|  sal|  city|
+---+------+----+-----+------+
|  1| Karan|  10|25000|  Pune|
|  3| Sneha|  10| NULL|  Pune|
|  4|  Amit|  30|35000|Mumbai|
|  6|Rajesh|  10| NULL|  Pune|
|  8|Sameer|NULL|35000|Mumbai|
+---+------+----+-----+------+

df_emp.filter(~(df_emp['city'].isin('Pune','Mumbai'))).show()

+---+------+---+-----+---------+
|eid| ename|did|  sal|     city|
+---+------+---+-----+---------+
|  7| Pooja| 30|40000|    Delhi|
|  9|Ankita| 10|30000|Hyderabad|
+---+------+---+-----+---------+
```

### like

```python

df_emp.filter(df_emp['city'].like("%P%")).show()

+---+------+---+-----+----+
|eid| ename|did|  sal|city|
+---+------+---+-----+----+
|  1| Karan| 10|25000|Pune|
|  3| Sneha| 10| null|Pune|
|  6|Rajesh| 10| null|Pune|
+---+------+---+-----+----+

df_emp.filter(df_emp['city'].like("%m%")).show()

+---+------+----+-----+------+
|eid| ename| did|  sal|  city|
+---+-----------+-----+------+
|  4|  Amit|  30|35000|Mumbai|
|  8|Sameer|null|35000|Mumbai|
+---+------+----+-----+------+

df_emp.filter(df_emp['city'].like("%d")).show()

+---+------+---+-----+---------+
|eid| ename|did|  sal|     city|
+---+------+---+-----+---------+
|  9|Ankita| 10|30000|Hyderabad|
+---+------+---+-----+---------+
```

### withColumnRenamed

```python
df_emp.withColumnRenamed("city","City").show()

+---+------+----+-----+---------+
|eid| ename| did|  sal|     City|
+---+------+----+-----+---------+
|  1| Karan|  10|25000|     Pune|
|  2| Rahul|  20|30000|     NULL|
|  3| Sneha|  10| NULL|     Pune|
```

### drop

```python
df1 = df_emp.drop("city","sal")
df1.show()

+---+------+----+
|eid| ename| did|
+---+------+----+
|  1| Karan|  10|
|  2| Rahul|  20|
|  3| Sneha|  10|
|  4|  Amit|  30|
|  5|  Neha|  20|
|  6|Rajesh|  10|
|  7| Pooja|  30|
|  8|Sameer|NULL|
|  9|Ankita|  10|
| 10|Vikram|  30|
+---+------+----+
```

### fillna

Replace null with given value

```python
df_emp.fillna("NA").show()

+---+------+----+-----+---------+
|eid| ename| did|  sal|     city|
+---+------+----+-----+---------+
|  1| Karan|  10|25000|     Pune|
|  2| Rahul|  20|30000|       NA|
|  3| Sneha|  10| NULL|     Pune|
|  4|  Amit|  30|35000|   Mumbai|
|  5|  Neha|  20|30000|       NA|
|  6|Rajesh|  10| NULL|     Pune|
|  7| Pooja|  30|40000|    Delhi|
|  8|Sameer|NULL|35000|   Mumbai|
|  9|Ankita|  10|30000|Hyderabad|
| 10|Vikram|  30|40000|       NA|
+---+------+----+-----+---------+


df_emp.fillna(0).show()

+---+------+---+-----+---------+
|eid| ename|did|  sal|     city|
+---+------+---+-----+---------+
|  1| Karan| 10|25000|     Pune|
|  2| Rahul| 20|30000|     NULL|
|  3| Sneha| 10|    0|     Pune|
|  4|  Amit| 30|35000|   Mumbai|
|  5|  Neha| 20|30000|     NULL|
|  6|Rajesh| 10|    0|     Pune|
|  7| Pooja| 30|40000|    Delhi|
|  8|Sameer|  0|35000|   Mumbai|
|  9|Ankita| 10|30000|Hyderabad|
| 10|Vikram| 30|40000|     NULL|
+---+------+---+-----+---------+

df_emp.fillna("NA").fillna(0).show()

+---+------+---+-----+---------+
|eid| ename|did|  sal|     city|
+---+------+---+-----+---------+
|  1| Karan| 10|25000|     Pune|
|  2| Rahul| 20|30000|       NA|
|  3| Sneha| 10|    0|     Pune|
|  4|  Amit| 30|35000|   Mumbai|
|  5|  Neha| 20|30000|       NA|
|  6|Rajesh| 10|    0|     Pune|
|  7| Pooja| 30|40000|    Delhi|
|  8|Sameer|  0|35000|   Mumbai|
|  9|Ankita| 10|30000|Hyderabad|
| 10|Vikram| 30|40000|       NA|
+---+------+---+-----+---------+
```

### dropna

Drop records with `null` value

```python
df_emp.dropna().show()

+---+------+---+-----+---------+
|eid| ename|did|  sal|     city|
+---+------+---+-----+---------+
|  1| Karan| 10|25000|     Pune|
|  4|  Amit| 30|35000|   Mumbai|
|  7| Pooja| 30|40000|    Delhi|
|  9|Ankita| 10|30000|Hyderabad|
+---+------+---+-----+---------+
```

### joins

```python
df_adv.py in pycharm
```

### Window Functions
