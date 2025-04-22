# [Monitoring and Observability for Development and DevOps, Coursera📊📈](https://www.coursera.org/learn/monitoring-and-observability-for-development-and-devops)

👍Pros: tbd

👎Cons: tbd

⌚Duration: tbd

💯Overall: _/10

## Intorduction

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

## Monitoring Systems and Techniques

**Synthetic Monitoring**

Involves **simulating user interactions** with predefined actions to assess website performance. Helps identify technical issues and slow performance. **Process of Synthetic Monitoring**: The monitoring system selects checkpoints to perform tests, checks responses, and reports findings back to the monitoring system. If errors are detected, alerts are sent out, allowing for quick problem resolution.

Synthetic Monitoring provides quick problem resolution and alerts teams to issues before users are affected.
Synthetic monitoring is essential for maintaining productivity, revenue, and reputation, especially for companies relying on online services.

### Application Monitoring

Performance Monitoring
Availability Monitoring
User Experience Monitoring
Error Monitoring
Log Monitoring



Prometheus vs Grafana vs Kibana vs Splunk, I don't understand the difference

Coach
Let's break down the differences between Prometheus, Grafana, Kibana, and Splunk:

| tool | for what |  functions | example |
| --- | --- | --- | --- |
|Prometheus|Monitoring and alerting toolkit|collecting and storing metrics as time series data, designed for reliability and scalability|monitoring applications and infrastructure, especially in cloud-native environments|
|Grafana|Data visualization and analytics platform|Works with various data sources (including Prometheus) to create dashboards and visualizations, does not collect data itself|visualizing metrics and logs from different sources in a unified dashboard|
|Kibana|Data visualization tool for Elasticsearch|visualizes log data stored in Elasticsearch, provides powerful search and filtering capabilities|analyzing and visualizing log data, especially in conjunction with the ELK stack (Elasticsearch, Logstash, Kibana)|
|Splunk|Data analysis and monitoring platform|collects, indexes, and analyzes machine-generated data, provides powerful search, monitoring, and reporting capabilities|large-scale data analysis, security monitoring, and operational intelligence|

Summary:
- Prometheus: Focuses on metrics collection and monitoring.
- Grafana: Visualizes data from various sources, including Prometheus.
- Kibana: Visualizes log data from Elasticsearch.
- Splunk: Comprehensive data analysis and monitoring platform for various data types.

