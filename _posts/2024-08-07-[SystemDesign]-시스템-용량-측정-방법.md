---
layout: post
date: 2024-08-07
title: "[SystemDesign] 시스템 용량 측정 방법"
tags: [SystemDesign, Architecture, ]
categories: [SystemDesign, Basics, ]
---


# Step 1: Traffic Estimation

1. **QPS (Queries Per Second) Estimation**:
	- Calculate the expected number of requests per day.

	
{% raw %}
```markdown
	Daily Requests = 100,000,000
	QPS = Daily Requests / (24 * 60 * 60)
	QPS = 100,000,000 / 86,400 ≈ 1157 QPS
```
{% endraw %}


2. **Peak Traffic Estimation**:
	- Consider peak traffic times, assuming peak traffic is double the average.

	
{% raw %}
```markdown
	Peak QPS = Average QPS * Peak Factor
	Peak QPS = 1157 * 2 ≈ 2314 QPS
```
{% endraw %}



#### Step 2: Data Storage Estimation

1. **Calculate Data Size per URL**:
	- Determine the average size of stored data for each URL.

	
{% raw %}
```markdown
	Average Original URL Length = 100 bytes
	Short URL Length = 10 bytes
	Metadata Size = 50 bytes
	Total Size per URL = 100 + 10 + 50 = 160 bytes
```
{% endraw %}


2. **Daily Storage Requirement**:
	- Estimate the number of URLs generated daily.

	
{% raw %}
```markdown
	Daily URL Count = 1,000,000 URLs/day
	Daily Storage Requirement = Daily URL Count * Total Size per URL
	Daily Storage Requirement = 1,000,000 * 160 bytes = 160 MB/day
```
{% endraw %}


3. **Annual Storage Requirement**:

	
{% raw %}
```markdown
	Annual Storage Requirement = Daily Storage Requirement * 365
	Annual Storage Requirement = 160 MB/day * 365 ≈ 58.4 GB/year
```
{% endraw %}



#### Step 3: Memory Requirements

1. **Cache Size Calculation**:
	- Estimate the cache size needed based on frequently accessed URLs.

	
{% raw %}
```markdown
	Cache Hit Rate = 20%
	Cache Size = Daily URL Count * Cache Hit Rate * Total Size per URL
	Cache Size = 1,000,000 * 0.2 * 160 bytes = 32 MB
```
{% endraw %}



#### Step 4: Database Requirements

1. **Storage Requirement for 5 Years**:
	- Calculate the total storage needed over a period of 5 years.

	
{% raw %}
```shell
	Storage Requirement for 5 years = Annual Storage Requirement * 5
	Storage Requirement for 5 years = 58.4 GB/year * 5 ≈ 292 GB
```
{% endraw %}


2. **IOPS Estimation**:
	- Estimate the database IOPS for write operations.

	
{% raw %}
```markdown
	Write IOPS = Daily URL Count / (24 * 60 * 60)
	Write IOPS = 1,000,000 / 86,400 ≈ 11.6 IOPS
```
{% endraw %}



#### Step 5: Bandwidth Requirements


Calculate the bandwidth based on request and response sizes and frequencies.

1. **Bandwidth Calculation**:
	- **Request Traffic**: QPS * Request Size
	- **Response Traffic**: QPS * Response Size
	- **Total Traffic**: Request Traffic + Response Traffic

	
{% raw %}
```markdown
	Total Traffic = (Request Traffic + Response Traffic) * 8 (bits/byte) / 1,000,000 (Mbps conversion)
	Bandwidth = 3,072,000 bytes/sec * 8 / 1,000,000 = 24.576 Mbps
```
{% endraw %}



Thus, the required network bandwidth is approximately 24.576 Mbps.

