---
layout: post
date: 2024-08-12
title: "[SystemDesign-Youtube] Database Schema"
tags: [System Design, Architecture, Youtube, ]
categories: [System Design, Problems, Youtube, ]
---

1. User

| Column          | Data Type | Attribute | Nullable |
| --------------- | --------- | --------- | -------- |
| user_id         | int       | PK        | No       |
| user_name       | String    |           | No       |
| creation_date   | datetime  |           | No       |
| last_login_date | datetime  |           | Yes      |

1. Video

| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| video_id      | bigint    | PK        | NO       |
| title         | varchar   |           | NO       |
| description   | text      |           | NO       |
| size          | int       |           | NO       |
| thumbnail_url | varchar   |           | NO       |
| user_id       | bigint    |           | NO       |
| like_cnt      | bigint    |           | NO       |
| dislike_cnt   | bigint    |           | NO       |
| view_cnt      | bigint    |           | NO       |

1. Comment

| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| comment_id    | bigint    | PK        | NO       |
| video_id      | bigint    |           | NO       |
| user_id       | bigint    |           | NO       |
| comment       | text      |           | NO       |
| creation_date | datetime  |           | NO       |

