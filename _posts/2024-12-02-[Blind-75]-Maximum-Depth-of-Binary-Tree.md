---
layout: post
date: 2024-12-02
title: "[Blind 75] Maximum Depth of Binary Tree"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/maximum-depth-of-binary-tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)


이 문제는 트리의 최대 깊이를 구하는 것이다. 나는 이 문제가 잠깐 헷갈려서 leaf node까지의 길이로 착각했다. depth는 각 가장 깊은 leaf node까지의 레벨이 몇개인지를 구하는 것이다. 


#### 풀이1



{% raw %}
```java
class Solution {

    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }

        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```
{% endraw %}


