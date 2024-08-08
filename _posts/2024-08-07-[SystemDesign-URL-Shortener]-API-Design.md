---
layout: post
date: 2024-08-07
title: "[SystemDesign-URL Shortener] API Design"
tags: [SystemDesign, UrlShortener, Architecture, ]
categories: [SystemDesign, Problems, UrlShortener, ]
---



{% raw %}
```markdown
```
{% endraw %}



**Request Body:**



{% raw %}
```json
{
  "original_url": "http://example.com",
  "user_id": "test",
  "expiration_date": 1231232
}
```
{% endraw %}



**Response Body:**



{% raw %}
```json
{
  "url_key": 123,
  "original_url": "http://example.com",
  "short_url": "http://example.com",
  "expiration_date": 1231232
}
```
{% endraw %}



**Request:**

- `expiration_date`: Optional

**Response:**

- **200 OK:** URL shortened successfully.
- **400 Bad Request:** Invalid URL format or length exceeds limit.
- **404 Not Found:** URL is not valid.
- **401 Unauthorized:** Invalid or missing `api_dev_key`.
- **429 Too Many Requests:** Rate limit exceeded.

#### 2. Get Original URL API


**Endpoint:** `/api/v1/url/{url_key}`


**Method:** `GET`


**Headers:**



{% raw %}
```json

{
  "api_dev_key": "your_api_dev_key_here"
}
```
{% endraw %}



**Response:**

- **200 OK:** Original URL retrieved.
- **404 Not Found:** Shortened URL does not exist or has expired.
- **401 Unauthorized:** Invalid or missing `api_dev_key`.
- **429 Too Many Requests:** Rate limit exceeded.

#### 3. Redirect to Original URL API


**Endpoint:** `/{url_key}`


**Method:** `GET`


**Response:**

- **302 Found:** Redirects to the original URL.
- **410 Gone:** Shortened URL has expired.
- **404 Not Found:** Shortened URL does not exist.

#### 4. Delete Shortened URL API


**Endpoint:** `/api/v1/url/{url_key}`


**Method:** `DELETE`


**Headers:**



{% raw %}
```json

{
  "api_dev_key": "your_api_dev_key_here"
}
```
{% endraw %}



**Response:**

- **200 OK:** URL deleted successfully.
- **404 Not Found:** Shortened URL does not exist.
- **401 Unauthorized:** Invalid or missing `api_dev_key`.
- **429 Too Many Requests:** Rate limit exceeded.
