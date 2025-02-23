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

## Data Frame API Functionsy

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


### Group By 

```python
df1=df.groupBy("did").count()  
df1.show()  
  
df1=df.groupBy("did").sum("sal")  
df1.show()  
  
df1=df.groupBy("did").max("sal")  
df1.show()  
  
df1=df.groupBy("did").min("sal")  
df1.show()  
  
df1=df.groupBy("did").avg("sal")  
df1.show()  
  
## fiter groupBy 

df1=df.groupBy("did").avg("sal").filter(df["did"]==101)  
df1.show()

## Output

+---+-----+
|did|count|
+---+-----+
|101|    6|
|103|    4|
|102|    5|
+---+-----+

+---+--------+
|did|sum(sal)|
+---+--------+
|101|  311000|
|103|  287000|
|102|  308000|
+---+--------+

+---+--------+
|did|max(sal)|
+---+--------+
|101|   55000|
|103|   75000|
|102|   65000|
+---+--------+

+---+--------+
|did|min(sal)|
+---+--------+
|101|   48000|
|103|   70000|
|102|   58000|
+---+--------+

+---+------------------+
|did|          avg(sal)|
+---+------------------+
|101|51833.333333333336|
|103|           71750.0|
|102|           61600.0|
+---+------------------+

+---+------------------+
|did|          avg(sal)|
+---+------------------+
|101|51833.333333333336|
+---+------------------+
```

### aggregate  functions


### distinct

- Removes duplicates based on All Columns

```python
df.distinct().show()  

## Output

+---+------+---+-----+
|eid| ename|did|  sal|
+---+------+---+-----+
|  2|  ABCD|102|60000|
|  3| Arjun|101|55000|
|  5| Karan|102|65000|
|  1| Aarav|101|50000|
|  4| Rohan|103|70000|
|  2|Vihaan|102|60000|
+---+------+---+-----+
```

### dropDuplicates

- By default removes duplicates based on all columns

```python
df.dropDuplicates().show()  
  
df.dropDuplicates(["eid"]).show()

## output

+---+------+---+-----+
|eid| ename|did|  sal|
+---+------+---+-----+
|  2|  ABCD|102|60000|
|  3| Arjun|101|55000|
|  5| Karan|102|65000|
|  1| Aarav|101|50000|
|  4| Rohan|103|70000|
|  2|Vihaan|102|60000|
+---+------+---+-----+

+---+------+---+-----+
|eid| ename|did|  sal|
+---+------+---+-----+
|  1| Aarav|101|50000|
|  2|Vihaan|102|60000|
|  3| Arjun|101|55000|
|  4| Rohan|103|70000|
|  5| Karan|102|65000|
+---+------+---+-----+
```

### set operators

```python
# UnionALL
df1.union(df2).show()  
  
# UnionAll  
df1.union(df2).distinct().show()  
  
# Intersect  
df1.intersect(df2).show()  
  
# Except  
df1.exceptAll(df2).show()
df2.exceptAll(df1).show()

## Output

+---+------+------+
|eid| ename|  city|
+---+------+------+
|  1| karan|  pune|
|  2|rajesh|  pune|
|  3|rakesh|mumbai|
|  1| karan|  pune|
|  2|rajesh|  pune|
|  4|  Bond| Delhi|
+---+------+------+

+---+------+------+
|eid| ename|  city|
+---+------+------+
|  3|rakesh|mumbai|
|  2|rajesh|  pune|
|  1| karan|  pune|
|  4|  Bond| Delhi|
+---+------+------+

+---+------+----+
|eid| ename|city|
+---+------+----+
|  2|rajesh|pune|
|  1| karan|pune|
+---+------+----+

+---+------+------+
|eid| ename|  city|
+---+------+------+
|  3|rakesh|mumbai|
+---+------+------+

+---+-----+-----+
|eid|ename| city|
+---+-----+-----+
|  4| Bond|Delhi|
+---+-----+-----+
```

### Date Functions

