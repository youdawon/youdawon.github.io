---
layout: post
date: 2024-11-30
title: "[Blind 75] Invert Binary Tree"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/invert-binary-tree](https://leetcode.com/problems/invert-binary-tree/)


이 문제는 root.left와 root.right의 위치를 서로 바꾼 후 바꾼 root.left의 자식노드와 root.right의 자식노드를 null 이 나올때까지 바꿔주는 식으로 코드를 작성하였다. 


시간 복잡도는 모든 노드를 방문하기 때문에 O(N)이다. 



{% raw %}
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {    
        
        invert(root);

        return root;
    }

    public void invert(TreeNode root){

        if(root == null){
            return;
        }
        
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;

        invert(root.left);
        invert(root.right);         
    }
}
```
{% endraw %}


