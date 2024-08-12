---
layout: post
date: 2024-08-07
title: "[SystemDesign-Pastebin] API Design"
tags: [SystemDesign, Architecture, Pastebin, ]
categories: [SystemDesign, Problems, Pastebin, ]
---


### 1. Create Paste

- **Endpoint:** `POST /api/v1/pastebin`
- **Method:** `POST`
- **Description:** Create a new paste.
- **Request Header:**

	`Authorization: Bearer jwt_token`

- **Request Body:**


{% raw %}
```json
	{
	  "content": "text12123",
	  "expiration_date": "2024-08-05T12:34:56Z",  // optional
	  "user_id": "user",  
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



#### 2. Get Paste

- **Endpoint:** `GET /api/v1/pastebin/{url_key}`
- **Method:** `GET`
- **Description:** Retrieve a paste by URL key.
- **Request Header:**

`Authorization: Bearer jwt_token`

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



#### 3. Delete Paste

- **Endpoint:** `DELETE /api/v1/pastebin/{url_key}`
- **Method:** `DELETE`
- **Description:** Delete a paste by URL key.
- **Request Header:**
	- `Authorization: Bearer jwt_token`
- **Response Body:**


{% raw %}
```json
	{
	  "message": "Paste deleted successfully",
	  "url_key": "test1232s"
	}
```
{% endraw %}


