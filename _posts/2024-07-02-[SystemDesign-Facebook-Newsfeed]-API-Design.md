---
layout: post
date: 2024-07-02
title: "[SystemDesign-Facebook Newsfeed] API Design"
tags: [System Design, Architecture, Facebook Newsfeed, ]
categories: [System Design, Problems, Facebook Newsfeed, ]
---


### 1. Get Newsfeed

- **Endpoint:** `GET /api/v1/facebook/newsfeed`
- **Method:** `GET`
- **Request header:**
	- user_id
- **Request Parameters:**
	- Pagination: `page=<page_number>&size=<page_size>`
- **Response Body:**

	
{% raw %}
```json
	{
	  "newsfeed": [
	    {
	      "content_id": test1232,
	      "content_url": "https://pastebin.com/test1232s",
	      "desc": "name1",
	      "creation_date": "2024-08-05T12:34:56Z"
	    },
	    {
	      "content_id": test1232,
	      "content_url": "https://pastebin.com/test1232t",
	      "desc": "name2",
	      "creation_date": "2024-08-06T12:34:56Z"
	    }
	  ],
	  "page": 1,
	  "size": 10,
	  "total_pages": 2,
	  "total_posts": 20
	}
```
{% endraw %}


