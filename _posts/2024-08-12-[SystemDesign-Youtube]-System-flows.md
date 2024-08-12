---
layout: post
date: 2024-08-12
title: "[SystemDesign-Youtube] System flows"
tags: [SystemDesign, Architecture, Youtube, ]
categories: [SystemDesign, Youtube, ]
---


### **User Interaction**

- **Users** interact with the system through a **Load Balancer/API Gateway**, which routes requests to the appropriate backend services.

#### **User Services**

- **User Metadata**: Manages user-related data like likes, dislikes, and other preferences. This data is stored in a **SQL database** and replicated to read-only instances to handle high read volumes.
- **Caching**: Frequently accessed user metadata is stored in a cache with an **LRU** (Least Recently Used) strategy to improve performance.

#### **Search Services**

- **Video Search**: Handles searching for videos by title using **Elasticsearch**, which indexes video metadata for fast retrieval.

#### **Video Services**

- **Video Metadata**: Manages video-related data such as views, likes, and metadata. This data is stored in a **NoSQL database** and also replicated to read-only instances for scalability.
- **Caching**: Similar to user metadata, frequently accessed video metadata is cached.

#### **Video Upload and Processing**

- **Asynchronous Uploads**: Users upload videos, which are then placed in a **Processing Queue** for asynchronous handling.
- **Encoding**: Videos in the queue are processed by an encoding service, which converts them into various formats and resolutions.
- **Storage**: Encoded videos and thumbnails are stored in **Amazon S3** and then delivered to users via a **Content Delivery Network (CDN)** for efficient playback.

#### **Data Flow and Replication**

- **Data Replication**: Both user and video metadata are replicated to read-only databases to handle high read demand, ensuring that the system remains responsive under load.
- **Cache Invalidation**: TTL (Time-To-Live) and LRU strategies are used to manage cache validity and optimize data retrieval.

![0](/assets/img/2024-08-12-[SystemDesign-Youtube]-System-flows.md/0.png)

