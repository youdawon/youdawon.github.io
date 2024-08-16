---
layout: post
date: 2024-08-16
title: "[SystemDesign-Twitter Search] Data Partitioning"
tags: [SystemDesign, Architecture, Twitter Search, ]
categories: [SystemDesign, Problems, Twitter Search, ]
---


120GB of new data every day. 



{% raw %}
```text
For 5 years : 120GB * 365 days * 5 years = 219TB
```
{% endraw %}



For the fault tolerance : 500GB



{% raw %}
```text
500TB % 4TB = 125 servers
```
{% endraw %}



400M new tweets every day


how many tweet object can we expect in 5 years?



{% raw %}
```text
400M * 365 days * 5 years = 730B
```
{% endraw %}



최소 5바이트(8bits * 5) 


인덱스의 크기 



{% raw %}
```text
500K * 5(length) = 2.5MB
```
{% endraw %}



how much memory will we need to store all the TweetIDs for Index for two years?



{% raw %}
```text
730Billion % 5 years * 2 years * 5 (length) = 1460GB
```
{% endraw %}


