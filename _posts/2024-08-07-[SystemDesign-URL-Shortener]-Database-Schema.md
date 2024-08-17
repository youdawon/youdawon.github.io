---
layout: post
date: 2024-08-07
title: "[SystemDesign-URL Shortener] Database Schema"
tags: [System Design, UrlShortener, Architecture, ]
categories: [System Design, Problems, UrlShortener, ]
---


### 1.Paste Table


| Column            | Data Type      | Attribute | Nullable |
| ----------------- | -------------- | --------- | -------- |
| `url_id`          | `int`          | PK        | No       |
| `text`            | `varchar(512)` |           | No       |
| `data_path`       | `varchar(512)` |           | No       |
| `creation_date`   | `datetime`     |           | No       |
| `expiration_date` | `datetime`     |           | No       |


#### 2.User Table


| Column            | Data Type     | Attribute | Nullable |
| ----------------- | ------------- | --------- | -------- |
| `user_id`         | `int`         | PK        | No       |
| `user_email`      | `varchar(40)` |           | No       |
| `creation_date`   | `datetime`    |           | No       |
| `last_login_date` | `datetime`    |           | No       |

