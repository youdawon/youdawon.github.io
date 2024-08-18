---
layout: post
date: 2024-07-02
title: "[SystemDesign-Facebook Newsfeed] Database Schema"
tags: [System Design, Architecture, Facebook Newsfeed, ]
categories: [System Design, Problems, Facebook Newsfeed, ]
---


### 1. SQL

1. User

| Column          | Data Type | Attribute | Nullable |
| --------------- | --------- | --------- | -------- |
| user_id         | bigint    | PK        | NO       |
| user_name       | varchar   |           | NO       |
| creation_date   | datetime  |           | NO       |
| last_login_date | datetime  |           | NO       |

1. UserFollow

| Column               | Data Type | Attribute | Nullable |
| -------------------- | --------- | --------- | -------- |
| follower_id          | bigint    | PK        | NO       |
| user_id_or_entity_id | bigint    |           | NO       |
| type                 | tinyint   |           | NO       |

1. Entity

| Column             | Data Type    | Attribute | Nullable |
| ------------------ | ------------ | --------- | -------- |
| entity_id          | bigint       | PK        | NO       |
| type               | tinyint      |           | NO       |
| description        | varchar(512) |           | NO       |
| category           | smallint     |           | NO       |
| creation_date      | datetime     |           | NO       |
| last_modified_date | datetime     |           | NO       |

1. Newsfeed

| Column        | Data Type    | Attribute | Nullable |
| ------------- | ------------ | --------- | -------- |
| newsfeed_id   | bigint       | PK        | NO       |
| user_id       | bigint       |           | NO       |
| entity_id     | bigint       |           | NO       |
| content       | varchar(256) |           | YES      |
| creation_date | datetime     |           | NO       |
| view_cnt      | bigint       |           | NO       |

1. NewsfeedMedia

| Column      | Data Type | Attribute | Nullable |
| ----------- | --------- | --------- | -------- |
| newsfeed_id | bigint    | PK        | NO       |
| media_id    | bigint    | PK        | NO       |

1. Media

| Column        | Data Type    | Attribute | Nullable |
| ------------- | ------------ | --------- | -------- |
| media_id      | bigint       | PK        | NO       |
| type          | tinyint      |           | NO       |
| entity_id     | bigint       |           | YES      |
| description   | varchar(256) |           | YES      |
| media_url     | varchar(256) |           | YES      |
| creation_date | datetime     |           | NO       |

