---
layout: post
date: 2024-08-17
title: "[Algorithm] Floyd-Warshall Algorithm"
tags: [Algorithm, Graph, Floyd Warshall, ]
categories: [Algorithm, graph, ]
---


Floyd-Warshall 알고리즘은 모든 쌍의 최단 경로를 찾기 위한 알고리즘입니다. 이 알고리즘은 가중치가 있는 그래프에서 모든 노드 쌍 간의 최단 경로를 계산할 수 있으며, 음수 가중치를 가진 엣트도 처리할 수 있지만, 음수 사이클(사이클의 가중치 합이 음수인 경우)이 있을 경우에는 정확하게 동작하지 않습니다.


#### Floyd-Warshall 알고리즘의 특징

- **모든 쌍의 최단 경로**: 그래프의 모든 노드 쌍 간의 최단 경로를 계산합니다.
- **음수 가중치 처리 가능**: 음수 가중치를 가진 엣트가 있는 그래프에서도 동작합니다. 그러나 음수 사이클이 존재하면 정확한 결과를 제공하지 않습니다.
- **시간 복잡도**: \( O(V^3) \), 여기서 \( V \)는 노드의 수입니다.
- **공간 복잡도**: \( O(V^2) \), 최단 경로 거리를 저장하기 위해 2차원 행렬이 필요합니다.

#### Floyd-Warshall 알고리즘 설명

1. **초기화**:
	- 거리 행렬 `dist`를 생성하여 `dist[i][j]`가 노드 `i`에서 노드 `j`까지의 최단 거리임을 나타냅니다. 이 행렬은 다음으로 초기화합니다:
		- `0`으로 설정하여 `dist[i][i]` (자기 자신까지의 거리).
		- 직접 연결된 엣트의 가중치로 설정합니다.
		- 엣트가 없는 노드 쌍에 대해서는 `∞`(무한대)로 설정합니다.
2. **완화(Relaxation)**:
	- 모든 가능한 중간 노드 `k`를 고려하여, 노드 쌍 `i`와 `j` 간의 최단 거리를 업데이트합니다. `k`를 경유하는 경로가 더 짧다면 `dist[i][j]`를 업데이트합니다.
3. **음수 사이클 탐지**:
	- 최단 경로 계산 후, 거리 행렬의 대각선(`dist[i][i]`)을 검사하여 음수 값이 있는지 확인합니다. 음수 값이 있으면 음수 사이클이 존재함을 의미합니다.

#### 알고리즘 의사 코드



{% raw %}
```python
def floyd_warshall(graph):
    # graph는 그래프의 엣트 가중치를 포함하는 딕셔너리
    V = len(graph)
    # 거리 행렬 초기화
    dist = [[float('inf')] * V for _ in range(V)]
    for u in range(V):
        for v in range(V):
            if u == v:
                dist[u][v] = 0
            elif (u, v) in graph:
                dist[u][v] = graph[u][v]

    # Floyd-Warshall 알고리즘
    for k in range(V):
        for i in range(V):
            for j in range(V):
                if dist[i][k] + dist[k][j] < dist[i][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]

    # 음수 사이클 확인
    for i in range(V):
        if dist[i][i] < 0:
            print("그래프에 음수 사이클이 존재합니다.")
            return None

    return dist
```
{% endraw %}



#### Python 코드 예제



{% raw %}
```python
def floyd_warshall(graph):
    # graph는 {i: {j: 가중치, ...}, ...} 형태의 딕셔너리
    V = len(graph)
    # 거리 행렬 초기화
    dist = [[float('inf')] * V for _ in range(V)]

    for u in graph:
        for v in graph[u]:
            dist[u][v] = graph[u][v]
        dist[u][u] = 0  # 자기 자신까지의 거리는 0

    # Floyd-Warshall 알고리즘
    for k in range(V):
        for i in range(V):
            for j in range(V):
                if dist[i][k] < float('inf') and dist[k][j] < float('inf'):
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])

    # 음수 사이클 확인
    for i in range(V):
        if dist[i][i] < 0:
            print("그래프에 음수 사이클이 존재합니다.")
            return None

    return dist
```
{% endraw %}



#### 핵심 포인트

- **초기화**: 직접 연결된 엣트의 가중치와 자기 자신까지의 거리(0)로 거리 행렬을 초기화합니다.
- **완화**: 각 노드를 중간 노드로 고려하여 최단 거리를 업데이트합니다.
- **음수 사이클 탐지**: 거리 행렬의 대각선을 검사하여 음수 사이클의 존재 여부를 확인합니다.

#### 사용 사례

- **모든 쌍의 최단 경로**: 모든 노드 쌍 간의 최단 경로가 필요한 경우 사용합니다.
- **그래프 분석**: 음수 가중치를 처리할 수 있는 그래프의 속성 분석에 유용합니다.

#### 제한 사항

- **시간 복잡도**: \( O(V^3) \)로 매우 큰 그래프에는 비효율적일 수 있습니다.
- **음수 사이클**: 음수 사이클이 존재하면 알고리즘의 결과가 정확하지 않습니다.

Floyd-Warshall 알고리즘은 그래프 이론의 기본 알고리즘으로, 모든 쌍의 최단 경로를 찾는 데 유용합니다.

