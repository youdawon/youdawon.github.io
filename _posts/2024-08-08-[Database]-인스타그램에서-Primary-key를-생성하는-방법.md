---
layout: post
date: 2024-08-08
title: "[Database] 인스타그램에서 Primary key를 생성하는 방법"
tags: [Dabatabse, Instagram, Architecture, ]
categories: [Database, ]
---


시스템 디자인을 공부하다가 대규모 서비스에서는 Primary Key를 어떤 식으로 구성하는지 궁금해졌다. 


Zookeeper를 이용해 노드 별로 생성할 수 있는 키 범위를 정하는 방법도 있고 Key Generation Service를 따로 구성해서 Base62(a-z, A-Z, 0-9)기준으로 키를 생성하여 DB에 저장한 후 사용하는 방법도 있었는데 아래와 같은 방법도 처음 보는 방법이라 정리해보았다. 


auto-increment 사용 시 PostgreSQL기준으로 1ms에 약 1000개의 키 생성이 가능한데 트래픽이 많은 인스타그램에서는 이러한 제한으로 병목현상이 생긴다고 한다. 나는 Primary Key를 auto-increment로 생성해서 사용하는 방법만 해봤는데 아무래도 서비스 규모가 다르다보니 글로벌 서비스에서는 Primary Key 생성하는데도 상당한 고민이 필요해보인다. 


#### 1. Key Features of Instagram's ID Generation

- **Sortable by Time:** IDs are time-sortable, allowing easy chronological ordering of content.
- **64-bit IDs:** Smaller index size and better storage in systems like Redis.
- **Minimal Complexity:** Keep the system simple and minimize additional components.

#### 2. Structure of the Generated IDs

- **41 bits for Timestamp:** Represents milliseconds since a custom epoch (e.g., January 1, 2011).
- **13 bits for Logical Shard ID:** Identifies the logical shard.
- **10 bits for Sequence Number:** Allows for up to 1024 unique IDs per millisecond per shard.

#### 3. ID Generation Algorithm

1. **Timestamp:** The first 41 bits are the number of milliseconds since a predefined epoch.
2. **Logical Shard ID:** The next 13 bits represent the logical shard ID, which helps in distributing data across multiple shards.
3. **Sequence Number:** The final 10 bits are a sequence number, which is reset every millisecond, allowing for 1024 unique IDs per millisecond per shard.

#### 4. Implementation in PostgreSQL



{% raw %}
```sql
CREATE OR REPLACE FUNCTION next_id(OUT result bigint) AS $$
DECLARE
    our_epoch bigint := 1314220021721; -- Custom epoch (e.g., September 9, 2011)
    seq_id bigint;
    now_millis bigint;
    shard_id int := 5; -- Example shard ID (should be determined dynamically in a real scenario)
BEGIN
    -- Get the next value of the sequence, modulo 1024
    SELECT nextval('table_id_seq') % 1024 INTO seq_id;

    -- Get the current time in milliseconds
    SELECT FLOOR(EXTRACT(EPOCH FROM clock_timestamp()) * 1000) INTO now_millis;

    -- Shift the timestamp to the left by 23 bits (64 - 41)
    result := (now_millis - our_epoch) << 23;

    -- Add the shard ID (shifted left by 10 bits)
    result := result | (shard_id << 10);

    -- Add the sequence number
    result := result | (seq_id);
END;
$$ LANGUAGE PLPGSQL;
```
{% endraw %}



#### 5. Table Creation with the Custom ID


When creating a table for storing content, the custom ID generation function can be used as the default value for the primary key:



{% raw %}
```sql
CREATE TABLE Content (
    content_id bigint NOT NULL DEFAULT next_id(),
    user_id int NOT NULL,
    content_name VARCHAR(100) NOT NULL,
    photo_path VARCHAR(255) NOT NULL,
    creation_date TIMESTAMP NOT NULL,
    PRIMARY KEY (content_id),
    FOREIGN KEY (user_id) REFERENCES User(user_id)
);
```
{% endraw %}



#### Summary

- **Timestamp (41 bits):** Ensures IDs are sortable by time.
- **Shard ID (13 bits):** Distributes data across logical shards.
- **Sequence Number (10 bits):** Allows multiple unique IDs to be generated per millisecond per shard.

참고 : [https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c](https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c)

