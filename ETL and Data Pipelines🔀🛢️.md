# [ETL and Data Pipelines course](https://www.coursera.org/learn/etl-and-data-pipelines-shell-airflow-kafka)🔀🛢️

## ETL and ELT🔀🛢️

### ETL

**ETL**: an automated methodology for acquiring and preparing data for analytics environments like data warehouses or data marts. The process involves:
- extracting data from multiple sources which can be static or dynamic, and can include database querying, web scraping, and APIs
- transforming (wrangling) it into a suitable format, and includes cleaning, filtering, merging data sources, feature engineering, and formatting
- loading it into a new environment, such as databases or data warehouses

**Use Cases for ETL:** ETL processes are used to digitize analog data, capture transaction history for analysis, and prepare data for machine learning models.
They help in making large amounts of information accessible and usable for various applications.

### ELT

**ELT** (Extract, Load, Transform): a modern approach to data pipeline engineering. ELT involves:
- extracting data from various sources
- loading it AS IS directly into a destination environment
- transforming it on demand, which allows for more dynamic and flexible data manipulation after loading

**Use Cases for ELT:** high-performance computing and big data scenarios, such as real-time analytics and managing distributed data sources. It minimizes data movement, which can be a bottleneck, making it ideal for building data products with flexibility.

The rise of cloud computing has facilitated the growth of ELT, as cloud resources can handle large volumes of data efficiently and scale on demand.
ELT provides a clean separation between data movement and processing, reducing the risk of information loss and allowing for various transformation methods.

### Comparing ETL and ELT

|Differences|ETL|ELT|
|---|---|---|
|Transformation Order|transforms data before it reaches its destination|ELT transforms data in the destination environment|
|Flexibility|fixed process for specific functions|flexibility for self-service analytics|
|Handling Big Data|handles structured data with on-premises resources, which can limit scalability|can manage both structured and unstructured data, leveraging cloud scalability|
|Time-to-Insight|requires modifications that can delay insights|allows end users to access and analyze raw data more quickly|

The shift towards ELT is driven by the need to make raw data accessible to a broader user base. In summary, while ETL remains relevant, the trend is moving towards ELT due to its flexibility and ability to handle big data challenges.

### Data Transformation

**Data Transformation** involves:
- formatting data to suit applications, including data typing (casting to types like integer, float, etc.)
- structuring (converting formats like JSON or CSV to database tables)
- anonymizing and encrypting
- cleaning (removing duplicates, filling missing values)
- normalizing (ensuring comparability)
- merging disparate data sources

**Schema Approaches:**
- **Schema-on-write** is the traditional ETL approach, requiring data to conform to a defined schema before loading, enhancing stability but limiting versatility.
- **Schema-on-read** is used in modern ELT processes, applies schema after reading raw data, allowing for multiple views and greater data access without extensive preprocessing.

Information can be **lost** during transformation, often due to lossy data compression, permanent filtering, aggregation, and edge computing devices. While ETL processes may lose recoverable information, ELT retains all original data, preserving its content for future use.

### Data Loading

Data Loading Strategies:
- Full Loading: Used to initialize a data warehouse or load initial history; no existing content is present.
- Incremental Loading: Appends only changed data since the last load, useful for maintaining transaction history.
  - Stream Loading: Continuous updates triggered by events or thresholds, ideal for real-time data.
  - Batch Loading: Periodic updates scheduled at specific intervals, such as daily or weekly.
 
## Data pipelines🔀🛢️

A data pipeline is a system that moves data from one place or form to another, often involving optional transformation stages.
Data flows through the pipeline in the form of packets, which can vary in size from single records to large collections.

Performance:
- Latency: the total time it takes for a single packet to pass through the pipeline, limited by the slowest process.
- Throughput: how much data can be processed per unit of time, with larger packets potentially increasing productivity.

### Data Pipeline Processes

The main stages include:
- data extraction from sources
- ingestion into the pipeline
- optional transformation
- final loading into a destination
  
Additional processes involve scheduling jobs, monitoring workflows, and maintaining the pipeline for optimal performance.

**Monitoring:** key aspects to monitor include
- latency (time for data flow)
- throughput demand (volume of data)
- errors and failures (caused by network issues)
- resource utilization (cost implications)

A **logging** system is essential for alerting administrators about failures and ensuring data integrity.

### Batch and streaming data pipelines

**📦Batch data pipelines:** 
- process large sets of data as a single unit, typically on a fixed schedule or triggered by data size
- suitable for scenarios where accuracy is critical, but data recency is not, emphasizing accuracy over speed

**Use cases:** periodic data backups and transaction history loading, processing of customer orders and billing, data modeling on slowly varying data, mid- to long-range sales forecasting and weather forecasting, analysis of historical data and diagnostic medical image processing.

**▶️Streaming data pipelines:**
- handle data packets individually in real-time, allowing for immediate processing of events as they occur
- ideal for applications requiring low latency, when the most current data is needed

**Use cases:** watching movies and listening to music or podcasts,
social media feeds and sentiment analysis, fraud detection, user behavior analysis, and targeted advertising, stock market trading, 
real-time product pricing, and recommender systems

**λ Lambda architecture:** 
- combines batch and streaming methods, utilizing a batch layer for historical data and a speed layer for real-time data
- balances the need for accuracy and speed but brings complexity in design

Micro-batch processing can be used to simulate real-time data streaming, and Lambda architecture can be used in cases where access to earlier data is required, but speed is also important.

## Streaming pipelines with Kafka

**Event Stream Processing (ESP):** The main components of an ESP are Event broker, Event storage, Analytic, and Query Engine.
A stream processor receives, transforms, and forwards the processed stream 


**Core components of Kafka are:**
- brokers, the dedicated servers to receive, store, process, and distribute events
- topics, the containers or databases of events
- partitions divide topics into different brokers
- replications duplicate partitions into different brokers
- producers, Kafka client applications that publish events into topics
- consumers, Kafka client applications that subscribe to topics and read events from them

The Kafka-topics CLI manages topics. 

The Kafka-console-producer CLI manages producers and finally.

The Kafka-console-consumer manages consumers.

Kafka increase fault-tolerance and throughput by topic partitions and replications.






