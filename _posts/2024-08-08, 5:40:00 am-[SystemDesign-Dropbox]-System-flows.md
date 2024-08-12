---
layout: post
date: 2024-08-08, 5:40:00 am
title: "[SystemDesign-Dropbox] System flows"
tags: [SystemDesign, Architecture, Dropbox, ]
categories: [SystemDesign, Problems, Dropbox, ]
---


### 1. Initial File Upload Request:

- **1.1. User Action:** The user selects a file to upload from their local device.
- **1.2. Local Preparation:** The client app divides the file into chunks and stores metadata about each chunk (e.g., chunk number, size, state) in the local database.
- **1.3. API Request:** The client sends a request to the File Service via the Load Balancer/API Gateway, asking to upload the file.

#### **2. Server Processing:**

- **2.1. Presigned URL Generation:** The File Service requests a presigned URL from Amazon S3 for the file.
- **2.2. Response to Client:** The File Service returns the presigned URL to the client for direct upload to S3.

#### **3. Chunk Upload Process:**

- **3.1. Upload Execution:** The client uploads the file in chunks directly to S3 using the presigned URL.
- **3.2. Progress Monitoring:**
	- **3.2.1. Local Tracking:** The client keeps track of each chunk’s upload status locally, marking chunks as "completed" once they are successfully uploaded to S3.
	- **3.2.2. Server Notification:** S3 notifies the File Service of the upload progress, allowing the File Service to update the current process and file metadata.
- **3.3. Metadata Update:** After each successful chunk upload, the client updates the chunk’s status in the local database. The File Service also updates the metadata in the Metadata Storage (SQL).
- **3.4. Error Handling:** If an error or network issue occurs:
	- **3.4.1. Retry Logic:** The client retries uploading the failed chunk based on retry logic and an exponential backoff strategy.
	- **3.4.2. Resumption:** If the upload process is interrupted, the client resumes the upload from the last successfully uploaded chunk based on the saved state in the local database.

#### **4. Upload Completion:**

- **4.1. Final Metadata Update:** Once all chunks are successfully uploaded, the File Service finalizes the upload by updating the complete file metadata, including the file status, in the Metadata Storage.
- **4.2. Confirmation:** The client receives confirmation of the completed upload.

#### **5. Synchronization with Remote Server:**

- **5.1. Regular Sync Check:** When the client comes online, it calls the `getChange` API to check for changes on the remote server.
- **5.2. Change Detection:** The Sync Service compares the local files with those on the server, based on timestamps or versioning information.
- **5.3. Metadata Sync:** The Sync Service returns a list of file IDs with changes to the client.
- **5.4. Download Changed Files:** The client requests updated file metadata and downloads any changed files from S3 based on the received information.

#### **6. Remote Change Notification:**

- **6.1. Remote Change Detection:** If a change occurs on the remote server (e.g., a file is uploaded or modified by another client):
	- **6.1.1. Event Generation:** The Sync Service generates an event and publishes it to the Event Broker (Kafka).
	- **6.1.2. Client Notification:** The Event Broker notifies the client about the remote change.
- **6.2. Change Handling:** The client processes the notification, updates its local database, and downloads any necessary changes.

![0](/assets/img/2024-08-08, 5:40:00 am-[SystemDesign-Dropbox]-System-flows.md/0.png)

