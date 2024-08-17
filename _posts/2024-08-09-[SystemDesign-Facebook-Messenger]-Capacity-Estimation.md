---
layout: post
date: 2024-08-09
title: "[SystemDesign-Facebook Messenger] Capacity Estimation"
tags: [System Design, Architecture, FacebookMessenger, ]
categories: [System Design, Problems, FacebookMessenger, ]
---


500M daily active users, each user send 40 messages daily, 20 billion messages per day


#### 1. Storage Estimation

- Message size : 100 bytes
- One day : 20,000,000,000 * 100 = 2,000,000,000,000bytes = 2TB
- 5years : 2,000,000,000,000 * 365 days * 5 years = 3,650,000,000,000,000 bytes = 3.6PB
- 기타 사용자 정보나 메세지의 메타데이터 등의 정보 저장 용량은 미포함된 용량임

#### 2. Bandwidth Estimation

- 2,000,000,000,000 / (24 * 60 * 60) = 23,148,148 = 23MB
