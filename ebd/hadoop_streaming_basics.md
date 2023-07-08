# Basics of Stream processing

    https://www.netguru.com/blog/spark-streaming#:~:text=Apache%20Spark%20Structured%20Streaming%20is,with%20virtually%20no%20code%20changes
    https://www.upsolver.com/blog/apache-spark-and-spark-structured-streaming-compared 

    Stream processing is known as the continuous processing of endless streams of data.

    Traditional stream processing stacks use a record-at-a-time processing model. In this model, each node continuously receives one record at a time, processes it, and then forwards the generated data to the next node. It can achieve very low milliseconds latency.
     - However, this model isn’t very efficient at recovering from node failures and nodes that are lagging. It can either recover from a failure very fast with a lot of extra failover resources, or use minimal extra resources but recover slowly

## Spark Streaming

    Apache Spark Streaming – an extension of the core Spark API – is a scalable and fault-tolerant system that natively supports batch and streaming workloads.
    Streaming data is broken into a group of RDDs called DStreams. DStreams, represented as sequences of RDD blocks, are suitable for low-level RDD-based batch workloads.

## Structured Streaming

    It is a micro-batch stream processing approach where the streaming computation is modeled as a continuous series of small, map/reduce-style batch processing jobs (hence, “micro-batches”), on small chunks of the stream data.
        - Streaming data is divided into small chunks (of Dataset or dataframe)
        - Streaming computation = continuous series of small batch processing jobs that all work on small chunks of data

    Spark Structured streaming is part of the Spark 2.0 release built on the Spark SQL engine. Spark SQL engine takes care of running the data stream “incrementally and continuously and updating the final result as streaming data continues to arrive.”

    Spark Structured Streaming engine divides the data from the input stream into, say, one-second micro-batches. Each batch is processed in the Spark cluster in a distributed manner with small deterministic tasks that generate the output in micro-batches. 

    Advantages over the traditional, continuous-operator model:
        1. Spark’s smart scheduling system can quickly and efficiently recover from failures by rescheduling one or more copies of the task on the other executors.
        2. The deterministic nature of the tasks ensures the output remains the same no matter the number of times it’s executed.   
            Micro-batching provides strong consistency because batch determinations record the end and beginning of each batch.   

    Disadvantages: 
        But this efficient fault tolerance comes at a cost: latency. The micro-batch model can’t achieve millisecond-level latencies but half a second to a few seconds

### Structured Streaming - Offset 

    Let's assume we’re reading data from a single partition Kafka source. Each event is considered to have an ever-increasing offset. 
    - Structured streaming asks source (Kafka partition) for current offset and compares it with last processed offset. This informs Spark about the next batch of data to be processed.
    - Once processed, source is informed that data has been processed by committing a given offset. This guarantees all data with an offset less than or equal to the committed offset has been processed, and that subsequent requests will only include offsets greater than the committed offset. This process constantly repeats, ensuring the acquisition of streaming data. 
        getOffset()
        getBatch(0, 6)
        commit(6)
    - To recover from eventual failure, offsets are often checkpointed to external storage.

### How Spark Structured Streaming works ?

    Spark's architecture includes master (Cluster Manager) and workers (executors). A master allocates resources (memory, CPU, etc.) required for execution and sends application codes to executors to execute.

    Executors
        Since Data is distributed, Spark will instruct the executors to ingest our data in a distributed way into a partition in the worker’s memory.
            Executor = Tasks + Memory (partitioned and each partition stores a partition of input data)
            Executor = [Task1, Task2] + [Partition1, Partition2, Partition3...]

    Tasks
        Executors create tasks to read the data – a task is a unit of execution. A task maps to a single core on the worker and works on a single partition of the data.
        - An executor with two cores can have two or more tasks working on two or more partitions in parallel.
        - Each executor has access to the node’s memory and will assign a memory partition to the task.

    Task failure recovery
        1. A task is a unit of execution that processes the data in a single partition. What happens when there’s task failure due to possible out-of-memory errors, network errors, or data quality problems such as parsing or syntax errors, etc.?
        2. The application is the driver and data doesn't have to come to the driver – it can be driven remotely. The driver connects to a master and gets  a session. Driver contains DAGSs, logs, metadata, and scheduling state. If the driver fails, the stage of computation, what the computation consists of, and where the data can be found are deleted at the same time. How do we mitigate this?

        To mitigate task failure, Spark can 
            1) recompute using DAG or 
            2) Use cache() or persist() function to save a copy of the data on another node of the cluster which can be used to retrieve

        To mitigate Driver failure, 
            If run on cluster mode, then driver is hosted on a node inside the cluster. This adds the extra functionality of automatically restarting the driver when failure of any kind is detected.
            To avoid losing the intermediate state in the case of a driver crash, Spark also offers the option of checkpointing which saves a snapshot of the intermediate state to disk.

## Difference between Spark Streaming and Structured streaming

    https://www.linkedin.com/pulse/spark-streaming-vs-structured-nikkie-thomas 

    Spark streaming works on micro batch. The stream pipeline is registered with some operations and the Spark polls the source after every batch duration (defined in the application) and then a batch is created of the received data. i.e. each incoming record belongs to a batch of DStream.

    Structured Streaming works on the same architecture of polling the data after some duration, based on your trigger interval but it is more inclined towards real streaming.
        In Structured streaming, there is no concept of a batch. The received data in a trigger is appended to the continuously flowing data stream. Each row of the data stream is processed and the result is updated into the unbounded result table. How you want your result (updated, new result only or all the results) depends on the mode of your operations (Complete, Update, Append).
        Data Stream = Unbounded table
        New data in data stream = new rows appended to Unbounded table

    1. Spark Streaming utilizes the DStream API, while Structured Streaming employs the DataFrame and Dataset APIs.
    2. Spark Streaming is designed for continuous transformation, while Structured Streaming allows for SQL-like queries on streaming data.
    3. Structured Streaming provides end-to-end guarantees, which Spark Streaming lacks. 
    4. Spark Streaming's Dstreams are less efficient than Structured Streaming’s DataFrames
        - The time taken to partition data into RDD chunks can negatively impact analytical outcomes, leading to higher latency and slower data processing through the ETL pipeline.
        - In contrast, Spark Structured Streaming, built on top of the Apache Spark’s DStreams, eliminates the need for direct RDD block access. Instead, it relies on DataFrames, which offer lower latency, higher throughput, and guaranteed message delivery.
    5. RDD API does not optimize the data transformation chain, resulting in increased latency and time delays, particularly when processing faulty and slow data. In contrast, DataFrame API
    6. Spark streaming does not proces with event time but only with ingestion time. Structured Streaming provides event time processing mechanism.
        Hence Structured Streaming provides late data handling mechanism
