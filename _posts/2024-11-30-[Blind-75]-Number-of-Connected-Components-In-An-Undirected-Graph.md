---
layout: post
date: 2024-11-30
title: "[Blind 75] Number of Connected Components In An Undirected Graph"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)


Example 1:


Input: n = 5 and edges = [[0, 1], [1, 2], [3, 4]]



{% raw %}
```text
 0          3
 |          |
 1 --- 2    4
```
{% endraw %}



Output: 2
Example 2:


Input: n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]]



{% raw %}
```text
 0           4
 |           |
 1 --- 2 --- 3
```
{% endraw %}



Output:  1


위 문제는 연결된 컴포넌트의 개수를 구하는 문제이다. 무방향 그래프이기 때문에 그래프 생성 시 양쪽에 모두 vertex를 추가해주어야 한다.


verext의 개수는 5개이기 때문에 0부터 4까지 루프를 돌면서 각 vertex를 방문한다. 이미 방문한 vertex은 방문 처리를 해서 재방문하지 않도록 한다. 이미 방문한 vertex는 다른 vertex와 연결되어있다는 의미이므로 재방문을 할 필요가 없다. 이렇게 bfs을 이용해서 로직을 수행하게 되면 각각 연결되어 있는 컴포넌트가 2개라는 것을 알 수 있다. 



{% raw %}
```java
public class leetcode323{
	public static void main(String[] args) {

		int n = 5;
//		int[][] edges = {{0, 1}, {1, 2}, {3, 4}};
		 int[][] edges = {{0, 1}, {1, 2},{2, 3}, {3, 4}};

		List<List<Integer>> graph = new ArrayList<>();

		for (int i = 0; i < n; i++) {
			graph.add(new ArrayList<>());
		}

		for (int[] edge : edges) {
			graph.get(edge[0]).add(edge[1]);
			graph.get(edge[1]).add(edge[0]);
		}

		boolean[] visited = new boolean[n];
		int count = 0;

		for (int i = 0; i < n; i++) {
			if (visited[i] == false) {
				bfs(graph, i, visited);
				count++;
			}
		}

		System.out.println(count);
	}

	public static void bfs(List<List<Integer>> graph, int index, boolean[] visited){
		visited[index] = true;

		for(int neighbor : graph.get(index)){
			if(visited[neighbor] == true){
				continue;
			}
			bfs(graph, neighbor, visited);
		}
	}
}
```
{% endraw %}


