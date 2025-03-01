RDDS are low level data structure, DF are high level abstractions that store data in column like structure
RDD provides functional programming API, DF provide SQL Like API 
RDDS are slower than DF due to the lack of optimizer, DF is faster due to the catalyst optimizer
RDDs process unstructured data, DF process structured data
RDDs do not support schema, DF supports schema 
#

- Spark is an in memory data processing framework, MR is disk based data processing framework
- Spark is faster than MR as MR processes data on the disk 
- MR is complex as the user has to write all the code, Spark provides functional and SQL Like APIs to process data
- MR runs on Hadoop clusters where as spark can run on clusters as well as standalone
# 

- Transformations are operations which return a RDD when processed
- Examples are map, reduce, filter 
- Types, narrow transformations, wide transformations 

# 

re partition and coalesce are both optimization techniques used in spark
re-partitions shuffles the whole data where as coalesce tries to avoid a full shuffle
re-partition creates new partitions where as coalesce utilizes existing partitions 

# 

Data Skewness occurs when the data is not distributed evenly access the partitions, this may lead to job failure and inefficient resource utilization and slower performance. 
Can be solved with Salting and Re partitioning 

# 

