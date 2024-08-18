---
layout: post
date: 2024-08-18
title: "Kruskal Algorithm"
tags: [Algorithm, Graph, Krustal, ]
categories: [Algorithm, graph, ]
---


Kruskal’s Algorithm은 그래프에서 최소 신장 트리(MST)를 찾는 알고리즘이다. 최소 신장 트리는 그래프의 모든 정점을 포함하면서, 간선들의 가중치 합이 최소가 되는 트리이다.


#### Kruskal’s Algorithm 개요

1. **간선의 가중치 기준 정렬**:
	- 모든 간선을 가중치의 오름차순으로 정렬한다. 가장 작은 가중치의 간선부터 트리에 추가한다.
2. **트리에 간선 추가**:
	- 간선을 하나씩 선택하여 트리에 추가한다. 사이클이 생기는 간선은 제외한다.
3. **사이클 검출 및 Union-Find 사용**:
	- 사이클을 검출하기 위해 Union-Find 자료구조를 사용한다. 두 정점이 같은 집합에 속해 있으면 그 간선을 추가하지 않는다.
4. **완성 조건**:
	- 간선의 수가 `n-1`개가 되면, 즉 트리에 `n`개의 정점과 `n-1`개의 간선이 모두 포함되면 알고리즘을 종료한다.

#### Kruskal’s Algorithm의 시간 복잡도

- 시간 복잡도는 `O(E log E)` 또는 `O(E log V)`이다. 여기서 `E`는 간선의 수, `V`는 정점의 수이다. 간선 정렬이 가장 많은 시간을 소요한다.

#### Kruskal’s Algorithm 구현 (Python)



{% raw %}
```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [1] * n

    def find(self, u):
        if self.parent[u] != u:
            self.parent[u] = self.find(self.parent[u])
        return self.parent[u]

    def union(self, u, v):
        root_u = self.find(u)
        root_v = self.find(v)

        if root_u != root_v:
            if self.rank[root_u] > self.rank[root_v]:
                self.parent[root_v] = root_u
            elif self.rank[root_u] < self.rank[root_v]:
                self.parent[root_u] = root_v
            else:
                self.parent[root_v] = root_u
                self.rank[root_u] += 1

def kruskal(n, edges):
    mst = []
    total_weight = 0

    edges.sort(key=lambda x: x[2])

    uf = UnionFind(n)

    for u, v, weight in edges:
        if uf.find(u) != uf.find(v):
            uf.union(u, v)
            mst.append((u, v, weight))
            total_weight += weight

            if len(mst) == n - 1:
                break

    return mst, total_weight

n = 4  # 정점의 수
edges = [
    (0, 1, 10),
    (0, 2, 6),
    (0, 3, 5),
    (1, 3, 15),
    (2, 3, 4)
]

mst, total_weight = kruskal(n, edges)
print("Minimum Spanning Tree:", mst)
print("Total Weight:", total_weight)
```
{% endraw %}



#### 설명:

1. **Union-Find 클래스**:
	- `find` 함수: 주어진 노드가 속한 집합의 루트를 찾는다. 경로 압축(Path Compression)을 사용하여 효율성을 높인다.
	- `union` 함수: 두 노드가 속한 집합을 병합한다. 랭크 기반 합치기(Union by Rank)를 사용하여 트리의 높이를 최소화한다.
2. **Kruskal’s Algorithm**:
	- 간선 정렬: 모든 간선을 가중치 기준으로 정렬한다.
	- MST 구성: 간선을 하나씩 선택하여 MST에 추가한다. 두 정점이 같은 집합에 속하지 않는 경우에만 간선을 추가한다.
	- MST 반환: 간선의 리스트와 총 가중치를 반환한다.

#### 출력:



{% raw %}
```text
Minimum Spanning Tree: [(2, 3, 4), (0, 3, 5), (0, 1, 10)]
Total Weight: 19
```
{% endraw %}



#### Kruskal’s Algorithm의 사용 사례

- 네트워크 연결 비용 최소화
- 클러스터링에서의 연결선 최소화
- 그래프에서 최소 신장 트리를 찾는 모든 문제에 사용 가능

Kruskal’s Algorithm은 간선이 많은 밀집 그래프에서 효율적이다.

