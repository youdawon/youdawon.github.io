---
layout: post
date: 2024-08-12
title: "[SystemDesign-Youtube] Capacity Estimation"
tags: [System Design, Architecture, Youtube, ]
categories: [System Design, Problems, Youtube, ]
---


1,500,000,000 total users, 800,000,000 daily active users. 


A user views five videos every day 


the total video-views per second : (800,000,000*5) / (24*60*60) = 46,296 videos/sec


upload / view radio = 1:200, every video have 200 videos viewed


how many videos upload per second?


	46296 / 200 = 230 video/sec


Message Queue를 통해서 encoding시 몇 개의 encoding 서비스가 동시에 필요할까? 비디오를 인코딩하는 과정이 1분이 넘어가기 때문에 230 * 60분을 곱한 값이 encoding 서비스의 개수로 적정할 것이다.


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
```
{% endraw %}


