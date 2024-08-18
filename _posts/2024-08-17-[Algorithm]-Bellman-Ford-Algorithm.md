---
layout: post
date: 2024-08-17
title: "[Algorithm] Bellman-Ford Algorithm"
tags: [Algorithm, ]
categories: [Algorithm, graph, ]
---


벨만-포드 알고리즘(Bellman-Ford Algorithm)은 단일 출발점에서 모든 정점까지의 최단 경로를 찾기 위한 알고리즘으로, 음수 가중치의 엣지가 있는 그래프에서도 동작할 수 있다. 이 알고리즘은 음수 사이클을 탐지할 수도 있다.


#### 벨만-포드 알고리즘의 특징

- **음수 가중치**: 음수 가중치를 허용하지만, 음수 사이클이 있는 경우 최단 경로를 정의할 수 없다.
- **시간 복잡도**: ( O(V times E) ), 여기서 ( V )는 정점의 수, ( E )는 엣지의 수이다.

#### 벨만-포드 알고리즘의 작동 원리

1. **초기화**:
	- 출발 정점의 거리 값을 0으로 설정하고, 나머지 정점들의 거리 값을 무한대(`float('inf')`)로 설정한다.
2. **완화(Relaxation)**:
	- 그래프의 모든 엣지에 대해 반복하여 최단 거리를 업데이트한다. 이 과정을 V-1번 반복한다. 즉, 모든 정점의 거리 값을 한 번씩 업데이트할 기회를 준다.
3. **음수 사이클 탐지**:
	- 추가적인 반복을 통해, 거리가 여전히 줄어들 수 있는 엣지가 있는지를 확인하여 음수 사이클을 탐지한다.

#### 파이썬으로 벨만-포드 알고리즘 구현



{% raw %}
```python
def bellman_ford(graph, start):
    # 그래프는 {정점: [(인접 정점, 가중치), ...]} 형태로 가정
    # 거리 초기화
    dist = {node: float('inf') for node in graph}
    dist[start] = 0

    # 모든 엣지에 대해 V-1번 완화
    for _ in range(len(graph) - 1):
        for u in graph:
            for v, weight in graph[u]:
                if dist[u] != float('inf') and dist[u] + weight < dist[v]:
                    dist[v] = dist[u] + weight

    # 음수 사이클 검사
    for u in graph:
        for v, weight in graph[u]:
            if dist[u] != float('inf') and dist[u] + weight < dist[v]:
                print("그래프에 음수 사이클이 존재합니다.")
                return None

    return dist
```
{% endraw %}



#### 코드 설명

1. **거리 초기화**:
	- 출발 정점의 거리를 0으로 설정하고, 나머지 정점들은 무한대로 설정한다.
2. **완화 과정**:
	- 모든 엣지에 대해 V-1번 반복하면서, 현재 최단 거리보다 더 짧은 경로가 있으면 거리를 업데이트한다.
3. **음수 사이클 탐지**:
	- V번 반복하여 음수 사이클이 있는지 확인한다. 만약 거리를 여전히 줄일 수 있는 엣지가 있다면, 그래프에 음수 사이클이 존재한다는 의미이다.

#### 벨만-포드 알고리즘의 시간 복잡도

- **시간 복잡도**: ( O(V times E) )
	- **V**: 정점의 수
	- **E**: 엣지의 수

벨만-포드 알고리즘은 특히 음수 가중치가 있는 그래프에서 유용하며, 다익스트라 알고리즘과 달리 음수 가중치를 허용한다는 점에서 차별화된다. 그러나 다익스트라 알고리즘보다 시간이 더 오래 걸리는 경우가 많다.

