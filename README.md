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


# spark components


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

# core concept in spark

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