```python
from pyspark.sql.functions import *

df2.withColumn("pcd",date_add(df2['doj'],90)).show()  
df2.withColumn("dcd",date_sub(df2['doj'],2)).show()  
df2.withColumn("year",year(df2['doj'])).show()  
df2.withColumn("month",month(df2['doj'])).show()  
df2.withColumn("dayOfMonth",dayofmonth(df2['doj'])).show()  
df2.withColumn("hour",hour(df2['doj'])).show()  
df2.withColumn("minute",minute(df2['doj'])).show()  
df2.withColumn("seconds",second(df2['doj'])).show()
df2.withColumn("dayOfWeek",dayofweek(df2['doj'])).show()

## Output

+---+------+------+-------------------+----------+
|eid| ename|  city|                doj|       pcd|
+---+------+------+-------------------+----------+
|  1| karan|  pune|2020-01-31 10:15:25|2020-04-30|
|  2|rajesh|  pune|2021-05-07 12:25:11|2021-08-05|
|  3|rakesh|mumbai|2023-03-02 11:45:25|2023-05-31|
+---+------+------+-------------------+----------+

+---+------+------+-------------------+----------+
|eid| ename|  city|                doj|       dcd|
+---+------+------+-------------------+----------+
|  1| karan|  pune|2020-01-31 10:15:25|2020-01-29|
|  2|rajesh|  pune|2021-05-07 12:25:11|2021-05-05|
|  3|rakesh|mumbai|2023-03-02 11:45:25|2023-02-28|
+---+------+------+-------------------+----------+

+---+------+------+-------------------+----+
|eid| ename|  city|                doj|year|
+---+------+------+-------------------+----+
|  1| karan|  pune|2020-01-31 10:15:25|2020|
|  2|rajesh|  pune|2021-05-07 12:25:11|2021|
|  3|rakesh|mumbai|2023-03-02 11:45:25|2023|
+---+------+------+-------------------+----+

+---+------+------+-------------------+-----+
|eid| ename|  city|                doj|month|
+---+------+------+-------------------+-----+
|  1| karan|  pune|2020-01-31 10:15:25|    1|
|  2|rajesh|  pune|2021-05-07 12:25:11|    5|
|  3|rakesh|mumbai|2023-03-02 11:45:25|    3|
+---+------+------+-------------------+-----+

+---+------+------+-------------------+----------+
|eid| ename|  city|                doj|dayofmonth|
+---+------+------+-------------------+----------+
|  1| karan|  pune|2020-01-31 10:15:25|        31|
|  2|rajesh|  pune|2021-05-07 12:25:11|         7|
|  3|rakesh|mumbai|2023-03-02 11:45:25|         2|
+---+------+------+-------------------+----------+

+---+------+------+-------------------+----+
|eid| ename|  city|                doj|hour|
+---+------+------+-------------------+----+
|  1| karan|  pune|2020-01-31 10:15:25|  10|
|  2|rajesh|  pune|2021-05-07 12:25:11|  12|
|  3|rakesh|mumbai|2023-03-02 11:45:25|  11|
+---+------+------+-------------------+----+

+---+------+------+-------------------+------+
|eid| ename|  city|                doj|minute|
+---+------+------+-------------------+------+
|  1| karan|  pune|2020-01-31 10:15:25|    15|
|  2|rajesh|  pune|2021-05-07 12:25:11|    25|
|  3|rakesh|mumbai|2023-03-02 11:45:25|    45|
+---+------+------+-------------------+------+

+---+------+------+-------------------+------+
|eid| ename|  city|                doj|seconds|
+---+------+------+-------------------+------+
|  1| karan|  pune|2020-01-31 10:15:25|    25|
|  2|rajesh|  pune|2021-05-07 12:25:11|    11|
|  3|rakesh|mumbai|2023-03-02 11:45:25|    25|
+---+------+------+-------------------+------+

+---+------+------+-------------------+---------+
|eid| ename|  city|                doj|dayOfWeek|
+---+------+------+-------------------+---------+
|  1| karan|  pune|2020-01-31 10:15:25|        6|
|  2|rajesh|  pune|2021-05-07 12:25:11|        6|
|  3|rakesh|mumbai|2023-03-02 11:45:25|        5|
+---+------+------+-------------------+---------+

```

### UDFs

- User Defined Functions 

```python
from pyspark.sql.types import IntegerType

def make_zero(x) :  
    if x < 0:  
        return 0  
    else:  
        return x  
  
make_zero=udf(make_zero,IntegerType())  
  
df2.withColumn("Mint",make_zero(df2['Mint'])).withColumn("Maxt",make_zero(df2['Maxt'])).show()

## Output
+-----+----+----+----+
|state|Mint|Maxt|year|
+-----+----+----+----+
|   MH|   0|  40|2023|
|   KA|  18|  35|2023|
|   TN|  25|  38|2023|
|   GJ|  22|  42|2023|
|   WB|  15|  30|2023|
|   RJ|  30|  45|2023|
|   UP|  20|  37|2023|
|   MH|   0|  39|2023|
|   KA|   0|  36|2023|
|   TN|  26|  39|2023|
|   GJ|  23|  43|2023|
|   WB|  16|  31|2023|
|   RJ|  31|  46|2023|
|   UP|  21|  38|2023|
+-----+----+----+----+
```


