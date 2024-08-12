---
layout: post
date: 2024-07-31
title: "[SystemDesign-Youtube] Capacitiy Estimation"
tags: [SystemDesign, Architecture, Youtube, ]
categories: [SystemDesign, Youtube, ]
---


1,500,000,000 total users, 800,000,000 daily active users. 


A user views five videos every day 


the total video-views per second : (800,000,000*5) / (24*60*60) = 46,296 videos/sec


upload / view radio = 1:200, every video have 200 videos viewed


how many videos upload per second?


	46296 / 200 = 230 video/sec


#### 1. Storage Estimates


Every minute 500 hours worth of videos are uploaded on Youtube. one minute of video need 50MB of storage.


total storage needed for videos uploaded in a min



{% raw %}
```text
500hours * 50MB * 60min = 1,500,000MB -> 1500GB/min
```
{% endraw %}



#### 2. Bandwidth Estimates


Uploading each minute of the video takes 10MB



{% raw %}
```text
Write : 500hours * 60mins * 10MB = 300,000MB -> 300GB/min
Read : 500hours *
```
{% endraw %}


