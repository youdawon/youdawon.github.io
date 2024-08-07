---
layout: post
date: 2024-08-07
title: "[Instagram] API Design"
tags: [systemdesign, architecture, Instagram, ]
categories: [systemDesign, problems, Instagram, ]
---


### 1. Create Instagram Post

- **Endpoint:** `POST /api/v1/instagram`
- **Method:** `POST`
- **Description:** Create a new post on Instagram.
- **Request Header:**
	- Optional: `Authorization: Bearer jwt_token`
- **Request Body:**


{% raw %}
```json
	{
	  "content": "text12123",
	  "expiration_date": "2024-08-05T12:34:56Z",  // optional
	  "user_id": "user",  // optional
	  "url_alias": "test"  // optional
	}
```
{% endraw %}


- **Response Body:**


{% raw %}
```json
	{
	  "url_key": "test1232s",
	  "url": "<https://pastebin.com/test1232s>",
	  "expiration_date": "2024-08-05T12:34:56Z"
	}
```
{% endraw %}



#### 2. Get photos

- **Endpoint:** `GET /api/v1/photos`
- **Method:** `GET`
- **Description:** Retrieve a paste by URL key.
- **Response Body:**


{% raw %}
```json
	{
	  "url_key": "test1232s",
	  "url": "<https://pastebin.com/test1232s>",
	  "content": "This is a test paste.",
	  "expiration_date": "2024-08-05T12:34:56Z"
	}
```
{% endraw %}



#### 3. Create Post

- **Endpoint:** `POST /api/v1/instagram`
- **Method:** `POST`
- **Description:** Create a new paste.
- **Request Header:**
	- Optional: `Authorization: Bearer jwt_token`
- **Request Body:**


{% raw %}
```json
	{
	  "content": "text12123",
	  "expiration_date": "2024-08-05T12:34:56Z",  // optional
	  "user_id": "user",  // optional
	  "url_alias": "test"  // optional
	}
```
{% endraw %}


- **Response Body:**
- 


{% raw %}
```json
	{
	  "content": "text12123",
	  "expiration_date": "2024-08-05T12:34:56Z",  // optional
	  "user_id": "user",  // optional
	  "url_alias": "test"  // optional
	}
```
{% endraw %}



#### 4. Delete Post on Instagram

- **Endpoint:** `DELETE /api/v1/instagram/{photo_id}`
- **Method:** `DELETE`
- **Description:** Delete a post by photo_id.
- **Request Header:**
	- `Authorization: Bearer jwt_token`
- **Response Body:**


{% raw %}
```json
	{
	  "message": "Photo deleted successfully"
	}
```
{% endraw %}


