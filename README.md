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
