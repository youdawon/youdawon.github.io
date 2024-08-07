---
layout: post
date: 2024-08-07
title: "[URL Shortener] Capacity Estimation"
tags: [systemdesign, urlshortener, architecture, ]
categories: [systemDesign, problems, urlShortener, ]
---


## Step 1: Traffic Estimation

1. **QPS (Queries Per Second) Estimation**

	
{% raw %}
```markdown
	Monthly Requests for new URL shortenings = 500,000,000 per month
	Read/Write ratio : 100:1
	Write QPS: 500,000,000 / (30 * 24 * 60 * 60) = 200 QPS
	Read QPS: 200 QPS * 100 = 20,000 QPS
```
{% endraw %}


2. **Peak Traffic Estimation**:
	- Consider peak traffic times, assuming peak traffic is double the average.

	
{% raw %}
```markdown
	Peak QPS = Average QPS * Peak Factor
	Peak QPS = 20,000 * 2 = 40,000 QPS
```
{% endraw %}



#### Step 2: Data Storage Estimation

1. **Calculate Data Size per URL**:
	- Determine the average size of stored data for each URL.

	
{% raw %}
```markdown
	Total Size per URL = 500 bytes
```
{% endraw %}


2. **Daily Storage Requirement**:
	- Estimate the number of URLs generated daily.

	
{% raw %}
```markdown
	Daily Storage Requirement = 24 * 60 * 60 * 200 * 500 bytes = 8.64 GB/day
```
{% endraw %}


3. **Annual Storage Requirement**:

	
{% raw %}
```markdown
	Annual Storage Requirement = Daily Storage Requirement * 365
	Annual Storage Requirement = 8.64 GB/day * 365 ≈ 3.1 TB/year
```
{% endraw %}


4. **5-Year Storage Requirement**:

	
{% raw %}
```markdown
	3.1 TB/year * 5 = 15.5 TB
```
{% endraw %}



#### Step 3: Memory Requirements

1. **Cache Size Calculation**:
	- Estimate the cache size needed based on frequently accessed URLs.

	
{% raw %}
```markdown
	Cache Hit Rate = 20%
	Cache Size = Daily URL Count * Cache Hit Rate * Total Size per URL
	Cache Size = 1,000,000 * 0.2 * 500 bytes = 100 MB
```
{% endraw %}



#### Step 4: Database Requirements

1. **Storage Requirement for 5 Years**:
	- Calculate the total storage needed over a period of 5 years.

	
{% raw %}
```markdown
	Storage Requirement for 5 years = Annual Storage Requirement * 5
	Storage Requirement for 5 years = 3.1 TB/year * 5 ≈ 15.5 TB
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
```scss
	Total Traffic = (Request Traffic + Response Traffic) * 8 (bits/byte) / 1,000,000 (Mbps conversion)
	Bandwidth = 3,072,000 bytes/sec * 8 / 1,000,000 = 24.576 Mbps
```
{% endraw %}



Thus, the required network bandwidth is approximately 24.576 Mbps.

