---
layout: post
date: 2024-08-18
title: "[Algorithm] Topological Sorting"
tags: [Algorithm, Graph, Topological Sorting, ]
categories: [Algorithm, graph, ]
---


**위상 정렬(Topological Sorting)**은 방향성 비순환 그래프(DAG, Directed Acyclic Graph)의 정점들을 정렬하는 방법이다. 이 정렬은 그래프의 모든 간선 (u, v)에 대해, 정점 u가 v 앞에 오도록 한다. 위상 정렬은 주로 그래프에서 작업의 의존 관계를 나타낼 때 사용되며, 작업을 순서대로 나열하는 데 유용하다.


#### **위상 정렬의 특징**

1. **DAG(Directed Acyclic Graph)에서만 가능**:
	- 위상 정렬은 반드시 방향성 비순환 그래프에서만 수행할 수 있다. 순환(Cycle)이 있는 그래프에서는 위상 정렬을 수행할 수 없다.
2. **정렬의 유일성**:
	- DAG의 경우, 위상 정렬은 항상 존재하지만, 유일하지 않을 수 있다. 그래프의 구조에 따라 여러 가지 정렬이 가능할 수 있다.

#### **위상 정렬의 알고리즘**

1. **DFS(깊이 우선 탐색)를 이용한 위상 정렬**:
	- 각 정점에 대해 DFS를 수행하여, 모든 인접 정점을 처리한 후에 현재 정점을 스택에 삽입한다. DFS가 끝난 후 스택에 담긴 정점을 역순으로 출력하면 위상 정렬이 된다.

	**알고리즘**:

	- 그래프의 모든 정점에 대해 DFS를 수행한다.
	- DFS를 수행하는 동안, 모든 인접 정점을 먼저 방문하고, 현재 정점을 스택에 추가한다.
	- 모든 정점에 대해 DFS가 완료되면, 스택에서 정점을 하나씩 꺼내어 출력한다.

	**시간 복잡도**: `O(V + E)` (V는 정점의 수, E는 간선의 수)

2. **Kahn's Algorithm (BFS 기반의 위상 정렬)**:
	- 위상 정렬을 BFS 방식으로 구현한 알고리즘으로, 진입 차수(indegree)가 0인 정점을 먼저 처리한다.

	**알고리즘**:

	- 그래프의 모든 정점의 진입 차수(indegree)를 계산한다.
	- 진입 차수가 0인 정점을 큐에 삽입한다.
	- 큐에서 정점을 하나씩 꺼내고, 해당 정점의 인접 정점들의 진입 차수를 1씩 감소시킨다.
	- 감소된 결과 진입 차수가 0이 된 정점을 큐에 삽입한다.
	- 큐가 빌 때까지 반복한다.
	- 모든 정점을 큐에서 꺼낸 순서대로 출력하면 위상 정렬이 된다.

	**시간 복잡도**: `O(V + E)`


#### **위상 정렬의 응용**

- **작업 스케줄링**:
	- 작업들 간의 의존성을 나타내는 DAG에서 작업을 올바른 순서로 수행해야 하는 경우에 위상 정렬이 사용된다. 예를 들어, 특정 과목을 수강하기 전에 다른 과목을 먼저 들어야 하는 경우 수강 순서를 결정할 때 위상 정렬이 사용될 수 있다.
- **컴파일러에서의 사용**:
	- 소스 코드에서 함수나 클래스 간의 의존성을 분석하여 컴파일 순서를 정할 때 위상 정렬이 사용된다.
- **프로젝트 관리**:
	- 프로젝트 관리에서 작업 간의 종속성을 분석하고 작업을 순차적으로 수행할 수 있도록 스케줄링하는 데 위상 정렬이 사용된다.

#### **위상 정렬의 구현 예시 (Python)**


#### **DFS를 이용한 위상 정렬**



{% raw %}
```python
from collections import defaultdict

def dfs(v, visited, stack, graph):
    visited[v] = True
    for neighbor in graph[v]:
        if not visited[neighbor]:
            dfs(neighbor, visited, stack, graph)
    stack.append(v)

def topological_sort_dfs(vertices, edges):
    graph = defaultdict(list)
    for u, v in edges:
        graph[u].append(v)

    visited = [False] * vertices
    stack = []

    for i in range(vertices):
        if not visited[i]:
            dfs(i, visited, stack, graph)

    return stack[::-1]  # Stack의 역순

## 예제 사용
vertices = 6
edges = [(5, 2), (5, 0), (4, 0), (4, 1), (2, 3), (3, 1)]
print(topological_sort_dfs(vertices, edges))
```
{% endraw %}



#### **Kahn's Algorithm (BFS 기반 위상 정렬)**



{% raw %}
```python
from collections import defaultdict, deque

def topological_sort_kahn(vertices, edges):
    graph = defaultdict(list)
    indegree = [0] * vertices

    for u, v in edges:
        graph[u].append(v)
        indegree[v] += 1

    queue = deque([i for i in range(vertices) if indegree[i] == 0])
    topo_order = []

    while queue:
        node = queue.popleft()
        topo_order.append(node)

        for neighbor in graph[node]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)

    if len(topo_order) == vertices:
        return topo_order
    else:
        return []  # 사이클이 있는 경우

## 예제 사용
vertices = 6
edges = [(5, 2), (5, 0), (4, 0), (4, 1), (2, 3), (3, 1)]
print(topological_sort_kahn(vertices, edges))
```
{% endraw %}


