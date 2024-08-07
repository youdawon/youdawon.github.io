---
layout: post
date: 2024-08-07
title: "[Instagram] Data Schema"
tags: [systemdesign, architecture, Instagram, ]
categories: [systemDesign, problems, Instagram, ]
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

undefined
### 2.Userfollower Table


| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| `follower_id` | `int`     | PK        | No       |
| `followee_id` | `int`     | PK        | No       |

undefined
### 3.Photo Table


| Column          | Data Type      | Attribute | Nullable |
| --------------- | -------------- | --------- | -------- |
| `photo_id`      | `int`          | PK        | No       |
| `photo_name`    | `varchar(100)` | INDEX     | No       |
| `user_id`       | `int`          | FK        | No       |
| `photo_path`    | `varchar(100)` |           | No       |
| `creation_date` | `datetime`     |           | No       |

undefined