---
layout: post
date: 2024-08-08
title: "[SystemDesign] Load Balancer vs API Gateway"
tags: [System Design, Architecture, ]
categories: [System Design, Basics, ]
---


### 1. Load Balancer

- **Purpose**: Distributes network or application traffic across multiple servers.
- **Functionality**:
	- Accepts incoming requests.
	- Routes them to one of several backend servers.
	- Uses factors such as the number of current connections, server response times, or server health for routing decisions.
- **Example**: A load balancer sits in front of website servers and evenly distributes incoming user requests to prevent any single server from becoming overloaded.

#### 2. API Gateway

- **Purpose**: Acts as a reverse proxy to route requests, simplify the API, and aggregate results from various services.
- **Functionality**:
	- Handles tasks such as request routing, API composition, rate limiting, authentication, and authorization.
	- Provides a unified interface to a set of microservices.
- **Use Case**: Commonly used in microservices architectures to make it easier for clients to consume the services.

#### 3. Key Differences

- **Focus**:
	- **Load Balancer**: Focused on distributing traffic to prevent overloading servers and ensure high availability and redundancy.
	- **API Gateway**: Focused on providing a central point for managing, securing, and routing API calls.