## RDS

### Read from RDS write to LFS

```python
from pyspark.sql import SparkSession

spark=SparkSession.builder.appName("RDBMS Data Process").getOrCreate()

#read
df=(spark.read.format("JDBC")
    .option("url","jdbc:postgresql://database-1.cfqqsumomryu.eu-north-1.rds.amazonaws.com:5432/DEV")
    .option("user","puser")
    .option("password","ppassword")
    .option("driver","org.postgresql.Driver")
    .option("dbtable","cust")
    .load())
df.show()

#process

#write

#df1.write.mode('append').format("CSV").option("header","true").option("delimiter","|").save("D:/cust_new")
df1.write.mode('overwrite').format("CSV").option("header","true").option("delimiter","|").save("/home/niranjan/Documents/Sayu")
```

```python
from pyspark.sql import SparkSession

spark=SparkSession.builder.appName("RDBMS Data Process").getOrCreate()

#read
df=(spark.read.format("JDBC")
    .option("url","jdbc:postgresql://database-1.cfqqsumomryu.eu-north-1.rds.amazonaws.com:5432/DEV")
    .option("user","puser")
    .option("password","ppassword")
    .option("driver","org.postgresql.Driver")
    .option("dbtable","cust")
    .load())
df.show()

#process

df1 = df.withColumn("dataLoadDate",current_timestamp())

#write

df1.write.partitionBy("did").mode('append').format("CSV").option("header","true").option("delimiter","|").save("D:/cust_new")
(df.write.mode('append')
    .format("JSON")
    .option("header","true")
    .option("delimiter","|")
    .save("/home/niranjan/Documents/Sayu"))

```

### Read from LFS write to RDS

```python
from pyspark.sql import SparkSession

spark=SparkSession.builder.appName("RDBMS Data Process").getOrCreate()

## Remaining

```

### Read from Hive Write to S3

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("Hive Data Processing").enableHiveSupport().getOrCreate()

print("Data reading Started")

#read data from Hive 
df = spark.sql("select * from products")
df.show()

#processing
df1 = df.where(df['avlqty']>25)

df1.show()

#load
df1.write.format("CSV").option("header","true").save("s3://anildata/productsop_niranjan")

print("Data Successfully written")
print("#############Program completed################")
```

## Yarn 

- `$ yarn application -list` : Shows running applications
- `$ yarn application -status app_id` : Shows status of `app_id`
- `$ yarn -kill app_id` : Terminate the job with `app_is`
- `$ yarn logs -applicationId app_id` : Shows logs for `app_id`

### Read from S3 write to Hive

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import *

spark=SparkSession.builder.appName("Hive Data Processing").enableHiveSupport().getOrCreate()

#read data from s3 
df=spark.read.format("CSV").option("header","true").option("inferschema","true").option("delimiter",",").load("s3://anildata/emp_data/*")

df.show()

#processing
df1=df.withColumn("src",lit("S3")).withColumn("loaddate",current_date())
df1.show()

#query on hive through spark
spark.sql("create database if not exists dev")

#write data into Hive
df1.write.partitionBy("did").saveAsTable("dev.emp_niranjan")

print("******************program completed***************************")
```
# Check Logs

- Yarn Application Master
- Spark History Server

# JSON

- JavaScript Object Notation
- Semi Structured Data
- Elements are in Key Value pairs

```json
[
    {
        "eid" : 1,
        "ename" : "niranjan",
        "address" :
	        {
		        "city" : "Pune",
		        "pin" : 412208
	        }
    },
    {
        "eid" : 2,
        "ename" : "ABCD",
        "mobile" : 9090909090
    }
]
```

## Single Line JSON

```python
(spark.read.format("JSON").load("/home/niranjan/data.json").show())
```

## Multi line JSON

```python
(spark.read.format("JSON")  
    .option("multiline","true")  
    .load("/home/niranjan/Documents/json/sample_mul.json").show())
```

## Complex JSON

