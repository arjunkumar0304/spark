# spark

# Hadoop
 
 * Hadoop is an open-source framework used to store and process big data efficiently across many computers instead of one.


# Why Hadoop?
Earlier, a single computer wasn’t enough to handle large data.
Hadoop solved this by using distributed computing — breaking data and tasks into smaller parts and running them on clusters (many computers working together).


| Component                                     | Description                                                                                                                       |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **1. HDFS (Hadoop Distributed File System)**  | Used to **store** large files across many machines. Splits data into **blocks (e.g., 128MB)** and stores them on different nodes. |
| **2. YARN (Yet Another Resource Negotiator)** | The **resource manager** of Hadoop. It allocates CPU & memory to different jobs running on the cluster.                           |
| **3. MapReduce**                              | The **data processing engine**. It processes data in two steps — **Map** (split task) and **Reduce** (combine results).           |


# 2. Spark Introduction

* 2.1 Overview of Apache Spark and Its Advantages

Apache Spark is an open-source, distributed computing system designed for fast data processing.


Spark provides an in-memory computing framework, making it 100x faster than traditional Hadoop MapReduce in some workloads.


| Feature                 | Hadoop MapReduce         | Apache Spark                       |
| ----------------------- | ------------------------ | ---------------------------------- |
| **Processing**          | Batch only               | Batch + Streaming                  |
| **Speed**               | Slower (disk-based)      | Faster (in-memory)                 |
| **Ease of Programming** | Complex (Java-based)     | Simple APIs (Python, Scala)        |
| **Fault Tolerance**     | Data replication         | RDD lineage (recomputes lost data) |
| **Use Cases**           | Log analysis, batch jobs | Real-time analytics, ML, streaming |


# 3. Spark Architecture Overview
3.1 Understanding the Key Components of the Spark Architecture

Driver:

Plans and controls the whole job

Converts code → tasks for executors

SparkContext:

Establishes connection to cluster manager

Cluster Manager:

Example: YARN, Standalone, Mesos, Kubernetes

Decides how many executors to give


Executors:

Perform the actual computation

Store data in memory

Tasks:

Part of job executed on executor cores


#  4 spark components


# Driver

First, the Driver starts the Spark application.

Driver runs the main() function and creates SparkContext/SparkSession.

It converts your code into tasks, builds the DAG, and schedules tasks.

It coordinates the entire job.

This is the first component to start.

# Cluster Manager

After the Driver starts, it contacts the Cluster Manager.

Cluster Manager's job is to allocate resources (CPU, memory).

It provides the executors needed to run the application.


# Executors

Once resources are allocated, Executors are launched on worker nodes.

Executors run tasks in parallel.

They also store data in memory or disk.

After completing tasks, they return results to the Driver.

Executors keep running until the application ends.

# 4.1 core concept in spark

# RDD (Resilient Distributed Dataset)

RDD is the basic data structure in Spark.

It is immutable (cannot be changed once created).

It is distributed across multiple nodes in the cluster.

Supports parallel processing.


# Spark Core

Spark Core is the foundation of the entire Spark ecosystem.

It contains:

RDDs

Task scheduling

Memory management

Fault tolerance

Job execution engine

All other components (SQL, Streaming, MLlib, GraphX) are built on top of Spark Core.

*  Spark Core = the engine that runs everything in Spark.

# Spark SQL

Module used for structured and semi-structured data.

Works with DataFrames and Datasets.

Allows SQL queries using:

spark.sql()

DataFrame API

Optimized by Catalyst Optimizer.

* Spark SQL = handles structured data using DataFrames + SQL.

# Spark Streaming

Used for near real-time data processing.

Processes data in micro-batches.

Can read from:

Kafka

Files

New version is Structured Streaming (more advanced).

* Spark Streaming = real-time data processing engine.

# MLlib (Machine Learning Library)

Spark’s built-in machine learning library.

Supports:

Classification

Regression

Clustering

Feature engineering

Model evaluation

* MLlib = scalable ML algorithms running on distributed data.

# GraphX

Spark’s graph processing API.

Used for:

PageRank

Connected components

Graph analytics

