---
layout: post
date: 2024-08-07
title: "[Pastebin] System flows and High Level Design"
tags: [SystemDesign, Architecture, Pastebin, ]
categories: [SystemDesign, Problems, Pastebin, ]
---


### Unique Key Generation and Management

- **Encoding:** Base62 (a-z, A-Z, 0-9)
- **Key Length:** 6 characters
- **Total Combinations:**
	- \( 62^6 = 56,800,235,584 \)
- **Expected URLs:** 36,000,000,000 (sufficient to avoid collisions)

#### Metadata Storage (RDBMS)

- **Database:** PostgreSQL or MySQL
- **Purpose:** Store detailed metadata about pastes, including user information, expiration dates, visibility, and references to content.

#### Key Management (NoSQL)

- **Database:** Cassandra or MongoDB
- **Purpose:** Efficiently manage and recycle unique keys using a key-based NoSQL database.
- **Collections:** `ready_keys` (for available keys) and `used_keys` (for used keys).

#### Caching

- **Algorithm:** Least Recently Used (LRU)
- **Purpose:** Caching metadata and content for quick access.

#### Flows


#### Creating a Pastebin Entry

1. **Client Request:** Client sends a request to create a new paste.
2. **Load Balancer:** Distributes the request to an available server.
3. **Server Processing:** Validates the input data.
4. **Unique Key Generation:** Server selects an unused key from the `ready_keys` collection and moves it to the `used_keys` collection in NoSQL.
5. **Metadata Storage:** Server stores metadata in the `pastes` table (RDBMS) and metadata cache (LRU).
6. **Content Storage:** Server stores content in object storage (e.g., S3) and object cache (LRU).
7. **Response to Client:** Server returns a response with the unique URL for the new paste.

#### Deleting a Pastebin Entry

1. **Trigger Deletion:** A paste is deleted manually or automatically when it expires.
2. **Remove Data from Cache and Storage:** Server removes content from the object cache and object storage, and metadata from the metadata cache and `pastes` table (RDBMS).
3. **Update Key-DB:** Server moves the unique key from the `used_keys` collection back to the `ready_keys` collection in NoSQL.
4. **Cleanup Batch Job:** Periodically scans and deletes expired entries, recycling keys.

#### High Level Design


![0](/assets/img/2024-08-07-[Pastebin]-System-flows-and-High-Level-Design.md/0.png)

