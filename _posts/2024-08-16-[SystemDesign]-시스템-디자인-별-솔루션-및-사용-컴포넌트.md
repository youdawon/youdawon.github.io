---
layout: post
date: 2024-08-16
title: "[SystemDesign] 시스템 디자인 별 솔루션 및 사용 컴포넌트"
tags: [System Design, ]
categories: [System Design, Basics, ]
---


# System Design Use Cases and Solutions 


### Unified API access

- **Use Cases/Problems**: Centralizes client requests.
- **System Design Questions**: Design an API gateway for microservices.
- **⭐ Component**: API Gateway
- **What it solves**: Single entry point, manages authentication and routing.
- **Caveats/Issues**: Can become a bottleneck, adds latency.
- **Mitigations**:
	- Use multiple gateways with load balancing.
	- Implement rate limiting and caching.
	- Use circuit breakers and retries.
- **Examples of Tools**: Kong, Apigee, AWS API Gateway

### High traffic websites

- **Use Cases/Problems**: Ensures uptime and balances load.
- **System Design Questions**: Design a scalable web application.
- **⭐ Component**: Load Balancer across multiple redundant workers
- **What it solves**: Distributes traffic across workers, improves reliability and availability.
- **Caveats/Issues**: Single point of failure, adds complexity.
- **Mitigations**:
	- Use multiple load balancers in different regions.
	- Implement health checks.
	- Use DNS-based load balancing.
- **Examples of Tools**: Nginx, HAProxy, AWS ELB

### Financial transactions

- **Use Cases/Problems**: Requires ACID compliance.
- **System Design Questions**: Design a financial transaction system.
- **⭐ Component**: SQL Database
- **What it solves**: Strong ACID properties, structured data, complex queries.
- **Caveats/Issues**: Limited scalability, schema management.
- **Mitigations**:
	- Implement sharding.
	- Use read replicas.
	- Employ clustering and partitioning.
- **Examples of Tools**: MySQL, PostgreSQL, MS SQL Server

### Large-scale data

- **Use Cases/Problems**: Supports horizontal scaling.
- **System Design Questions**: Design a large-scale user profile store.
- **⭐ Component**: NoSQL Database
- **What it solves**: Flexible schema, horizontal scalability, high performance.
- **Caveats/Issues**: Eventual consistency, limited transaction support.
- **Mitigations**:
	- Use consistency settings (e.g., quorum reads/writes).
	- Design for idempotent operations.
	- Implement conflict resolution strategies.
- **Examples of Tools**: MongoDB, Cassandra, DynamoDB

### High availability

- **Use Cases/Problems**: Ensures data is replicated and available.
- **System Design Questions**: Design a data replication strategy.
- **⭐ Component**: Data Replication
- **What it solves**: Ensures data durability, to ensure system availability.
- **Caveats/Issues**: Increases costs, consistency issues.
- **Mitigations**:
	- Use asynchronous replication.
	- Implement conflict resolution.
	- Use multi-master replication.
- **Examples of Tools**: AWS RDS standby (synchronous), AWS RDS Read Replicas (asynchronous), MongoDB Replica Set (asynchronous)

### High read load

- **Use Cases/Problems**: Reduces latency for frequent reads.
- **System Design Questions**: Design a high-performance caching layer.
- **⭐ Component**: Cache
- **What it solves**: Reduces latency, decreases load on databases.
- **Caveats/Issues**: Cache consistency issues, potential for stale data.
- **Mitigations**:
	- Implement cache invalidation strategies.
	- Use Time-to-Live (TTL) settings.
	- Employ write-through or write-back caching.
- **Examples of Tools**: Redis, Memcached

### Real-time analytics

- **Use Cases/Problems**: Requires fast data access.
- **System Design Questions**: Design a real-time analytics system.
- **⭐ Component**: In-Memory Database
- **What it solves**: Extremely fast data retrieval, reduces latency.
- **Caveats/Issues**: Volatile storage, high memory cost.
- **Mitigations**:
	- Enable persistence options.
	- Use hybrid storage models (in-memory + disk).
	- Implement data backup strategies.
- **Examples of Tools**: Redis, Memcached