Uses RDDs internally.

 * GraphX = library for graph-based computations.


# 5.1 RDD, DataFrame, Dataset – Difference & Conversion

# RDD (Resilient Distributed Dataset)

* Lowest-level abstraction in Spark.

* Works with unstructured data.

* You write code using Java/Python/Scala functions.

* No schema, no automatic optimization.

* Slowest among the three.

* Best when you need full low-level control (custom transformations).

#  DataFrame

* Structured data (rows & columns like a table).

* Has schema.

* Built on top of Spark SQL engine.

* Uses Catalyst Optimizer → much faster than RDD.

* Operations are simple, SQL-like & optimized.

* Best for ETL, SQL queries, analytics.

# Dataset (Scala & Java only)

* (Not available in Python)

* Combination of RDD (type safety) + DataFrame (performance).

* Strongly typed.

* Also uses Catalyst Optimizer.

* Best for type-safe, high-performance pipeline



# Converting Between RDD, DataFrame & Dataset

1️⃣ RDD → DataFrame
Scala
val df = rdd.toDF()

Python
df = rdd.toDF(schema)

2️⃣ RDD → Dataset (Scala only)
case class Person(name: String, age: Int)
val ds = rdd.map(x => Person(x._1, x._2)).toDS()

3️⃣ DataFrame → RDD
val rdd = df.rdd


Python:

rdd = df.rdd

4️⃣ DataFrame → Dataset (Scala only)
case class Person(name: String, age: Int)
val ds = df.as[Person]

5️⃣ Dataset → DataFrame
val df = ds.toDF()

6️⃣ Dataset → RDD
val rdd = ds.rdd



# transformation

A transformation in Spark is an operation that creates a new RDD/DataFrame from an existing one.

Transformations are lazy — they do not execute immediately.
Spark waits until an action (like count(), show(), collect()) is called.

# Narrow Transformation 

A Narrow Transformation is when data does NOT move between partitions.

👉 Each partition uses only its own data
👉 No shuffle, no network, no data transfer
👉 Very fast and efficient

# Examples

map()

filter()

flatMap()

mapPartitions()

union() (if partitions align)

# Wide Transformations

Wide transformations are operations where data from one partition may need to move to multiple partitions.

* Involves data shuffling
* Slower, network heavy, requires sorting/grouping

Examples

reduceByKey

groupBy

groupByKey

join

distinct

orderBy / sortBy

#  Understanding Shuffling in Spark
# What is Shuffling?

Shuffling is the process of redistributing data across partitions in Spark.
It happens when a task needs data from a different partition.


# Examples of Narrow and Wide Transformations

# Narrow Transformations (NO shuffle)

Definition
Output partition depends only on one input partition. No data movement, faster.

| Operation         | Why it is Narrow?                        |
| ----------------- | ---------------------------------------- |
| `map()`           | Each element processed independently     |
| `filter()`        | Only checks conditions on same partition |
| `flatMap()`       | Same as map                              |
| `mapPartitions()` | Stays inside the partition               |

# Wide Transformations (Shuffle happens)
Definition

Output partition depends on multiple input partitions. Requires data movement (shuffle)

| Operation       | Why it is Wide?                         |
| --------------- | --------------------------------------- |
| `reduceByKey()` | Needs all values of same key            |
| `groupByKey()`  | Groups keys across partitions           |
| `join()`        | Matches keys from two datasets          |
| `distinct()`    | Removes duplicates → needs global check |
| `sortByKey()`   | Needs all keys to sort properly         |


# Basic practices (RDD, Dataframe)
<img width="1231" height="710" alt="Screenshot 2025-11-21 175456" src="https://github.com/user-attachments/assets/12b9fb0e-5e7c-45bc-be2f-d372611a787a" />



<img width="1048" height="420" alt="Screenshot 2025-11-21 175525" src="https://github.com/user-attachments/assets/ac90e2ab-f269-4585-8dd8-5fd79a0d1722" />



<img width="1264" height="723" alt="Screenshot 2025-11-21 175544" src="https://github.com/user-attachments/assets/85bb3bc2-4409-4deb-ad23-92ed1ad2402e" />
