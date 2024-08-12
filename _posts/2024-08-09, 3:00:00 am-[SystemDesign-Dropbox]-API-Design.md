---
layout: post
date: 2024-08-09, 3:00:00 am
title: "[SystemDesign-Dropbox] API Design"
tags: [SystemDesign, Architecture, Dropbox, ]
categories: [SystemDesign, Problems, Dropbox, ]
---


### 1. Upload File

- **Endpoint:** `POST /api/v1/files`
- **Method:** `POST`
- **Description:** Upload a photo to Amazon S3.
- **Request Header:**
	- Content-Type: multipart/form-data
- **Request Body (multipart/form-data):**
	- `file_name:` The name of the content (string).
	- `file:` The photo file to upload (file).
- **Response Body:**


{% raw %}
```json
{
  "message": "Photo uploaded successfully",
  "file_name": "My Photo",
  "file_url": "https://your-s3-bucket.s3.amazonaws.com/1611234567890-photo.png"
}
```
{% endraw %}



#### 2. Get File

- **Endpoint:** `GET /api/v1/files?file_id={file_id}`
- **Method:** `GET`
- **Description:** Retrieve file metadata.
- **Response Body:**

	
{% raw %}
```json
	{
	    "status": "success",
	    "message": "Chunk uploaded successfully",
	    "chunk_details": {
	        "chunk_number": 3,
	        "chunk_size": "5MB",
	        "total_chunks": 10,
	        "upload_session_id": "123456789abcdef"
	    },
	    "file_metadata": {
	        "file_id": 2,
	        "user_id" : 1,
	        "file_name": "example_document.pdf",
	        "file_size": "50MB",
	        "uploaded_size": "15MB",
	        "upload_status": "in_progress",  //1:Started, 2:Finished, 3.Failed, 
	        "uploaded_at": "2024-08-09T12:34:56Z",
	        "checksum": "e99a18c428cb38d5f260853678922e03"
	    }
	}
```
{% endraw %}



#### 3. get Change

- **Endpoint:** `GET /api/v1/files/change?since={timestamp}`
- **Method:** `GET`
- **Description:** Get changes from a remote server.
- **Response Body:**

	
{% raw %}
```json
	{
		"file_id": [1, 2, 3, 4, 5, 6]
	}
```
{% endraw %}


