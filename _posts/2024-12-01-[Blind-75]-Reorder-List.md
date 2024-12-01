---
layout: post
date: 2024-12-01
title: "[Blind 75] Reorder List"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/reorder-list](https://leetcode.com/problems/reorder-list/)


이 문제는 fast & slow 포인터를 사용해야한다. fast는 두번 이동하고 slow는 한번 이동해서 리스트의 중간값을 구한다. 중간 이후의 노드들의 순서를 반대로 바꿔준다. 


중간 이전의 노드와 중간 이후의 노드를 각각 순서대로 번갈아서 붙여주면 Reorder List가 완성된다. 



{% raw %}
```java
class Solution {
    public void reorderList(ListNode head) {
        
        ListNode fast = head;
        ListNode slow = head;

        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode tail = null;
        ListNode current = slow.next;
        slow.next = null;

        while(current != null){
            ListNode temp = current.next;
            current.next = tail;
            tail = current;
            current = temp;                        
        }

        ListNode l1 = head;
        ListNode l2 = tail;

        while(l1 != null && l2 != null){
            ListNode temp = l1.next;
            l1.next = l2;
            l2 = temp;
            l1 = l1.next;
        }
    }
}
```
{% endraw %}


