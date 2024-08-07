---
layout: post
date: 2024-08-07
title: "[Pastebin] Capacity Estimation"
tags: [systemdesign, architecture, pastebin, ]
categories: [systemDesign, problems, pastebin, ]
---


## Traffic Estimation


read/write Ratio : 5:1


one million new pastes every day


#### Step 1: Traffic Estimation

1. **QPS (Queries Per Second) Estimation**

{% raw %}



{% raw %}
```text
    Write QPS: 12 * 5 = 60 pastes/s
    Read QPS: 1M / (24 * 3600) = 12 pastes/s
```
{% endraw %}



{% endraw %}


#### Step 2: Data Storage Estimation

1. **Calculate Data Size per URL**:
	- Determine the average size of stored data for each URL.

{% raw %}



{% raw %}
```text
    10KB per pastes
    per day: 10GB
    for a year : 3.6TB
    for 10 years : 36TB
```
{% endraw %}



{% endraw %}


#### Step 3: Memory Requirements

1. **Cache Size Calculation**:
	- Estimate the cache size needed based on frequently accessed URLs.

{% raw %}



{% raw %}
```text
    follow 80-20rules
    per day : 0.2 * 10KB * 5,000,000 = 10GB
```
{% endraw %}



{% endraw %}


#### Step 4: Bandwidth Requirements


{% raw %}



{% raw %}
```text
    read per second : 60 pastes/s * 10KB = 600KB/s
    write per second : 12 pastes/s * 10KB = 120KB/s
```
{% endraw %}



{% endraw %}