### Event streaming

- **Use Cases/Problems**: Manages high-throughput data streams.
- **System Design Questions**: Design a real-time event streaming platform.
- **⭐ Component**: Message Broker
- **What it solves**: Facilitates message exchange, supports multiple patterns.
- **Caveats/Issues**: Bottleneck potential, delivery guarantees.
- **Mitigations**:
	- Use scalable brokers with partitions.
	- Implement backpressure handling.
	- Monitor message broker performance.
- **Examples of Tools**: Apache Kafka, RabbitMQ, ActiveMQ

### Event-driven systems

- **Use Cases/Problems**: Manages asynchronous events.
- **System Design Questions**: Design an event-driven architecture.
- **⭐ Component**: Distributed Queue
- **What it solves**: Manages asynchronous communication, decouples components.
- **Caveats/Issues**: Message ordering and delivery guarantees.
- **Mitigations**:
	- Use message brokers with strong ordering guarantees.
	- Implement idempotent message processing.
	- Use message deduplication techniques.
- **Examples of Tools**: Apache Kafka, RabbitMQ, AWS SQS

### Large applications

- **Use Cases/Problems**: Enhances modularity and scalability.
- **System Design Questions**: Design a scalable microservices architecture.
- **⭐ Component**: Microservices
- **What it solves**: Improves modularity, independent deployment.
- **Caveats/Issues**: Increased communication complexity.
- **Mitigations**:
	- Use service meshes.
	- Implement standardized APIs.
	- Use centralized logging and monitoring.
- **Examples of Tools**: Docker, Kubernetes, Istio

### Microservices

- **Use Cases/Problems**: Enables service discovery.
- **System Design Questions**: Design a service discovery mechanism.
- **⭐ Component**: Service Registry
- **What it solves**: Tracks services and their instances.
- **Caveats/Issues**: High availability required, consistency issues.
- **Mitigations**:
	- Use distributed service registries.
	- Implement regular health checks.
	- Use consensus algorithms for consistency.
- **Examples of Tools**: Consul, Eureka, Zookeeper

### Content-heavy sites

- **Use Cases/Problems**: Improves load times for users.
- **System Design Questions**: Design a content delivery system.
- **⭐ Component**: CDN (Content Delivery Network)
- **What it solves**: Reduces latency, improves load times.
- **Caveats/Issues**: Cache invalidation complexity, cost.
- **Mitigations**:
	- Implement cache purging strategies.
	- Use regional CDNs.
	- Monitor CDN performance and hit rates.
- **Examples of Tools**: Cloudflare, Akamai, AWS CloudFront

### Business intelligence

- **Use Cases/Problems**: Centralizes analytics data.
- **System Design Questions**: Design a data warehouse for analytics.
- **⭐ Component**: Data Warehouse
- **What it solves**: Centralizes data, supports complex queries.
- **Caveats/Issues**: High storage and maintenance costs.
- **Mitigations**:
	- Use data compression and partitioning.
	- Implement data lifecycle management.
	- Use cloud-based, scalable data warehouses.
- **Examples of Tools**: Amazon Redshift, Snowflake, Google BigQuery

### E-commerce sites

- **Use Cases/Problems**: Provides fast product search.
- **System Design Questions**: Design a product search system.
- **⭐ Component**: Search Engine
- **What it solves**: Enables fast search over large datasets.
- **Caveats/Issues**: Indexing and maintenance required.
- **Mitigations**:
	- Implement efficient indexing strategies.
	- Use distributed search architectures.
	- Optimize search queries and relevance.
- **Examples of Tools**: Elasticsearch, Solr, Algolia

### Media storage

- **Use Cases/Problems**: Handles large files like images and videos.
- **System Design Questions**: Design a scalable file storage system.
- **⭐ Component**: File Storage
- **What it solves**: Scales with data growth, handles unstructured data.
- **Caveats/Issues**: Backup and redundancy required, retrieval latency.
- **Mitigations**:
	- Use distributed file systems.
	- Implement multi-region replication.
	- Use lifecycle policies for data management.
- **Examples of Tools**: AWS S3, Google Cloud Storage, HDFS

### Data warehousing

