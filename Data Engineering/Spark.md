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