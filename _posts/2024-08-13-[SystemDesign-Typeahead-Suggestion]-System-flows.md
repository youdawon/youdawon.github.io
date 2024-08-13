---
layout: post
date: 2024-08-13
title: "[SystemDesign-Typeahead Suggestion] System flows"
tags: [SystemDesign, Architecture, Typeahead Suggestion, ]
categories: [SystemDesign, Problems, Typeahead Suggestion, ]
---


### 1. **사용자 요청 처리**

- **사용자(User) 요청**: 사용자가 검색어를 입력하면, 이 요청이 **Load Balancer** 또는 **API Gateway**로 전달한다.
- **로드 밸런싱 (Load Balancer, API Gateway)**: 해시 기반 파티셔닝(Hash based Partitioning)을 통해 검색어 요청을 적절한 서버로 분산 처리한다. 이를 통해 동일한 검색어가 동일한 서버로 라우팅되어 캐싱 효율을 높인다.

#### 2. **검색 API와 데이터 저장**

- **검색 API (Search API)**: 특정 서버로 전달된 요청은 **Search API**에 의해 처리되며, Redis에 저장된 Trie 구조를 사용해 해당 검색어의 추천 결과를 찾아 반환한다.
- **데이터 저장 (Terms Storage - Redis)**:
	- **Trie 구조로 저장**: 각 문자별로 데이터를 Trie 구조로 Redis에 저장해, 검색어 추천의 기본 데이터를 제공한다.

#### 3. **로그 수집 및 저장 (Log Storage)**

- **로그 수집**: 사용자 요청과 관련된 모든 이벤트(예: 검색어 입력)를 기록하여 로그 데이터를 생성한다.
- **로그 저장 (Log Storage)**: 수집된 로그는 **Log Storage**에 저장돼. 이 저장소는 로그 데이터를 일관되게 보관하며, 나중에 배치 작업에서 이를 처리할 수 있도록 한다.

#### 4. **배치 작업 (Batch Job)에서의 MapReduce 처리**

- **로그 데이터 가져오기**: 배치 작업이 시작되면, **Log Storage**에 저장된 로그 데이터를 가져와 분석을 시작한다.
- **MapReduce 작업**:
	- **Map 단계**: 로그 데이터를 처리하여 각 검색어를 키로, 해당 검색어의 발생 횟수를 값으로 매핑해. 이 단계에서 각 로그 항목은 특정 검색어에 대한 정보로 변환된다.
	- **Reduce 단계**: 동일한 키(검색어)를 가진 데이터를 그룹화하여 합산하거나, 상위 N개의 검색어를 선정한다.
- **Trie 및 Top N 갱신**: MapReduce 작업의 결과를 바탕으로 Redis에 저장된 Trie 구조를 갱신하고, 상위 검색어 리스트를 최신화한다.

#### 5. **Top N 동기화 및 추천**

- **Top N 동기화**: 배치 작업 후, 갱신된 Top N 검색어 목록을 Redis에 저장해. 이를 통해 실시간 검색어 추천 기능에서 항상 최신 데이터를 사용할 수 있다.

#### 6. **Redis 복제 및 읽기-쓰기 분리**

- **쓰기 전용 Redis**: 배치 작업의 결과로 생성된 데이터는 주로 쓰기 전용 Redis 인스턴스에 저장된다.
- **읽기 전용 Redis**: 쓰기 전용 Redis 인스턴스에서 업데이트된 데이터는 읽기 전용 Redis로 복제(Replication)하며 읽기 전용 Redis는 주로 검색 API에서 사용되며, 사용자 요청에 대한 빠른 응답을 제공한다.
- **데이터 일관성 유지**: 쓰기 작업이 완료된 후, 데이터는 읽기 전용 Redis로 동기화되어, 실시간으로 최신 데이터를 조회할 수 있게 한다.

![0](/assets/img/2024-08-13-[SystemDesign-Typeahead-Suggestion]-System-flows.md/0.png)

