---
layout: post
date: 2024-08-07
title: "[Instagram] System flows and High Level Design"
tags: [systemdesign, architecture, Instagram, ]
categories: [systemDesign, problems, Instagram, ]
---


## 1. Users

- Multiple users accessing the system.

### 2. Load Balancer

- Distributes incoming requests to various servers to handle large numbers of users simultaneously.

### 3. Upload Image Request Server

- Handles image upload requests from users.
- Interacts with:
	- **Master Database** for writing metadata and reading confirmation.
	- **Cache (LRU with TTL)** to store frequently accessed metadata temporarily.
	- **Amazon S3** to generate pre-signed URLs for direct uploads by clients.
	- **Kafka Producer** to publish messages to Kafka topics.

### 4. Download Image Request Server

- Handles image download requests from users.
- Interacts with:
	- **Slave Database** for reading metadata.
	- **Cache (LRU with TTL)** to retrieve frequently accessed metadata.
	- Provides pre-signed URLs or direct URLs to **Amazon CloudFront** for image delivery.

### 5. Master Database

- Handles all write operations and reads for confirmation.
- Replicates data to one or more slave databases to ensure data consistency and availability.

### 6. Slave Database(s)

- Handles read operations to offload read traffic from the master database.
- Ensures high availability and load distribution for read requests.

### 7. Data Consistency Mechanism

- **Replication Lag Monitoring**: Continuously monitor replication lag between master and slave databases to ensure timely data consistency.
- **Fallback Mechanism**: In case of significant lag, redirect read requests temporarily to the master database.
- **Eventual Consistency Handling**: Implement strategies to handle eventual consistency scenarios, where data may take some time to propagate to slave databases.

### 8. Cache (LRU with TTL)

- Stores frequently accessed metadata to improve performance.
- Implements a TTL mechanism to automatically expire and remove outdated entries.
- **Cache Invalidation**: Implement cache invalidation strategies to ensure consistency between cache and database.

### 9. Amazon S3

- Stores image files securely and scalably.
- Provides pre-signed URLs for direct uploads and access.

### 10. Amazon CloudFront

- Acts as a Content Delivery Network (CDN) to deliver images quickly to users across the globe.

### 11. Content Delivery Optimization

- **Edge Locations**: Use CloudFront edge locations to reduce latency by serving content from locations closer to the user.
- **Caching Policies**: Configure appropriate caching policies for static content like images to reduce load on the origin servers.
- **Compression**: Use Gzip or Brotli compression to reduce the size of transferred content, improving load times.
- **Optimized Media Formats**: Use efficient image formats (e.g., WebP) to reduce file sizes without compromising quality.
- **Content Versioning**: Implement versioning for static content to manage cache invalidation and ensure users get the latest content.

### 12. Scalability

- **Cloud-Based Server Scaling**: Utilize cloud services such as AWS, Azure, or Google Cloud Platform to dynamically scale the upload and download servers based on demand.
	- **Auto-Scaling**: Implement auto-scaling policies to automatically adjust the number of server instances in response to traffic load.
	- **Load Balancer**: Ensure the load balancer can handle scaling by distributing traffic evenly across the dynamically changing pool of server instances.
	- **Managed Databases**: Use managed database services that can automatically scale, such as Amazon RDS, Azure SQL Database, or Google Cloud SQL.

### 13. Newsfeed Generation Service

- **Kafka Producer**: Modify the Upload Image Request Server to act as a Kafka producer that publishes messages to a Kafka topic `image_uploads` after uploading an image and saving metadata.
- **Kafka Consumer**: Implement the Newsfeed Generation Service as a Kafka consumer that subscribes to the `image_uploads` topic.
- **Message Processing**: On receiving a message, the Newsfeed Generation Service updates the newsfeed table in the metadata database and updates the cache.
- **Kafka Cluster**: Set up a Kafka cluster with sufficient brokers to handle your expected load and ensure high availability.

![0](/assets/img/2024-08-07-[Instagram]-System-flows-and-High-Level-Design.md/0.png)

