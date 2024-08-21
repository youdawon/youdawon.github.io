---
layout: post
date: 2024-08-20
title: "[SystemDesign-Yelp] Database Schema"
tags: [System Design, Yelp, ]
categories: [System Design, Problems, ]
---

1. Place

| Column      | Data Type    | Attribute | Nullable |
| ----------- | ------------ | --------- | -------- |
| place_id    | bigint(8)    | PK        | NO       |
| longitude   | bigint(8)    |           | NO       |
| Latitude    | bigint(8)    |           | NO       |
| place_name  | varchar(256) |           | NO       |
| description | varchar(512) |           | YES      |
| category    | tinyint(4)   |           | NO       |

1. Review

| Column        | Data Type    | Attribute | Nullable |
| ------------- | ------------ | --------- | -------- |
| review_id     | bigint(8)    | PK        | NO       |
| place_id      | bigint(8)    |           | NO       |
| user_id       | bigint(8)    |           | NO       |
| review_text   | varchar(512) |           | NO       |
| rating        | tinyint(4)   |           | NO       |
| creation_date | datetime     |           | NO       |

1. picture

| Column      | Data Type    | Attribute | Nullable |
| ----------- | ------------ | --------- | -------- |
| picture_id  | bigint       | PK        | NO       |
| review_id   | bigint       |           | NO       |
| picture_url | varchar(256) |           | NO       |

