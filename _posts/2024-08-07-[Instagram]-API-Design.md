---
layout: post
date: 2024-08-07
title: "[Instagram] API Design"
tags: [systemdesign, architecture, Instagram, ]
categories: [systemDesign, problems, Instagram, ]
---


### 1. Create Post

- **Endpoint:** `POST /api/v1/instagram`
- **Method:** `POST`
- **Description:** Create a new post and upload a photo to Amazon S3.
- **Request Header:**
	- `Authorization: Bearer jwt_token`
- **Request Body (multipart/form-data):**
	- `content_name:` The name of the content (string).
	- `photo:` The photo file to upload (file).

#### Request Header Example



{% raw %}
```text
Content-Type: multipart/form-data
```
{% endraw %}


- **Response Body:**


{% raw %}
```json
{
  "message": "Photo uploaded successfully",
  "content_name": "My Photo",
  "photo_url": "https://your-s3-bucket.s3.amazonaws.com/1611234567890-photo.png"
}
```
{% endraw %}



#### 2. Get Post

- **Endpoint:** `GET /api/v1/instagram`
- **Method:** `GET`
- **Description:** Retrieve content, `content_title` is optional.
- **Request Header:**
	- `Authorization: Bearer jwt_token`
- **Request Parameters:**
	- Optional: `content_title=title`
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



#### 3. Delete Post

- **Endpoint:** `DELETE /api/v1/instagram/{content_id}`
- **Method:** `DELETE`
- **Description:** Delete a post by `content_id`.
- **Request Header:**
	- `Authorization: Bearer jwt_token`
- **Response Body:**

	
{% raw %}
```json
	{
	  "message": "Content deleted successfully"
	}
```
{% endraw %}



#### 4. Follow/Unfollow a User

- **Endpoint:** `POST /api/v1/instagram/follow`
- **Method:** `POST`
- **Description:** Follow/Unfollow a user.
- **Request Header:**
	- `Authorization: Bearer jwt_token`
- **Request Body:**

	
{% raw %}
```json
	{
	  "followee_id": 123,
	  "follow_yn": "Y"  // Y : follow, N : unfollow
	}
```
{% endraw %}


- **Response Body:**

	
{% raw %}
```json
	{
	  "message": "Followed successfully"
	}
```
{% endraw %}



#### 5. Get NewsFeed

- **Endpoint:** `GET /api/v1/instagram/newsfeed`
- **Method:** `GET`
- **Description:** Get news feed.
- **Request Header:**
	- `Authorization: Bearer jwt_token`
- **Request Parameters:**
	- Pagination: `page=<page_number>&size=<page_size>`
- **Response Body:**

	
{% raw %}
```json
	{
	  "newsfeed": [
	    {
	      "newsfeed_id": 1,
	      "followee_id": 1,
	      "user_name": "user1",
	      "content_url": "http://test.image.png",
	      "creation_date": "2024-08-05T12:34:56Z"
	    },
	    {
	      "newsfeed_id": 2,
	      "followee_id": 2,
	      "user_name": "user2",
	      "content_url": "http://example.image.png",
	      "creation_date": "2024-08-05T13:34:56Z"
	    }
	  ],
	  "page": 1,
	  "size": 10,
	  "total_pages": 5,
	  "total_newsfeeds": 50
	}
```
{% endraw %}