```json
{
    "persons": [
        {
            "name": "John",
            "age": 30,
            "cars": [
                {
                    "name": "Ford",
                    "models": [
                        "Fiesta",
                        "Focus",
                        "Mustang"
                    ]
                },
                {
                    "name": "BMW",
                    "models": [
                        "320",
                        "X3",
                        "X5"
                    ]
                }
            ]
        },
        {
            "name": "Peter",
            "age": 46,
            "cars": [
                {
                    "name": "Huyndai",
                    "models": [
                        "i10",
                        "i30"
                    ]
                },
                {
                    "name": "Mercedes",
                    "models": [
                        "E320",
                        "E63 AMG"
                    ]
                }
            ]
        }
    ]
}
```

```python
from pyspark.sql import SparkSession  
from pyspark.sql.functions import *

df = (spark.read.format("JSON")  
    .option("multiline", "true")  
    .load("/home/niranjan/Documents/json/persons.json"))  
    
df1 = (df.withColumn("persons",explode(df['persons']))  
      .withColumn("cars",explode("persons.cars"))  
      .withColumn("models",explode("cars.models"))  
      .selectExpr("persons.name","persons.age","cars.name as cname","models"))
  
df1.show()

## Output

+-----+---+--------+-------+
| name|age|   cname| models|
+-----+---+--------+-------+
| John| 30|    Ford| Fiesta|
| John| 30|    Ford|  Focus|
| John| 30|    Ford|Mustang|
| John| 30|     BMW|    320|
| John| 30|     BMW|     X3|
| John| 30|     BMW|     X5|
|Peter| 46| Huyndai|    i10|
|Peter| 46| Huyndai|    i30|
|Peter| 46|Mercedes|   E320|
|Peter| 46|Mercedes|E63 AMG|
+-----+---+--------+-------+
```

# Set Log Level

- `ALL`: The most detailed logging level. Logs all messages.
- `DEBUG`: Logs debug messages.
- `INFO`: Logs informational messages. This is the default level.
- `WARN`: Logs warning messages.
- `ERROR`: Logs error messages.
- `FATAL`: Logs fatal messages.
- `OFF`: Logs no messages.

```python
from pyspark.sql import SparkSession  
  
spark = SparkSession.builder.appName("SET LOG LEVEL").getOrCreate()  
  
spark.sparkContext.setLogLevel("DEBUG")
```

# Data Skewness

