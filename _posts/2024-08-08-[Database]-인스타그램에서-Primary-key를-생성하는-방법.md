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


#### 1. Instagram ID 생성의 주요 특징

- **시간 정렬 가능**: ID는 시간에 따라 정렬할 수 있어서 콘텐츠를 연대순으로 쉽게 정렬할 수 있다.
- **64비트 ID**: Redis 같은 시스템에서 인덱스 크기를 줄이고, 저장 효율을 높일 수 있다.
- **최소한의 복잡성**: 시스템을 간단하게 유지하고, 추가 구성 요소를 최소화할 수 있다.

#### 2. 생성된 ID의 구조

- **타임스탬프에 41비트**: 특정 기준 시점(예: 2011년 1월 1일) 이후의 밀리초를 나타낸다.
- **논리 샤드 ID에 13비트**: 논리적 샤드를 식별할 수 있다.
- **시퀀스 번호에 10비트**: 샤드당 밀리초당 최대 1024개의 고유 ID를 생성할 수 있다.

#### 3. ID 생성 알고리즘

- **타임스탬프**: 처음 41비트는 미리 정한 기준 시점 이후의 밀리초 수를 나타낸다.
- **논리 샤드 ID**: 다음 13비트는 논리 샤드 ID를 나타내고, 이를 통해 데이터를 여러 샤드에 분산시킬 수 있다.
- **시퀀스 번호**: 마지막 10비트는 시퀀스 번호로, 밀리초마다 초기화되며 샤드당 밀리초당 최대 1024개의 고유 ID를 생성할 수 있다.

#### 4. PostgreSQL 기준 키 생성 쿼리



{% raw %}
```sql
CREATE OR REPLACE FUNCTION next_id(OUT result bigint) AS $$
DECLARE
    our_epoch bigint := 1314220021721; -- 특정 기준 시점(예: 2011년 9월 9일)
    seq_id bigint;
    now_millis bigint;
    shard_id int := 5; -- 샤드 ID 예시 (실제 상황에서는 동적으로 정해야 한다)
BEGIN
    -- 시퀀스의 다음 값을 1024로 나눈 나머지를 가져올 수 있다.
    SELECT nextval('table_id_seq') % 1024 INTO seq_id;

    -- 현재 시간을 밀리초 단위로 가져올 수 있다.
    SELECT FLOOR(EXTRACT(EPOCH FROM clock_timestamp()) * 1000) INTO now_millis;

    -- 타임스탬프를 23비트(64 - 41)만큼 왼쪽으로 시프트할 수 있다.
    result := (now_millis - our_epoch) << 23;

    -- 샤드 ID를 10비트만큼 왼쪽으로 시프트해서 추가할 수 있다.
    result := result | (shard_id << 10);

    -- 시퀀스 번호를 추가할 수 있다.
    result := result | (seq_id);
END;
$$ LANGUAGE PLPGSQL;
```
{% endraw %}



#### 5. 사용자 정의 ID로 테이블 생성


콘텐츠를 저장할 테이블을 만들 때, 기본 키 값으로 사용자 정의 ID 생성 함수를 사용할 수 있다:



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



#### 요약

- **타임스탬프 (41비트)**: ID가 시간에 따라 정렬될 수 있게 할 수 있다.
- **샤드 ID (13비트)**: 데이터를 논리적 샤드에 분배할 수 있다.
- **시퀀스 번호 (10비트)**: 샤드당 밀리초당 여러 개의 고유 ID를 생성할 수 있다.

참고 : [https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c](https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c)

