---
layout: post
date: 2024-08-07
title: "[URL Shortener] Database Schema"
tags: [systemdesign, urlshortener, architecture, ]
categories: [systemDesign, problems, urlShortener, ]
---


### 1. URL Table


| Column            | Data Type      | Attribute | Nullable |
| ----------------- | -------------- | --------- | -------- |
| `url_id`          | `int`          | PK        | No       |
| `original_url`    | `varchar(250)` | Index     | No       |
| `user_id`         | `int`          |           | No       |
| `expiration_date` | `datetime`     |           | No       |
| `creation_date`   | `datetime`     |           | No       |

undefined
### 2. User Table


| Column            | Data Type  | Attribute | Nullable |
| ----------------- | ---------- | --------- | -------- |
| `user_id`         | `int`      | PK        | No       |
| `last_login_date` | `datetime` |           | Yes      |
| `creation_date`   | `datetime` |           | No       |

undefined