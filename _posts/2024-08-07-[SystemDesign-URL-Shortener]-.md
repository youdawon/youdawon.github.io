---
layout: post
date: 2024-08-07
title: "[SystemDesign-URL Shortener] "
tags: [SystemDesign, UrlShortener, Architecture, ]
categories: [SystemDesign, Problems, UrlShortener, ]
---


---

1. **Load Balancer**:
	- Routes the client's request to one of the server nodes.
2. **Server-side Validation**:
	- **Format Validation**: Checks if the URL format is correct.
	- **Length Validation**: Checks if the URL length exceeds the maximum limit.
	- **Validation Failure**: Returns a 404 status code and message if the URL is not valid.
	- **Format or Length Validation Failure**: Returns a 400 status code and message if the format is incorrect or the length is too long.
3. **Duplicate URL Check**:
	- Searches the database for an existing `original_url`.
	- If a duplicate exists, returns a 200 status code with the existing short URL and a message that the URL already exists.
	- Optimizes search speed by adding an index on the `original_url` field.
4. **Unique Sequence Generation**:
	- **Zookeeper Configuration**: Zookeeper assigns a unique sequence range to each node.
		- For example, Node 1: 1 to 1,000,000, Node 2: 1,000,001 to 2,000,000.
	- Each node generates a unique sequence within the assigned range.
	- Encodes the sequence to Base62 to create a short URL.
5. **Data Storage**:
	- Stores the new URL mapping in the database.
	- Returns the short URL as a response.
6. **URL Access Request Handling**:
	- Checks the cache for data.
	- If not found in the cache, queries the database and stores the data in the cache.
	- Uses LRU (Least Recently Used) algorithm to remove the least used data when the cache is full.
	- Sets TTL (Time-to-Live) to automatically expire data after a certain period.
7. **Cleanup Task**:
	- Regularly removes expired URLs from the database and cache.
	- Performs deletion based on the expiration date.
8. **Expired URL Handling**:
	- Returns a 410 status code and message when accessing an expired URL, then removes it from the database and cache.
9. **DDOS Protection and Request Limiting**:
	- Each client uses a unique `api_dev_key`.
	- The load balancer limits request rates based on the `api_dev_key` to prevent DDOS attacks.

#### Final Design Flow


#### URL Shortening Request Handling

1. **Load Balancer**:
	- Routes the client's request to one of the server nodes.
2. **Validation**:
	- **Format Validation**: Checks if the URL format is correct.
	- **Length Validation**: Checks if the URL length exceeds the maximum limit.
	- **Validation Failure**: Returns a 404 status code and message if the URL is not valid.
	- **Format or Length Validation Failure**: Returns a 400 status code and message if the format is incorrect or the length is too long.
	- **Accessibility Check (Optional)**: Implements asynchronous checks to see if the URL is reachable.
3. **Duplicate URL Check**:
	- Searches the database for an existing `original_url`.
	- If a duplicate exists, returns a 200 status code with the existing short URL and a message that the URL already exists.
	- Adds an index on the `original_url` field to optimize search speed.
4. **Unique Sequence Generation**:
	- **Zookeeper Configuration**: Assigns a unique sequence range to each node.
		- Node 1: 1-1,000,000, Node 2: 1,000,001-2,000,000.
	- Encodes the sequence to Base62 to create a short URL.
5. **Data Storage**:
	- Stores the new URL mapping in the database.
	- Returns the short URL as a response.
6. **Database Sharding**:
	- Hash-based partitioning using `original_url`.

#### URL Access Request Handling

1. **Cache Check**:
	- Checks the cache for data.
	- If not found, queries the database and stores the data in the cache.
	- Uses TTL to automatically expire data after a set time.
	- Manages the cache using the LRU policy.
2. **Redirection**:
	- Redirects to the original long URL.
	- For expired URLs, returns a 410 status code and message, and removes the URL from the database and cache.

#### Cleanup Task

1. **Regular Batch Job**:
	- Periodically removes expired URLs from the database and cache.

#### DDOS Protection and Request Limiting

1. **API Key-based Request Limiting**:
	- Uses a unique `api_dev_key` for each client to limit request rates.

#### Logging and Monitoring

1. **Log Storage**:
	- Stores logs of major events.
2. **Real-time Monitoring**:
	- Builds a dashboard for real-time system status monitoring.

#### Backup and Recovery

1. **Regular Backups**:
	- Regularly backs up database and cache data and establishes recovery procedures.

#### High Level Design


![0](/assets/img/2024-08-07-[SystemDesign-URL-Shortener]-.md/0.png)

