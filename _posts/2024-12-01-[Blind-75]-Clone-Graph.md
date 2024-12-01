---
layout: post
date: 2024-12-01
title: "[Blind 75] Clone Graph"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


BFS를 이용하여 풀었다. 그래프는 BFS랑 DFS만 잘 이해하면 푸는데 어려움은 없어보인다. 이미 방문한 노드는 또 방문하지 않도록 HashMap을 이용하였다. 노드의  이웃들이 HashMap에 있으면 이미 방문했으므로 다시 방문할 필요가 없이 edge만 이어준다. 방문하지 않은 노드는 새 노드들 만들어준 후 queue에 넣어서 이웃과의 edge를 연결하도록 처리한다.\


#### 풀이 1



{% raw %}
```java
class Solution {
    public Node cloneGraph(Node node) {

        if(node == null){
            return null;
        }
        
        Queue<Node> queue = new LinkedList<>();
        queue.offer(node);

        Map<Node, Node> map = new HashMap<>();        
        map.put(node, new Node(node.val)); 

        while(!queue.isEmpty()){
            Node current = queue.poll();
            Node newNode = map.get(current);

            for(Node neighbor : current.neighbors){
                if(!map.containsKey(neighbor)){
                    map.put(neighbor, new Node(neighbor.val));
                    queue.offer(neighbor);                                                      
                }
                newNode.neighbors.add(map.get(neighbor));
            }
        }
        return map.get(node);
    }
}
```
{% endraw %}


