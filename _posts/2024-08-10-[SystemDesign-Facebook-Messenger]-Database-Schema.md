---
layout: post
date: 2024-08-10
title: "[SystemDesign-Facebook Messenger] Database Schema"
tags: [SystemDesign, Architecture, FacebookMessenger, ]
categories: [SystemDesign, Problems, FacebookMessenger, ]
---


### 1. SQL

1. User

| Column          | Data Type | Attribute            | Nullable |
| --------------- | --------- | -------------------- | -------- |
| user_id         | int       | PK                   | NO       |
| user_name       | varchar   |                      | NO       |
| user_status     | varchar   | 1: online, 2:offline | NO       |
| creation_date   | datetime  |                      | NO       |
| last_login_date | datetime  |                      | NO       |

undefined1. Chat

| Column        | Data Type | Attribute | Nullable |
| ------------- | --------- | --------- | -------- |
| chat_id       | int       | PK        | NO       |
| user_id       | int       | FK        | NO       |
| is_group_chat | boolean   |           | NO       |
| creation_date | datetime  |           | NO       |

undefined1. ChatUser

| Column      | Data Type | Attribute | Nullable |
| ----------- | --------- | --------- | -------- |
| chat_id     | int       | PK, FK    | NO       |
| user_id     | int       | PK, FK    | NO       |
| joined_date | datetime  |           | NO       |

undefined
### 2. NoSQL


key : user_id#chat_id#timestamp


timestamp는 역순으로 정렬

