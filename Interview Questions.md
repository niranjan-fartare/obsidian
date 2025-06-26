# Primary Key vs Unique Key vs Composite Key vs Foreign Key

- **Primary Key**: Uniquely identifies records, only one per table, no NULLs.
- **Unique Key**: Ensures uniqueness, multiple allowed, can have NULLs.
- **Composite Key**: Combination of two or more columns as a primary key.
- **Foreign Key**: References a primary key in another table to establish relationships.
# SET Operators

Set operators are used to combine the results of two or more SELECT statements. They are, 

- **Union:** Combines the results of two or more SELECT statements, no duplicates
- **Union All:** Combines the results of two or more SELECT statements, including duplicates
- **Intersect:** Returns only the rows that are present in both result sets.
- **Except:** Returns rows from the first result set that are not present in the second result set.
# Why do we create View in SQL? 

A view is a virtual table that is based on the result of a SELECT query. Reasons to create view are,
- **Simplicity**: Makes complicated queries easier to use.
- **Data Abstraction**: Hides the details of data.
- **Security**: Protects sensitive information from users.
- **Re-usability**: Lets you use the same query again.
- **Data Aggregation**: Combines data from different places.
# Stored Procedure

A stored procedure in SQL is a collection of SQL statements stored in the database. The purpose of the stored procedure is to perform a sequence of operations on a database, such as inserting, updating, or deleting data.

The benefits of Stored Procedure:
- **Code re-usability:** Once a stored procedure is created, it can be called as many times as needed, eliminating redundancy in SQL code.
- **Enhanced performance:** Stored procedures often execute faster because they are precompiled and stored on the database server.
- **Security:** Stored procedures can improve data security and control over sensitive data access by granting users permission to execute a stored procedure without direct access to tables.
# Joins

A join is used to combine records from one or more tables based on related columns.

- **INNER JOIN**: Returns only the rows that have matching values in both tables.
- **LEFT JOIN**: Returns all rows from the left table and the matched rows from the right table. If there is no match, NULL values are returned for columns from the right table.
- **RIGHT JOIN:** Returns all rows from the right table and the matched rows from the left table. If there is no match, NULL values are returned for columns from the left table.
- **FULL JOIN**: Returns all rows when there is a match in either left or right table records. If there is no match, NULL values are returned for non-matching rows from both tables.
- **CROSS JOIN**: Returns the Cartesian product of the two tables, meaning every row from the first table is combined with every row from the second table.

# Apache Spark and PySpark Fundamentals

## 1. What is Apache Spark?

- Apache Spark is a fast, open source, in-memory data processing engine designed for big data processing.
- It is a powerful tool that can process huge amounts of data quickly across many computers.
- Unlike older systems like Hadoop that write to disk after each step, Spark keeps data in memory when possible, making it much faster.
- It supports multiple programming languages like Java, Scala, Python, R
- Spark offers various libraries for SQL, machine learning, graph processing, and stream processing.
## 2. What is PySpark and how does it differ from core Spark?

- Apache Spark is a fast, open source, in-memory data processing engine designed for big data processing.
- PySpark is the Python API for Apache Spark. It allows users to write Spark applications using the Python language.
- PySpark allows us to use the processing power pr Spark while using python syntax and libraries.

## 3. Explain Spark architecture in detail

Spark uses a master-worker architecture with these key components:
### Driver Program

- It is the central control unit
- It manages the overall workflow of a Spark job, communicating with the cluster manager, transforming user code into Spark Jobs, and scheduling tasks to be executed on worker nodes.
### Cluster Manager

- Allocates resources across the applications.
- Acts as a messenger between the Driver Program and Worker Nodes.
### Worker Node

- Worker node is also called as slave node.
- It's main task is to work on the task assigned by the Driver program process.

When you run a Spark job:

1. The driver breaks your code into tasks
2. The cluster manager assigns resources
3. Executors on worker nodes run the tasks
4. Results go back to your driver program

This distributed architecture allows Spark to process data in parallel across many machines.

## 4. What happens when we submit a Spark job?

When a Spark job is submitted, a chain of events happens:

1. Spark Submit sends the application code and configuration to the cluster
2. A driver process starts on a node and creates a SparkContext
3. SparkContext connects to the cluster manager like YARN, Kubernetes, etc.
4. The cluster manager allocates resources and launches executors on worker nodes
5. The application code is sent to the executors
6. Once the executors have completed their tasks the results are sent back to the Driver Program or are written to Storage.

This whole process happens automatically when a Spark job is submitted.

## 5. What is the Spark submit command?

The `spark-submit` command is how Spark Applications are executed on a cluster. It's like the "launch button" for Spark jobs. A basic example looks like:

```
spark-submit \
  --class org.example.MyApp \
  --master yarn \
  --deploy-mode cluster \
  --executor-memory 2g \
  --num-executors 10 \
  my-application.jar \
  application_args
```

Key parts include:

- The application file (JAR or Python script)
- The master URL (yarn, k8s://host, spark://host, local)
- Resource configurations (memory, cores, etc.)
- Application-specific arguments

For PySpark, you'd submit a Python script instead of a JAR file.

## 6. What is an RDD and how does it differ from a DataFrame?

**RDD (Resilient Distributed Dataset)** is Spark's fundamental data structure - a distributed collection of elements that can be processed in parallel.

**DataFrame** is a higher-level abstraction built on top of RDDs.

Key differences:

- **Structure**: RDDs are collections of objects with no schema, while DataFrames are organized into named columns (like database tables)
- **Optimization**: DataFrames use Catalyst optimizer and can be much faster due to optimized execution plans
- **API**: DataFrames have SQL-like operations (select, filter, groupBy), while RDDs use functional programming (map, reduce)
- **Ease of use**: DataFrames are more user-friendly and intuitive for most data tasks
- **Performance**: DataFrames are generally faster because Spark can optimize the execution

Think of RDDs as low-level building blocks, while DataFrames are higher-level, optimized structures for most data processing needs.

## 7. What is lazy evaluation in Spark?

Lazy evaluation means Spark doesn't process your data immediately when you define transformations (like map, filter, join). Instead, it:

1. Just remembers the operations you want to perform (builds a plan)
2. Only executes when you call an "action" (like count(), collect(), save())

Benefits include:

- **Optimization**: Spark can look at your entire processing chain and optimize it before execution
- **Efficiency**: Unnecessary operations can be skipped
- **Performance**: Multiple operations can be combined into fewer stages

Think of it like writing a shopping list (transformations) but only going to the store once (action) instead of making separate trips for each item.

## 8. What is fault tolerance in Spark?

Fault tolerance is Spark's ability to recover from failures during computation. If a machine crashes or a task fails, Spark can continue working without losing data.

How it works:

1. RDDs track their "lineage" (the sequence of transformations used to create them)
2. If a partition of data is lost, Spark can rebuild just that partition using the lineage information
3. Spark automatically retries failed tasks and can work around failed nodes

This makes Spark reliable for long-running jobs on large clusters where failures are common.

Think of it like having the recipe (lineage) to remake just the dish that fell on the floor, rather than remaking the entire meal.

## 9. What is schema enforcement?

Schema enforcement means Spark ensures that data conforms to a predefined structure (schema). It's like having strict rules about what data can look like.

Key aspects:

- Spark checks that incoming data matches the expected data types and column names
- It rejects records that don't match the schema (or handles them according to your settings)
- It prevents "garbage in, garbage out" problems by ensuring data quality

Benefits:

- Prevents data corruption
- Makes code more reliable
- Reduces unexpected errors during processing
- Improves query performance through optimizations

Example: If your schema expects an "age" column with integer values, Spark will validate that the data meets these requirements.

## 10. What is the Catalyst optimizer?

The Catalyst optimizer is Spark's query optimization engine that improves the performance of DataFrame and SQL operations. Think of it as Spark's "brain" for making your queries run faster.

How it works:

1. Converts your code into a logical plan
2. Applies optimization rules to improve the plan
3. Converts the optimized logical plan into a physical plan
4. Generates efficient code for execution

Key optimizations include:

- Predicate pushdown (filtering data early)
- Column pruning (reading only needed columns)
- Join reordering (finding the most efficient join sequence)
- Constant folding (pre-computing fixed expressions)

The best part is that this happens automatically - you write simple code, and Catalyst makes it run efficiently.

## 11. What is the difference between deployment modes in Spark?

Spark has two main deployment modes:

**Client Mode**:

- The driver process runs on the client machine (your computer)
- Good for interactive applications and debugging
- Output/logs appear on your local machine
- Your client machine needs to stay connected during the entire job

**Cluster Mode**:

- The driver process runs on one of the worker nodes in the cluster
- Better for production jobs
- More reliable since the job continues even if your client disconnects
- Logs are on the cluster, not your local machine

Choose client mode during development and testing, and cluster mode for production jobs that need to run reliably.

## 12. What is the difference between a Python shell and a Spark job?

**Python Shell** (like IPython or regular python interpreter):

- Interactive environment for running Python code line by line
- Single-process, runs only on your local machine
- Great for exploration, small tasks, and learning
- No distributed processing capabilities on its own

**Spark Job**:

- A complete application submitted to a Spark cluster
- Runs across multiple machines in a distributed way
- Handles large-scale data processing
- Requires proper setup with spark-submit or similar tools

The Python shell is like cooking in your home kitchen, while a Spark job is like running a large commercial kitchen with many chefs working simultaneously.

## 13. What is memory management in Spark?

Memory management in Spark is how the system allocates and uses memory for processing data. It's crucial because Spark's performance depends heavily on efficient memory use.

Spark divides memory into:

**Execution Memory**:

- Used for computation in joins, aggregations, shuffles
- Dynamically allocated based on need

**Storage Memory**:

- Used for caching data and intermediate results
- Can be adjusted with persist() and cache() operations

**User Memory**:

- Used for your application's data structures

**Reserved Memory**:

- System overhead and internal objects

Key memory management features:

- **Spill to disk**: When memory is insufficient, Spark can write data to disk
- **Dynamic allocation**: Executors can be added or removed as needed
- **Tungsten**: An optimization that stores data in memory more efficiently
- **Memory fractions**: Configurable settings that control how memory is divided

Good memory management means configuring these settings based on your workload to avoid out-of-memory errors and maximize performance.

## Spark Operations & Optimizations

1. What is repartition and coalesce? What are their differences?
2. What is cache and persist in Spark?
3. What is data skewness and how do you handle it?
4. What is salting and what is a salting factor?
5. What is partitioning in Spark?
6. What is bucketing in Spark?
7. How do you choose between bucketing and partitioning?
8. Which optimization techniques have you used in your projects?
9. How do you handle bad records in Spark?
10. What does the explode function do?

## SQL & Data Processing

1. What is the difference between WHERE and HAVING clauses?
2. What is dense_rank and how does it differ from rank and row_number?
3. What is a subquery and CTE (Common Table Expression)?
4. How would you write a query to find the 4th highest salary?
5. How would you write a query to delete duplicate records?
6. What is the difference between primary key and foreign key?
7. How do you identify records present in the first table but not in the second without using MINUS?
8. What are materialized views?
9. What is the difference between OLAP and OLTP systems?
10. What is a fact table and what is a dimension table?

## File Formats & Storage

1. What are different file formats used in data engineering?
2. What is the difference between Parquet and CSV file formats?
3. What is the difference between ORC and Parquet formats?
4. Which file formats have you used in your projects?
5. How do you read semi-structured data?
6. What is Hadoop and what kind of data is stored in it?
7. What is HBase and why would you use it?

## AWS & Cloud Tools

1. What is AWS EMR and why would you use it?
2. What AWS tools have you used in your projects? Explain in detail.
3. What is AWS Glue crawler?
4. Can you create a bucket inside another bucket in S3?
5. What is time travel in Databricks?

## Data Warehouse & Data Modeling

1. What is data modeling?
2. Explain data warehouse and data lake concepts
3. What are fact and dimension tables? Can you provide examples?
4. What is delta table?

## ETL & Data Pipelines

1. Which ETL tools have you used?
2. How do you handle daily/transactional/delta data?
3. What is SCD (Slowly Changing Dimension) and how do you handle incremental data?
4. How do you handle semi-structured data?
5. How do you decide which column is good for partitioning?
6. What are important components of Airflow?
7. What is the difference between a DAG and a Lineage Graph?

## Hive & Database Concepts

1. What is the difference between Hive internal and external tables?
2. What is data validation and how have you implemented it?

## Monitoring & Troubleshooting

1. How do you monitor your pipeline?
2. Where do you check logs when debugging?
3. How do you delete logs in Airflow?
4. If 90% of your data is loaded to a pipeline but 10% is not loaded, what can you do?
5. If your data has issues, what would be your next steps?
6. How do you handle git conflicts?

## Python Data Structures

1. What is the difference between a list and a tuple?
2. How do you remove duplicates in a list?
3. What is the difference between a dictionary and a tuple?
4. Which Python libraries have you used in your projects?
5. Write a program to find prime numbers from 1 to 100

## Project Experience Questions

1. What challenges did you face in your project?
2. What technical challenges did you face in AWS Glue?
3. What errors did you overcome?
4. What is the size of data you process daily (approximate)?
5. When is data available in your target system?
6. Who accesses the data you process?
7. What types of data do you handle in your projects?
8. Which transformations have you applied in your projects?
9. Have you worked with BI tools?
10. Which automation framework have you used in your projects?
11. What was the size of your team and who did you report to?
12. What was your daily routine?
13. Have you worked with real-time data handling?
14. What are API calls and how have you used them?
15. Which Linux commands did you use in your projects?
16. How do you copy multiple files from one cluster to another?
17. What types of reports did you generate?
18. What kind of results were you producing?
