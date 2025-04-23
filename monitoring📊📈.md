# [Monitoring and Observability for Development and DevOps, Coursera📊📈](https://www.coursera.org/learn/monitoring-and-observability-for-development-and-devops)

👍Pros: tbd

👎Cons: tbd

⌚Duration: tbd

💯Overall: _/10

## Intorduction🙋‍♂️📝

### Monitoring Basics

**Monitoring** is for the identification, measurement, and evaluation of applications. Monitoring results in an application that is performant and valuable. 

**Types of monitoring:**
- System monitoring (availability monitoring) measures the uptime and availability of your application, infrastructure, and network.
- Real User Monitoring (RUM) provides information about real user interactions and the historical performance of an application or service. 
- Security monitoring tracks anomalies and ensures that potential threats are stopped before they are a problem.
- Dependency Monitoring
- Integration Monitoring monitors third-party integrations to ensure they function correctly.
- Web Performance Monitoring: availability of web servers and services.
- Business Activity Monitoring (BAM) tracks key business performance metrics over time, such as sales or transaction volumes.
- Application Performance Monitoring (APM)

### Golden Signals of Monitoring🧈💰

The Golden Signals help you focus on the most critical performance indicators in your applications and systems. 

**⏱️Latency** measures the time taken for a request to be completed. Monitoring both successful and failed requests

**🚦Traffic** indicates the demand for your service, measured by user requests

**🚨Errors**: tracking all types of errors (server and client, incorrect content, identified errors)

**📶Saturation** measures resource utilization (e.g., CPU, memory)

### Monitoring Objectives

Monitoring != Evaluation

**Components of a Monitoring System**

**Metrics**: resource usage or behavior, can be low-level summaries or higher-level data

**Observation**: analyzing collected data to understand system behavior and identify patterns
Alerting Mechanisms

**Alerting**: triggers actions based on metric changes

An ideal monitoring system operates independently, is reliable, offers user-friendly dashboards, maintains historical data, allows for easy correlation of data, and supports flexible alerting capabilities.

**Types of Metrics**
- Host-based Metrics: CPU, memory, disk space, and processes to evaluate the health of individual machines.
- Application Metrics: error rates, service failures, performance, and resource usage to assess application health and efficiency.
- Network Metrics: connectivity, error rates, latency, and bandwidth utilization to ensure service availability and performance.
- Server Pool Metrics: Summarize the health of collections of servers, providing insights into the system's capacity to handle load and respond to requests.
- optional: external dependency metrics (tack interactions with external systems, including service status, success/error rates, and operational costs, to identify potential issues affecting operations).

**Metric Selection:**
- Available Resources: Limited by human resources, infrastructure, and budget.
- Application Complexity: Criticality of metrics varies based on the complexity and purpose of the application.
- Deployment Environment: Different metrics may be prioritized in production versus staging/testing environments.
- Potential Usefulness: Metrics should be evaluated for their future utility and necessity.

## Monitoring Systems and Techniques💻⚙️

**Synthetic Monitoring**

Involves **simulating user interactions** with predefined actions to assess website performance. Helps identify technical issues and slow performance. **Process of Synthetic Monitoring**: The monitoring system selects checkpoints to perform tests, checks responses, and reports findings back to the monitoring system. If errors are detected, alerts are sent out, allowing for quick problem resolution.

### Application Monitoring

Types:
- Performance Monitoring
- Availability Monitoring
- User Experience Monitoring
- Error Monitoring
- Log Monitoring

**Monitoring tools**

| tool | for what |  functions | example |
| --- | --- | --- | --- |
|Prometheus|Monitoring and alerting toolkit|collecting and storing metrics as time series data, designed for reliability and scalability|monitoring applications and infrastructure, especially in cloud-native environments|
|Grafana|Data visualization and analytics platform|Works with various data sources (including Prometheus) to create dashboards and visualizations, does not collect data itself|visualizing metrics and logs from different sources in a unified dashboard|
|Kibana|Data visualization tool for Elasticsearch|visualizes log data stored in Elasticsearch, provides powerful search and filtering capabilities|analyzing and visualizing log data, especially in conjunction with the ELK stack (Elasticsearch, Logstash, Kibana)|
|Splunk|Data analysis and monitoring platform|collects, indexes, and analyzes machine-generated data, provides powerful search, monitoring, and reporting capabilities|large-scale data analysis, security monitoring, and operational intelligence|

**Summary:**
- Prometheus: Focuses on metrics collection and monitoring.
- Grafana: Visualizes data from various sources, including Prometheus.
- Kibana: Visualizes log data from Elasticsearch.
- Splunk: Comprehensive data analysis and monitoring platform for various data types.


## Logging📁📝

**Distributed Logging** involves collecting and storing log data from multiple sources across different nodes or servers, enabling centralized monitoring and analysis.

**Distributed Tracing** profiles and monitors applications, particularly those with microservices, by tracking requests as they move through various services. Important concepts in distributed tracing include:
- trace: a collection of spans representing a single logical request or workflow
- span: a single operation within a trace
- trace ID
- parent/child relation: one span calls another span as part of its operation, the calling span becomes the parent, and the called span becomes the child,
- context propagation: how information about a trace is passed between different services and systems
- instrumentation

Application logs:
- event
- error
- access
- performance
- debugging

Analytical dimensions that give an idea of how long the retention period should be: criticality, security, maturity, frequency, cost-effectiveness, and discovery and resolution.

## Observability⚙️📈

Observability: ability to infer the internal state of a system by examining its external outputs.

**Observability != Monitoring**

Monitoring: collecting data over time to identify issues. A reactive approach with a limited view.

Observability: providing real-time insights and context-rich information, allowing for proactive issue resolution.

### Three Pillars of Observability 🏛️

**🏛️Logs** are records of events generated by infrastructure and platform software, providing detailed information about individual transactions. Easy to generate, human-readable, and allow for retrospective analysis of support incidents.

**🏛️Metrics** are numerical measurements that indicate the health of system components, offering a high-level view of performance through aggregated data. They are lightweight, intuitive for alerting, and effective for tracking trends over time.

**🏛️Traces** record the workflows of requests through a distributed system, helping to identify bottlenecks and latency issues. Identify the problematic component or step.

### Cloud native observability and sampling

Cloud native observability is the practice of monitoring and understanding the behavior of cloud-native applications running in dynamic and distributed environments. The pillars of cloud enterprise observability are automation, context, and intelligent action.

**Sampling in logging** is the practice of collecting only a subset of log events for analysis or storage. Instead of logging every single event or piece of data, a subset is selected randomly or by some other criteria for recording.
