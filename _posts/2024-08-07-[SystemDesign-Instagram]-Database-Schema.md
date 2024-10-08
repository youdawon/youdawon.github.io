---
layout: post
date: 2024-08-07
title: "[SystemDesign-Instagram] Database Schema"
tags: [System Design, Architecture, Instagram, ]
categories: [System Design, Problems, Instagram, ]
---


### 1.User Table


| Column            | Data Type     | Attribute | Nullable |
| ----------------- | ------------- | --------- | -------- |
| `user_id`         | `int`         | PK        | No       |
| `user_name`       | `varchar(20)` |           | No       |
| `user_email`      | `varchar(32)` |           | No       |
| `date_of_birth`   | `datetime(4)` |           | Yes      |
| `creation_date`   | `datetime(4)` |           | No       |
| `last_login_date` | `datetime(4)` |           | No       |


#### 2.Userfollower Table


| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| `follower_id` | `int`     | PK        | No       |
| `followee_id` | `int`     | PK        | No       |


#### 3.Content Table


| Column          | Data Type      | Attribute | Nullable |
| --------------- | -------------- | --------- | -------- |
| `content_id`    | `int`          | PK        | No       |
| `content_name`  | `varchar(100)` |           | No       |
| `user_id`       | `int`          | FK        | No       |
| `content_url`   | `varchar(100)` |           | No       |
| `creation_date` | `datetime`     |           | No       |


#### 4.NewsFeed Table


| Column          | Data Type  | Attribute | Nullable |
| --------------- | ---------- | --------- | -------- |
| `newsfeed_id`   | `int`      | PK        | No       |
| `user_id`       | `int`      | FK        | No       |
| `content_id`    | `int`      | FK        | No       |
| `creation_date` | `datetime` |           | No       |

