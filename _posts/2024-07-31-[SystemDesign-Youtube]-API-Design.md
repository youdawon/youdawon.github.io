---
layout: post
date: 2024-07-31
title: "[SystemDesign-Youtube] API Design"
tags: [SystemDesign, Architecture, Youtube, ]
categories: [SystemDesign, Youtube, ]
---


### 1. Upload Video

- **Endpoint:** `POST /api/v1/youtube`
- **Method:** `POST`
- **Description:** Upload a video
- **Request Header:**
	- Content-Type: multipart/form-data
- **Request Body (multipart/form-data):**
	- `video_title:` The name of the video (string).
	- `video_description:` Optional description of the video (string).
	- `tags:` Optional tag of the video (string).
	- `category_id:` The category of the video (string).
	- `default_language_id:` The default language id of the video (string).
	- `video_content:` The photo file to upload (file).
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



#### 2. Search Video

- **Endpoint:** `GET /api/v1/youtube/search`
- **Method:** `GET`
- **Request Parameters:**
	- `search_query=title`
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



#### 3. Streaming Video

- **Endpoint:** `GET /api/v1/youtube/{video_id}/stream`
- **Method**: `GET`
- **Description**: Streams video from a specified offset, supporting multi-device playback with codec and resolution options.

#### Request Parameters


#### Path Parameter

- **`video_id`** **(string)**: Unique identifier for the video.

#### Query Parameters

- **`offset`** **(number)**: Start time in seconds from the video’s beginning.
- **`codec`** **(string)**: Requested video codec (e.g., `h264`, `vp9`).
- **`resolution`** **(string)**: Desired video resolution (e.g., `1080p`, `720p`).

#### Request Headers

- **`Authorization`** **(string)**: `Bearer <jwt>`.

#### Response


#### Response Codes

- **`200 OK`**: Successful streaming from the specified offset.
- **`206 Partial Content`**: Partial content for seeking.
- **`404 Not Found`**: Video not found.
- **`403 Forbidden`**: Invalid API key or unauthorized access.
- **`400 Bad Request`**: Unsupported codec or resolution.

#### Response Headers

- **`Content-Type`**: `video/mp4`, `video/webm`, etc.
- **`Content-Length`**: Length of the video or byte range.
- **`Accept-Ranges`**: Supports range requests.
- **`Cache-Control`**: Controls caching behavior.

#### Example Request



{% raw %}
```text
GET /videos/12345/stream?offset=120&codec=h264&resolution=720p HTTP/1.1
Host: api.yourdomain.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```
{% endraw %}