- **Use Cases/Problems**: Prepares data for analysis.
- **System Design Questions**: Design an ETL pipeline for a data warehouse.
- **⭐ Component**: ETL Pipeline
- **What it solves**: Facilitates data integration and analysis.
- **Caveats/Issues**: Complex to build and maintain.
- **Mitigations**:
	- Use managed ETL services.
	- Implement monitoring and error handling.
	- Use data validation and transformation tools.
- **Examples of Tools**: Apache Nifi, AWS Glue, Talend

### System reliability

- **Use Cases/Problems**: Monitors uptime and performance.
- **System Design Questions**: Design a system monitoring solution.
- **⭐ Component**: Monitoring System
- **What it solves**: Tracks system health, enables alerting.
- **Caveats/Issues**: High overhead, potential noise.
- **Mitigations**:
	- Use threshold tuning and anomaly detection.
	- Implement efficient data collection.
	- Use centralized monitoring dashboards.
- **Examples of Tools**: Prometheus, Grafana, Datadog

### Debugging

- **Use Cases/Problems**: Captures logs for issue diagnosis.
- **System Design Questions**: Design a centralized logging system.
- **⭐ Component**: Logging System
- **What it solves**: Aids in auditing and troubleshooting.
- **Caveats/Issues**: Large data volumes, storage and querying.
- **Mitigations**:
	- Use log rotation and retention policies.
	- Implement centralized logging.
	- Optimize log storage and indexing.
- **Examples of Tools**: ELK Stack, Splunk, Fluentd

### Secure applications

- **Use Cases/Problems**: Manages user identity and access.
- **System Design Questions**: Design a secure authentication system.
- **⭐ Component**: Authentication Service
- **What it solves**: Enhances security, manages user authentication.
- **Caveats/Issues**: Single point of failure, security measures needed.
- **Mitigations**:
	- Use multi-factor authentication.
	- Implement redundancy and failover.
	- Use secure token storage and management.
- **Examples of Tools**: OAuth, Okta, Auth0

### Containerized apps

- **Use Cases/Problems**: Automates container management.
- **System Design Questions**: Design a container orchestration system.
- **⭐ Component**: Orchestration Tool
- **What it solves**: Automates deployment and management.
- **Caveats/Issues**: Adds complexity, learning curve.
- **Mitigations**:
	- Use managed orchestration services.
	- Implement robust CI/CD pipelines.
	- Use monitoring and scaling tools.
- **Examples of Tools**: Kubernetes, Docker Swarm, Mesos

### Dynamic applications

- **Use Cases/Problems**: Centralizes config changes.
- **System Design Questions**: Design a configuration management system.
- **⭐ Component**: Configuration Service
- **What it solves**: Centralizes configuration management.
- **Caveats/Issues**: Single point of failure, secure access needed.
- **Mitigations**:
	- Use distributed configuration stores.
	- Implement encryption for sensitive data.
	- Use versioning and rollback mechanisms.
- **Examples of Tools**: Consul, etcd, Spring Cloud Config

### Real-time dashboards

- **Use Cases/Problems**: Aggregates live data feeds.
- **System Design Questions**: Design a real-time analytics system.
- **⭐ Component**: Real-Time Data Aggregation
- **What it solves**: Enables real-time analytics and monitoring.
- **Caveats/Issues**: High complexity, data velocity issues.
- **Mitigations**:
	- Use stream processing frameworks.
	- Implement windowing and aggregation techniques.
	- Monitor and scale processing infrastructure.
- **Examples of Tools**: Apache Flink, Apache Storm, AWS Kinesis

### Microservices

- **Use Cases/Problems**: Tracks requests across services.
- **System Design Questions**: Design a distributed tracing system.
- **⭐ Component**: Distributed Tracing
- **What it solves**: Aids in debugging and performance monitoring.
- **Caveats/Issues**: High overhead, integration required.
- **Mitigations**:
	- Use sampling to reduce overhead.
	- Implement efficient trace storage.
	- Use correlation IDs for request tracking.
- **Examples of Tools**: Jaeger, Zipkin, OpenTracing

### Fault tolerance

