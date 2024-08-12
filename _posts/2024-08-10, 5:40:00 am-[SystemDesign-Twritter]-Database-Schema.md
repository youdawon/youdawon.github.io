---
layout: post
date: 2024-08-10, 5:40:00 am
title: "[SystemDesign-Twritter] Database Schema"
tags: [SystemDesign, Architecture, Twitter, ]
categories: [SystemDesign, Problems, Twitter, ]
---

1. User

| Column          | Data Type | Attribute | Nullable |
| --------------- | --------- | --------- | -------- |
| user_id         | bigint    | PK        | NO       |
| user_email      | varchar   |           | NO       |
| user_password   | varchar   |           | NO       |
| creation_date   | datetime  |           | NO       |
| last_login_date | datetime  |           | NO       |

1. UserFollow

| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| follower_id   | bigint    | PK, FK    | NO       |
| followee_id   | bigint    | PK, FK    | NO       |
| creation_date | datetime  |           | NO       |

1. Tweet

| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| tweet_id      | bigint    | PK        | NO       |
| user_id       | bigint    | FK        | NO       |
| content       | text      |           | YES      |
| creation_date | datetime  |           | NO       |

1. File

| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| file_id       | bigint    | PK        | NO       |
| tweet_id      | bigint    | FK        | NO       |
| file_size     | int       |           | NO       |
| file_url      | varchar   |           | NO       |
| creation_date | datetime  |           | NO       |

1. Favourite

| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| tweet_id      | bigint    | PK        | NO       |
| user_id       | bigint    | PK        | NO       |
| creation_date | datetime  |           | NO       |

1. Reply

| Column          | Data Type | Attribute | Nullable |
| --------------- | --------- | --------- | -------- |
| eply_id         | bigint    | PK        | NO       |
| tweet_id        | bigint    |           | NO       |
| parent_reply_id | bigint    |           | NO       |
| user_id         | bigint    |           | NO       |
| reply_content   | text      |           | NO       |
| creation_date   | datetime  |           | NO       |

