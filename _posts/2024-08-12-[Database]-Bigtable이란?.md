---
layout: post
date: 2024-08-12
title: "[Database] Bigtable이란?"
tags: [Architecture, Dabatabse, ]
categories: [Database, ]
---


**Google Bigtable**은 Google이 개발한 분산형 NoSQL 데이터베이스로, 대규모의 구조화된 데이터를 관리하고 빠르게 처리하기 위해 설계된 시스템이다. Bigtable은 특히 **대용량 데이터**를 **고성능**으로 처리하는 데 최적화되어 있으며, **수평적 확장성**을 제공해, 수십억 개의 행(row)과 수백만 개의 열(column)을 효율적으로 관리할 수 있다.


#### 주요 특징:

1. **대규모 데이터 처리**:
	- Bigtable은 테라바이트에서 페타바이트 규모의 데이터를 관리할 수 있다. 대규모 데이터셋을 처리하는 데 필요한 성능과 확장성을 제공한다.
2. **테이블 구조**:
	- 데이터는 행(row)과 열(column)로 구성된 테이블 형식으로 저장한다. 각 행은 고유한 행 키(row key)로 식별되고, 열은 컬럼 패밀리(column family)로 그룹화된다. 이 구조는 데이터를 효율적으로 저장하고 검색할 수 있게 한다.
3. **높은 확장성**:
	- Bigtable은 수평적 확장을 지원한다. 즉, 데이터를 저장하는 노드를 추가하면 성능이 선형적으로 확장될 수 있다. 이를 통해 급격히 증가하는 데이터도 효율적으로 처리할 수 있다.
4. **고성능**:
	- Bigtable은 초당 수백만 개의 읽기/쓰기 작업을 처리할 수 있는 성능을 제공한다. 이를 통해 실시간 분석, 검색 엔진, 광고 시스템 등에서 사용되는 대규모 데이터를 빠르게 처리할 수 있다.
5. **유연한 데이터 모델링**:
	- 데이터는 구조화된 테이블 형식으로 저장되지만, 스키마리스 방식이기 때문에 유연한 데이터 모델링이 가능하다. 필요한 경우 새로운 열을 추가하거나 삭제하는 것이 매우 쉽다.
6. **사용 사례**:
	- Google 내부에서는 검색 색인 저장, Google Earth의 이미지 저장, Google Analytics 데이터 처리 등 다양한 대규모 애플리케이션에서 Bigtable을 사용한다. 외부에서는 Apache HBase와 유사한 기술로 널리 사용되며, 특히 대규모 데이터 분석, IoT, 실시간 데이터 처리에 적합하다.
7. **Google Cloud Bigtable**:
	- Google은 Bigtable 기술을 기반으로 한 **Google Cloud Bigtable**이라는 클라우드 서비스도 제공한다. 이는 Google Cloud Platform(GCP)에서 관리형 서비스로 제공되며, 사용자가 인프라를 관리하지 않아도 대규모 데이터를 처리할 수 있도록 도와준다.
