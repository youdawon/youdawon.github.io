---
layout: post
date: 2024-08-20
title: "[SystemDesign-Yelp] API Design"
tags: [System Design, Yelp, ]
categories: [System Design, Problems, ]
---


### 1. Upload a place

- **Endpoint:** `POST /api/v1/yelp/place`
- **Method:** `POST`
- **Description:** Upload a place
- **Request Header:**
	- `user_id`
- **Request Body**
	- `place_name`
	- `latitude`
	- `longitude`
	- `category_id`
	- `place_description`
- **Response Body:**


{% raw %}
```json
{
  "message": "Place uploaded successfully"
}
```
{% endraw %}



#### 2. Search Video

- **Endpoint:** `GET /api/v1/yelp/search`
- **Method:** `GET`
- **Request Parameters:**
	- `search_query=title&category_id=1&user_location=&sort=`
	- Pagination: `page=<page_number>&size=<page_size>`
- **Response Body:**

	
{% raw %}
```json
	{
	  "posts": [
	    {
	      "content_id": test1232,
	      "content_url": "https://pastebin.com/test1232s",
	      "content_name": "name1",
	      "expiration_date": "2024-08-05T12:34:56Z"
	    },
	    {
	      "content_id": test1232,
	      "content_url": "https://pastebin.com/test1232t",
	      "content_name": "name2",
	      "expiration_date": "2024-08-06T12:34:56Z"
	    }
	  ],
	  "page": 1,
	  "size": 10,
	  "total_pages": 2,
	  "total_posts": 20
	}
```
{% endraw %}



#### 3. Upload a review

- **Endpoint:** `POST /api/v1/yelp/review`
- **Method:** `POST`
- **Description:** Upload a review
- **Request Header:**
	- Content-Type: multipart/form-data
	- user_id
- **Request Body (multipart/form-data):**
	- `video_title:` The name of the video (string).
	- `review_text:` review
	- `rating:` Optional tag of the video (string).
- **Response Body:**


{% raw %}
```json
{
  "message": "Review uploaded successfully"
}
```
{% endraw %}


