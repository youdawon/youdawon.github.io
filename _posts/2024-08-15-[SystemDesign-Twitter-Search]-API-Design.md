---
layout: post
date: 2024-08-15
title: "[SystemDesign-Twitter Search] API Design"
tags: [System Design, Architecture, Twitter Search, ]
categories: [System Design, Problems, Twitter Search, ]
---


### 1. Search Tweets

- **Endpoint:** `GET /api/v1/twitter/search`
- **Method:** `GET`
- **Request Parameters:**
	- `terms=write keywords`
	- `sort=1 //1:Latest(default), 2:Best Matched, 3:Most Liked`
	- Pagination: `page=<page_number>&size=<page_size>&sort=<sort>`
- **Response Body:**

	
{% raw %}
```json
	{
	  "tweets": [
	    {
	      "tweet_id": test1232,
	      "content_url": "https://pastebin.com/test1232s",
	      "tweet_text": "name1",
	      "creation_date": "2024-08-05T12:34:56Z"
	    },
	    {
	      "tweet_id": test1232,
	      "content_url": "https://pastebin.com/test1232t",
	      "tweet_text": "name2",
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


