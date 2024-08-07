---
layout: post
date: 2024-08-07
title: "[Instagram] System flows and High Level Design"
tags: [systemdesign, architecture, Instagram, ]
categories: [systemDesign, problems, Instagram, ]
---


## 1. Traffic Management


#### 1.1 Load Balancer

1. **Function:** Routes traffic to appropriate servers.
2. **Read Requests:** Directed to read servers.
3. **Write Requests:** Directed to write servers.

### 2. Read and Write Operations


#### 2.1 Read Servers

1. **Cache Check:**
	- Attempt to read metadata from cache.
	- If metadata is present, return the response.
	- If metadata is not present, fetch from metadata storage, update cache, and return the response.

#### 2.2 Write Servers

1. Handle all write operations to the master database.

### 3. Database Architecture


#### 3.1 Master Database

1. Handles both read and write operations for metadata.
2. Replicates data to slave databases.

#### 3.2 Slave Databases

1. Handle read-only operations to offload the master database.

### 4. Content Storage and Delivery


#### 4.1 Amazon S3

1. **Function:** Stores all photo and video content.
2. **Content URLs:** Provided to clients.
3. **Content Delivery:** Redirect clients to the CDN for fast content delivery.

### 5. News Feed Generation


#### 5.1 Scheduled Service

1. Periodically updates users' news feeds.
2. Updates are stored in both the database and cache.

### 6. Search Functionality


#### 6.1 Logstash

1. Frequently updates Elasticsearch with photo metadata from the database.

#### 6.2 Elasticsearch

1. Handles search queries for photo and video titles.

### 7. Follow/Unfollow Logic


#### 7.1 Database Schema

1. **UserFollower Table:** Manages follow relationships.

#### 7.2 API Endpoints

1. Endpoints for follow and unfollow actions.

### 8. User Notifications


#### 8.1 Notification Service

1. Handles and sends real-time notifications.

#### 8.2 Real-time Updates

1. Implement WebSockets or push notification services.

### 9. Rate Limiting


#### 9.1 API Gateway

1. Implements rate limiting policies.
2. Controls the number of requests per user/IP.

### 10. Backup and Disaster Recovery


#### 10.1 Regular Backups

1. Schedule regular backups for databases and critical data.

#### 10.2 Disaster Recovery Procedures

1. Implement and regularly test recovery procedures.

### 11. Security Enhancements


#### 11.1 Authentication and Authorization

1. Use OAuth 2.0 for secure authentication.

#### 11.2 Data Encryption

1. Encrypt data both at rest and in transit.

### 12. Monitoring and Alerts


#### 12.1 Performance Monitoring

1. Use tools like AWS CloudWatch or Datadog to monitor system performance.

#### 12.2 Alert Configuration

1. Set up alerts for critical issues such as high latency, cache misses, and replication lag.

[link_preview](https://whimsical.com/instagram-high-level-design-GrSuRQdbwqtwwBhtLa7337)

