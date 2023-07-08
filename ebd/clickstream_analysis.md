## Background

    Clickstream analysis commonly refers to analyzing the events (click data) that are collected as users browse a website. Such an analysis is typically done to extract insights into visitor behavior on your website in order to inform subsequent data-driven decisions.

## Problem

    Suppose you are an online retailer selling bike parts. Users visit your website to browse bike parts, read reviews, and hopefully make a purchase. Whenever users view a page or click a link, this gets logged by your website application (logs are plain old Apache web server or Nginx logs).

    As an online retailer, you’d like to gain a better understanding of your users and streamline your sales and marketing efforts. 

    Storing and analyzing this sheer volume of data requires a robust distributed system and with capability to process unstructured/semi-structured data. 
    Design a hadoop based system which will help you ingest, process, and analyze data logged by your web servers.


## Assumptions

    1. Commonly used web log format is Common Log format and its extension is Combined log format (CLF)
    2. Log data arrives at a very high velocity
    3. A very active website can generate several gigabytes of web server logs per day.
    4. Log data is semistructured; it may have user agent strings that need to be parsed, or additional parameters that might be added to and later removed from log records, such as parameters added for testing.


## Solution Design

    https://learning.oreilly.com/library/view/hadoop-application-architectures/9781491910313/ch08.html#idp14131872

### Design overview
    <img src="..click-stream-design.png">]


### Storage

    HDFS as storage
        - text file format to store raw data logs
        - columnar (parquet) format to store processed information which will be queried / analysed. We will compress the processed data set with Snappy due to its improved CPU efficiency.

    Directory Structure to store data
        raw data: /etl/BI/casualcyclist/clicks/rawlogs/year=2014/month=10/day=10
        processed data: /data/bikeshop/clickstream/year=2014/month=10/day=10


### Ingestion

    Flume is better suited to ingest Apache Webserver logs into hadoop
    Sqoop for data into hadoop from secondary sources such as CRM (RDBMS based), ODS (and out of hadoop)

    Since Flume is specifically made for Hadoop while Kafka is general purpose, we will select Flume

        Ingestion workflow:

            Client Tier                                 ---->       Collector Tier                                  ---->   Hadoop
            [Webserver: Flume Client Agents 1,2,3]                  [Edge node: Flume Collector Agents 1,2,3]               [HDFS]    


        Client Tier
        - Flume source type: Spooling Directory Source
        - Flume channel: File channel (for reliability; else for performance we can chose memory)
        - Flume sink: EdgeNode
        - Sink data format: Avro

        Collector Tier
        - Flume source type: Avro
        - Flume channel: File channel 
        - Flume terminal sink: HDFS 
        - Sink terminal data format: Text
        - Sink partitioned by: Timestamp (to minimize disk I/O during processing)
        (hdfs.fileType=DataStream and hdfs.writeFormat=Text)

       


### Processing (Raw data treatment)

    Processing here may refer to, but is not limited to, deduplication of data, filtering out “bad” clicks, converting the clicks into columnar format, sessionization (the process of grouping clicks made by a single user in a single visit by associating a session ID representing that visit to each click made as a part of the visit), and aggregation.

    Spark for processing

    Pre-processong:
    - Sanitising data: remove incomplete and invalid log lines
    - Deduplication : Because if any of Flume agents crash, data will be reset (promise of atleast once delivery)
        hive, pig, mapreduce, spark
    - Transform / filter data : select useful logs, perform sessionization

    Sessionization:
        group clicks made by a single user in a single visit by associating a session ID
        - Strategy: Consider all sessions terminated at the end of the day. So use 24 hours window.
        - run the sessionization algorithm once, every day 


### Analyzing Process

    Refers to running various analytical queries on the processed data sets to find answers and insights as per requirements

    Impala for analyzing the processed data. By connecting a BI tool to Impala, we will be able to perform interactive queries on the processed data.


### Orchestration

    Refers to automating the arrangement and coordination of various processes that perform ingestion, processing, and analyzing.

    Oozie to orchestrate multiple actions into a single workflow.

        pre-processing --> Sessionisation 


### Learnings

    1) To make efficient use of Hadoop’s processing capabilities, average size of each partition should be at least a few multiples of the HDFS block size 
    2) Avro is a serialization format that can be used when we’re transferring data from one process or another or when storing data on a filesystem, say HDFS.
    3) If data is ingested from RDBMS table, it is usually clean and do not require cleansing/sanitize.

