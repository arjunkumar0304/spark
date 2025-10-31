# spark

# Hadoop
 
 * Hadoop is an open-source framework used to store and process big data efficiently across many computers instead of one.

 * It allows you to handle huge volumes of data (GBs, TBs, PBs) by splitting the data into chunks and processing them in parallel across multiple machines (called nodes).

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

It was developed at UC Berkeley’s AMPLab in 2009 and became an Apache project in 2014.

Spark provides an in-memory computing framework, making it 100x faster than traditional Hadoop MapReduce in some workloads.

# Key Advantages:

* Speed: Performs in-memory computation, reducing disk I/O.

* Ease of Use: APIs available in Python, Scala, Java, and R.

* Versatility: Supports batch processing, streaming, machine learning, and graph processing.

* Integration: Works with HDFS, Hive, Cassandra, HBase, and Amazon S3.

| Feature                 | Hadoop MapReduce         | Apache Spark                       |
| ----------------------- | ------------------------ | ---------------------------------- |
| **Processing**          | Batch only               | Batch + Streaming                  |
| **Speed**               | Slower (disk-based)      | Faster (in-memory)                 |
| **Ease of Programming** | Complex (Java-based)     | Simple APIs (Python, Scala)        |
| **Fault Tolerance**     | Data replication         | RDD lineage (recomputes lost data) |
| **Use Cases**           | Log analysis, batch jobs | Real-time analytics, ML, streaming |


# 3. Spark Architecture Overview
3.1 Understanding the Key Components of the Spark Architecture

Driver Program:

* The main program that runs the SparkContext.

* Responsible for converting user code into tasks.

* Schedules and coordinates tasks across executors.

Cluster Manager:

* Allocates resources for Spark applications.

* Examples: YARN, Mesos, Kubernetes, or Standalone cluster manager.

Executors:

* Worker processes that run on nodes to execute tasks.

* Store data and perform computations.

Tasks:

* Smallest unit of work sent to executors.

RDD (Resilient Distributed Dataset):

* Core data structure of Spark.

Immutable and distributed collection of data.

3.2 Interaction Between Components During Execution

* Step 1 – Job Submission:

User submits the Spark application to the Driver program.

* Step 2 – Resource Allocation:

The Cluster Manager assigns resources (executors) to the Driver.

* Step 3 – Task Distribution:

The Driver divides the job into stages and tasks, sending them to Executors.

* Step 4 – Execution:

Executors perform computations and store intermediate results in memory.

* Step 5 – Result Collection:

The Driver collects results from Executors and returns the output to user
