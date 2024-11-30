---
layout: post
date: 2024-11-30
title: "[Blind 75] Kth Smallest Element In a Bst"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/kth-smallest-element-in-a-bst](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)


이 문제는 Binary Search Tree에서 k번째로 작은 수를 구하는 문제이다. Binary Search Tree는 루트 중심으로 왼쪽은 무조건 루트의 값보다 작은 수들로 이루어져 있고 오른쪽은 루트의 값보다 큰 수들로 이루어져있기 때문에 이 공식을 생각해서 풀어보았다. 


루트가 null이 되는 점까지 이동 후 count를 세어 k와 같은 값이 나올경우 해당 값을 return한다. 이 방법은 중위 순회(Inorder)를 사용한다. 


중위 순회(Inorder Traversal) : left → root → right 


전위 순회(Preorder Traversal) : root → left → right


후위 순회(Postorder Traversal) : left → right → root



{% raw %}
```java
class Solution {

    private int count = 0;
    private int result = 0;

    public int kthSmallest(TreeNode root, int k) {

        dfs(root, k);

        return result;
    }

    public void dfs(TreeNode root, int k){

        if(root == null){
            return;
        }
        dfs(root.left, k);
        count++;        
        if(k == count){
            result = root.val;
        }
        dfs(root.right, k);
    }
}
```
{% endraw %}