- **Use Cases/Problems**: Prevents system overloads.
- **System Design Questions**: Design a fault-tolerant microservices system.
- **⭐ Component**: Circuit Breaker
- **What it solves**: Protects services from cascading failures.
- **Caveats/Issues**: Adds complexity, tuning needed.
- **Mitigations**:
	- Use monitoring tools to detect failures.
	- Implement fallback strategies.
	- Use retries and exponential backoff.
- **Examples of Tools**: Hystrix, Resilience4j, Istio

### API management

- **Use Cases/Problems**: Protects against request floods.
- **System Design Questions**: Design an API rate limiting system.
- **⭐ Component**: Rate Limiter
- **What it solves**: Controls request rate, prevents abuse.
- **Caveats/Issues**: Can impact user experience.
- **Mitigations**:
	- Use dynamic rate limiting.
	- Implement user-based quotas.
	- Use monitoring to adjust limits.
- **Examples of Tools**: Kong, Envoy, Nginx

### Periodic tasks

- **Use Cases/Problems**: Automates recurring jobs.
- **System Design Questions**: Design a job scheduling system.
- **⭐ Component**: Scheduler
- **What it solves**: Manages background jobs and tasks.
- **Caveats/Issues**: Requires monitoring, can become bottleneck.
- **Mitigations**:
	- Use distributed schedulers.
	- Implement job prioritization.
	- Use monitoring and retry mechanisms.
- **Examples of Tools**: Apache Airflow, Celery, Kubernetes CronJobs

### Microservices

- **Use Cases/Problems**: Handles inter-service communication.
- **System Design Questions**: Design a service mesh for microservices.
- **⭐ Component**: Service Mesh
- **What it solves**: Manages microservices communication.
- **Caveats/Issues**: Adds operational complexity.
- **Mitigations**:
	- Use managed service meshes.
	- Implement automation tools.
	- Use monitoring and observability tools.
- **Examples of Tools**: Istio, Linkerd, Consul Connect

### Disaster recovery

- **Use Cases/Problems**: Ensures data is safe and recoverable.
- **System Design Questions**: Design a backup and recovery system.
- **⭐ Component**: Data Backup and Recovery
- **What it solves**: Ensures data durability, protects against data loss.
- **Caveats/Issues**: Resource-intensive, regular testing needed.
- **Mitigations**:
	- Use automated backup solutions.
	- Implement multi-region storage.
	- Regularly test backup and recovery processes.
- **Examples of Tools**: AWS Backup, Google Cloud Backup, Veeam

### Social networks

- **Use Cases/Problems**: Models complex relationships.
- **System Design Questions**: Design a social network graph database.
- **⭐ Component**: Graph Database
- **What it solves**: Efficiently handles graph-based data and relationships.
- **Caveats/Issues**: Steep learning curve, non-graph query inefficiency.
- **Mitigations**:
	- Use graph-specific optimizations.
	- Implement hybrid models for different data types.
	- Use indexing and caching for performance.
- **Examples of Tools**: Neo4j, Amazon Neptune, OrientDB

### Big data analytics

- **Use Cases/Problems**: Stores and processes vast data.
- **System Design Questions**: Design a big data analytics platform.
- **⭐ Component**: Data Lake
- **What it solves**: Supports diverse data types and analytics.
- **Caveats/Issues**: Governance required, risk of becoming data swamp.
- **Mitigations**:
	- Use metadata management.
	- Implement data cataloging.
	- Use data lifecycle policies.
- **Examples of Tools**: AWS Lake Formation, Azure Data Lake, Hadoop

### Event-driven architectures

- **Use Cases/Problems**: Processes data streams in real-time.
- **System Design Questions**: Design a real-time data streaming system.
- **⭐ Component**: Data Streaming Platform
- **What it solves**: Facilitates real-time data processing.
- **Caveats/Issues**: High operational complexity.
- **Mitigations**:
	- Use managed streaming services.
	- Implement scaling strategies.
	- Monitor and optimize processing.
- **Examples of Tools**: Apache Kafka, AWS Kinesis, Google Pub/Sub

출처 : [https://github.com/bhavul/System-Design-Cheatsheet](https://github.com/bhavul/System-Design-Cheatsheet)

