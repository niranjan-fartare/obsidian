- In Memory Processing
- 10x Faster than Map Reduce
- Process structured, semi structured and unstructured data
- Programming Module
- Computation Framework
- 

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

- Narrow Transformation : Perform operations on specific partitions
- Wide Transformation : Perform operations on multiple partitions

![[Screenshot 2025-02-02 at 11-49-31 Learning Spark Second Edition - LearningSpark2.0.pdf.png]]

## Lazy Evaluation



# Re-partition and Coalesce