- Occurs when data is not distributed evenly across partitions. 
- This can lead to job failure, longer processing times, inefficient resource utilization and slower performance.
- [Ref](https://medium.com/@manishshrivastava26/data-skew-problem-and-different-ways-to-resolve-it-in-pyspark-bfb3a9183af)
## Solutions

- [Re-Partitioning](#re-partition-and-coalesce)
- Salting
- Adaptive Query Execution (AQE)

### Salting

- Adding one extra 

```python
from pyspark.sql.functions import *

df=spark.read.format("CSV").option("header","true").option("inferschema","true").load("D:/emp1.csv")

df.show() 
df1=df.withColumn("sf", floor(rand() * 10))
df2=df1.withColumn("city",concat("city",lit("_"),"sf")).drop("sf")
#opr can cause data skewness
df3=df2.groupBy("city").count()
df3=df3.withColumnRenamed("count","cnt")
df4=df3.withColumn("city",split(df3['city'],"_")[0])
df5=df4.groupBy("city").sum("cnt")
df5.show()
```


# RDD to DF

```sql
-- data.txt

Mumbai-192.168.1.1:Techsight|India|www.google.com  
Delhi-192.168.2.2:Techsight|India|www.microsoft.com  
Bangalore-192.168.3.3:Techsight|India|www.apple.com  
Pune-192.168.4.4:Techsight|India|www.amazon.com  
Chennai-192.168.5.5:Techsight|India|www.facebook.com  
Hyderabad-192.168.6.6:Techsight|India|www.twitter.com  
Kolkata-192.168.7.7:Techsight|India|www.linkedin.com  
Pune-192.168.8.8:Techsight|India|www.instagram.com  
Jaipur-192.168.9.9:Techsight|India|www.reddit.com  
Ahmedabad-192.168.10.10:Techsight|India|www.github.com  
Mumbai-192.168.11.11:Techsight|India|www.medium.com  
Delhi-192.168.12.12:Techsight|India|www.snapchat.com  
Bangalore-192.168.13.13:Techsight|India|www.pinterest.com  
Pune-192.168.14.14:Techsight|India|www.tumblr.com  
Chennai-192.168.15.15:Techsight|India|www.quora.com  
Hyderabad-192.168.16.16:Techsight|India|www.whatsapp.com  
Kolkata-192.168.17.17:Techsight|India|www.telegram.org  
Pune-192.168.18.18:Techsight|India|www.netflix.com  
Jaipur-192.168.19.19:Techsight|India|www.spotify.com  
Ahmedabad-192.168.20.20:Techsight|India|www.adobe.com  
Mumbai-192.168.21.21:Techsight|India|www.oracle.com  
Delhi-192.168.22.22:Techsight|India|www.ibm.com  
Bangalore-192.168.23.23:Techsight|India|www.salesforce.com  
Pune-192.168.24.24:Techsight|India|www.dropbox.com  
Chennai-192.168.25.25:Techsight|India|www.skype.com
```

```python
from pyspark.sql.types import *

rdd=spark.sparkContext.textFile("D:/data.txt")
rdd1=rdd.map(lambda x:x.replace("-","|")).map(lambda x:x.replace(":","|"))

schema=StructType([
StructField("city",StringType(),True),
StructField("ip",StringType(),True),
StructField("user",StringType(),True),
StructField("country",StringType(),True),
StructField("site",StringType(),True)
])

rdd2=rdd1.map(lambda x:x.split("|")).map(lambda x:(x[0],x[1],x[2],x[3],x[4]))
df=spark.createDataFrame(rdd2,schema)
df.show()

# Output

+---------+-------------+---------+-------+-------------------+
|     city|           ip|     user|country|               site|
+---------+-------------+---------+-------+-------------------+
|   Mumbai|  192.168.1.1|Techsight|  India|   www.google.com  |
|    Delhi|  192.168.2.2|Techsight|  India|www.microsoft.com  |
|Bangalore|  192.168.3.3|Techsight|  India|    www.apple.com  |
|     Pune|  192.168.4.4|Techsight|  India|   www.amazon.com  |
|  Chennai|  192.168.5.5|Techsight|  India| www.facebook.com  |
|Hyderabad|  192.168.6.6|Techsight|  India|  www.twitter.com  |
|  Kolkata|  192.168.7.7|Techsight|  India| www.linkedin.com  |
|     Pune|  192.168.8.8|Techsight|  India|www.instagram.com  |
|   Jaipur|  192.168.9.9|Techsight|  India|   www.reddit.com  |
|Ahmedabad|192.168.10.10|Techsight|  India|   www.github.com  |
|   Mumbai|192.168.11.11|Techsight|  India|   www.medium.com  |
|    Delhi|192.168.12.12|Techsight|  India| www.snapchat.com  |
|Bangalore|192.168.13.13|Techsight|  India|www.pinterest.com  |
|     Pune|192.168.14.14|Techsight|  India|   www.tumblr.com  |
|  Chennai|192.168.15.15|Techsight|  India|    www.quora.com  |
|Hyderabad|192.168.16.16|Techsight|  India| www.whatsapp.com  |
|  Kolkata|192.168.17.17|Techsight|  India| www.telegram.org  |
|     Pune|192.168.18.18|Techsight|  India|  www.netflix.com  |
|   Jaipur|192.168.19.19|Techsight|  India|  www.spotify.com  |
|Ahmedabad|192.168.20.20|Techsight|  India|    www.adobe.com  |
+---------+-------------+---------+-------+-------------------+
```

# CDC 

- Change Data Capture

# Historic Data

# Delta

Also knows as,
- Daily Data
- Incremental Data
- Transactional Data 
# SCD

- Slowly Changing Dimension
- Maintain history in Data Warehouse

## Types

- Type 0: No changes are made to the existing data. Historical data remains unchanged.
- Type 1 : Old data is overwritten with new data. No historical data is preserved.
- Type 2 : A new record is added for each change, preserving historical data. This typically includes effective dates or versioning.
- Type 3 : A new column is added to store the previous value.
- Type 4 : Historical data is stored in a separate table, while the current dimension table holds only the latest data.
- Type 6 : Combines Type 1, Type 2, and Type 3

```sql
-- emp_ini.csv

eid,ename,city
1,karan,Pune
2,Rajesh,Mumbai

-- emp_upd.csv

eid,ename,city
1,karan,Surat
3,Meera,Delhi
```

```python
from pyspark.sql.functions import *
from pyspark.sql.window import Window

df_ini=spark.read.format("CSV").option("header","true").option("inferschema","true").load("emp_ini.csv")
df_ini.show()

###

+---+------+------+
|eid| ename|  city|
+---+------+------+
|  1| karan|  Pune|
|  2|Rajesh|Mumbai|
+---+------+------+

###

df_ini1=df_ini.withColumn("start_date",date_sub(current_date(),1)).withColumn("end_date",lit('NA')).withColumn("current_flag",lit('Y'))
df_ini1.show()

###

+---+------+------+----------+--------+------------+
|eid| ename|  city|start_date|end_date|current_flag|
+---+------+------+----------+--------+------------+
|  1| karan|  Pune|2025-02-22|      NA|           Y|
|  2|Rajesh|Mumbai|2025-02-22|      NA|           Y|
+---+------+------+----------+--------+------------+

###


df_upd=spark.read.format("CSV").option("header","true").option("inferschema","true").load("emp_upd.csv")
df_upd.show()

###

+---+-----+-----+
|eid|ename| city|
+---+-----+-----+
|  1|karan|Surat|
|  3|Meera|Delhi|
+---+-----+-----+

###

df_upd1=df_upd.withColumn("start_date",current_date()).withColumn("end_date",lit('NA')).withColumn("current_flag",lit('Y'))
df_upd1.show()

###

+---+-----+-----+----------+--------+------------+
|eid|ename| city|start_date|end_date|current_flag|
+---+-----+-----+----------+--------+------------+
|  1|karan|Surat|2025-02-23|      NA|           Y|
|  3|Meera|Delhi|2025-02-23|      NA|           Y|
+---+-----+-----+----------+--------+------------+

###

dfu=df_ini1.union(df_upd1)
dfu.show()

#

+---+------+------+----------+--------+------------+
|eid| ename|  city|start_date|end_date|current_flag|
+---+------+------+----------+--------+------------+
|  1| karan|  Pune|2025-02-22|      NA|           Y|
|  2|Rajesh|Mumbai|2025-02-22|      NA|           Y|
|  1| karan| Surat|2025-02-23|      NA|           Y|
|  3| Meera| Delhi|2025-02-23|      NA|           Y|
+---+------+------+----------+--------+------------+

###

win_spec=Window.partitionBy("eid").orderBy(desc("start_date"))
dfu1=dfu.withColumn("rn",row_number().over(win_spec))
dfu1.show()

###

+---+------+------+----------+--------+------------+---+
|eid| ename|  city|start_date|end_date|current_flag| rn|
+---+------+------+----------+--------+------------+---+
|  1| karan| Surat|2025-02-23|      NA|           Y|  1|
|  1| karan|  Pune|2025-02-22|      NA|           Y|  2|
|  2|Rajesh|Mumbai|2025-02-22|      NA|           Y|  1|
|  3| Meera| Delhi|2025-02-23|      NA|           Y|  1|
+---+------+------+----------+--------+------------+---+

###

dfu2=dfu1.withColumn("current_flag",when(dfu1['rn']>1,lit('N')).otherwise(dfu1['current_flag']))
dfu2.show()

###

+---+------+------+----------+--------+------------+---+
|eid| ename|  city|start_date|end_date|current_flag| rn|
+---+------+------+----------+--------+------------+---+
|  1| karan| Surat|2025-02-23|      NA|           Y|  1|
|  1| karan|  Pune|2025-02-22|      NA|           N|  2|
|  2|Rajesh|Mumbai|2025-02-22|      NA|           Y|  1|
|  3| Meera| Delhi|2025-02-23|      NA|           Y|  1|
+---+------+------+----------+--------+------------+---+

###

dfu3=dfu2.withColumn("end_date",lag("start_date",1,'NA').over(win_spec)).drop("rn")
dfu3.show()

###

+---+------+------+----------+----------+------------+
|eid| ename|  city|start_date|  end_date|current_flag|
+---+------+------+----------+----------+------------+
|  1| karan| Surat|2025-02-23|      NULL|           Y|
|  1| karan|  Pune|2025-02-22|2025-02-23|           N|
|  2|Rajesh|Mumbai|2025-02-22|      NULL|           Y|
|  3| Meera| Delhi|2025-02-23|      NULL|           Y|
+---+------+------+----------+----------+------------+
```