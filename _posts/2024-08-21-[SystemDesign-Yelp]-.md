---
layout: post
date: 2024-08-21
title: "[SystemDesign-Yelp] "
tags: [System Design, Yelp, ]
categories: [System Design, Problems, ]
---


각 장소는 위도와 경도를 가지고 있으며, 검색 속도를 높이기 위해 그리드로 장소를 나누어 저장할 것이다. 그러나 장소들이 고르게 분포되어 있지 않기 때문에, 어떤 그리드에는 많은 장소가 몰려있고, 어떤 그리드에는 거의 없을 수 있다. 이러한 문제는 어떻게 해결할 수 있을까?


#### 해결책: 동적 그리드 크기와 쿼드트리 사용

1. **그리드 크기 조정**:
	- **목표**: 하나의 그리드에 500개 이상의 장소가 들어가지 않도록 한다.
	- **방법**: 만약 어떤 그리드에 500개 이상의 장소가 있다면, 이 그리드를 네 개의 작은 그리드로 나누고, 장소들을 새로 나뉜 그리드에 분배한다. 이렇게 하면 장소가 많은 도심 지역은 작은 그리드로 세분화되고, 장소가 적은 지역은 큰 그리드로 유지된다.
2. **데이터 구조: 쿼드트리(QuadTree)**
	- **쿼드트리란?**: 쿼드트리는 각 노드가 네 개의 자식을 가지는 트리 구조이다. 이 구조는 공간을 효율적으로 분할하고, 검색 속도를 높이는 데 사용된다.
	- **동작 방식**:
		- 처음에는 전 세계를 하나의 큰 그리드로 나타낸다.
		- 이 그리드에 500개 이상의 장소가 있으면 네 개의 노드로 나누고 장소를 분배한다.
		- 이 과정을 반복하여, 모든 그리드가 500개 이하의 장소만 포함하도록 한다.
		- 최종적으로, 각 리프 노드(더 이상 나눌 수 없는 그리드)는 그 그리드 내의 장소 목록을 유지하게 된다.
3. **이웃 그리드를 찾는 방법**
	- **이중 연결 리스트(Doubly Linked List) 사용**:
		- **리프 노드 간 연결**: 쿼드트리에서 리프 노드만 장소 목록을 포함하므로, 모든 리프 노드를 이중 연결 리스트로 연결한다.
		- **검색 방법**: 이 연결 리스트를 통해 이웃하는 리프 노드 간에 앞으로 또는 뒤로 이동하면서 원하는 위치를 가진 장소를 찾는다. 이 방법은 특정 그리드에서 가까운 다른 그리드를 빠르게 검색할 수 있도록 도와준다.
	- **부모 노드를 이용한 이웃 그리드 찾기**:
		- **부모 포인터 사용**: 각 노드에 부모 노드를 가리키는 포인터를 추가한다.
		- **형제 노드 접근**: 부모 노드는 모든 자식 노드에 대한 포인터를 가지고 있으므로, 이를 통해 같은 부모를 공유하는 형제 노드(이웃 그리드)에 쉽게 접근할 수 있다.
		- **검색 범위 확장**: 특정 노드의 이웃을 찾기 위해 부모 노드를 따라 올라가면서 다른 형제 노드를 확인하거나, 이웃하는 부모 노드의 자식들까지 검색 범위를 확장할 수 있다.
4. **검색과 삽입**
	- **검색**: 사용자의 위치를 기반으로 해당 위치에 해당하는 그리드를 찾는다. 이 그리드에 충분한 장소가 있으면 결과를 반환하고, 그렇지 않으면 이웃 그리드를 찾아 검색 범위를 확장한다.
	- **삽입**: 새로운 장소가 추가될 때, 이 장소가 들어갈 그리드를 찾아서 데이터를 추가합니다. 만약 이 그리드가 이미 500개의 장소를 포함하고 있다면, 이 그리드를 네 개로 나누고 장소들을 새로 나뉜 그리드에 분배한다.

#### 쿼드 트리 사용 시 시스템 흐름 

1. **쿼드트리 탐색**
- 사용자가 특정 위치와 반경 `D`를 지정하여 검색 요청을 하면, 쿼드트리는 해당 위치를 포함하는 노드를 찾아내고, 그 노드 내의 하위 노드들(4구역으로 나뉘는 경우)을 탐색한다.
- 쿼드트리는 공간을 분할하여 각 노드에 해당 위치의 **LocationID** 리스트를 보유하고 있다. 탐색 과정에서, 지정된 반경 `D` 내에 있는 모든 관련 노드(및 서브노드)를 탐색한다.
1. **LocationID 수집**
- 탐색된 노드들에서 **LocationID**들을 수집한다. 이 **LocationID**들은 해당 노드와 서브노드에 속한 장소들을 고유하게 식별한다.
- 예를 들어, 특정 노드가 4개의 하위 구역으로 나뉘어 있다면, 이 네 구역에 있는 모든 **LocationID**를 수집한다.

#### 3. **Place 테이블 조회**

- 수집된 **LocationID**들을 사용하여 **Place** 테이블에서 필요한 데이터를 조회한다.
- SQL 쿼리 예시:

	
{% raw %}
```sql
	sql코드 복사
	SELECT * FROM Place WHERE LocationID IN (location_id1, location_id2, location_id3, ...);
```
{% endraw %}


- 이 쿼리는 쿼드트리에서 검색된 모든 **LocationID**에 해당하는 장소 데이터를 **Place** 테이블에서 조회한다.

#### 4. **결과 반환**

- 조회된 장소 데이터는 사용자에게 반환된다. 이 데이터는 사용자가 지정한 위치와 반경 `D` 내에 있는 장소들이다.
