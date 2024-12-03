---
layout: post
date: 2024-12-03
title: "[Blind 75] Reverse Linked List"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/reverse-linked-list](https://leetcode.com/problems/reverse-linked-list/)


tail이라는 null 값을 만들어주고 현재 노드의 다음 노드를 임시로 저장한다. 현재 노드의 다음을 tail로 연결해주고 현재 노드를 tail로 바꿔준다. 그리고 임시저장했던 노드를 현재 노드로 선언해준다.  


#### 풀이1



{% raw %}
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        
        ListNode tail = null;
        ListNode current = head;

        while(current != null){
            ListNode temp = current.next;
            current.next = tail;
            tail = current;
            current = temp;
        }

        return tail;
    }
}
```
{% endraw %}


