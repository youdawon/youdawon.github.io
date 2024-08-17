---
layout: post
date: 2024-08-12
title: "[SystemDesign-Youtube] System flows"
tags: [System Design, Architecture, Youtube, ]
categories: [System Design, Problems, Youtube, ]
---


### **User Interaction**

- **Users** access the platform through a **Load Balancer/API Gateway**, which routes their requests to the appropriate backend services.

#### **User Services**

- Manages user-related data (likes, dislikes). This data is cached using **LFU** (Least Frequently Used) to keep frequently accessed data readily available, and is stored in a **SQL database** with read-only replicas to handle high read volumes.

#### **Search Services**

- Handles video search functionality using **Elasticsearch**, which indexes video metadata to allow for fast and efficient searches by video title.

#### **Video Services**

- Manages video metadata (e.g., view counts, likes/dislikes). This data is cached using **LRU** (Least Recently Used) to ensure that the most recently accessed data remains in the cache, and is stored in a **NoSQL database** with replication for scalability.

#### **Video Upload and Processing**

- Users upload videos asynchronously, which are placed in a **Processing Queue**.
- The videos are then encoded into various formats by the encoding service, stored in **Amazon S3**, and distributed to users via a **Content Delivery Network (CDN)**.

#### **Data Flow**

- **Replication**: User and video metadata are replicated to read-only instances to handle read operations efficiently.
- **Caching**: Metadata is cached to improve performance, with **LFU** used for user data and **LRU** for video data.

![0](/assets/img/2024-08-12-[SystemDesign-Youtube]-System-flows.md/0.png)

