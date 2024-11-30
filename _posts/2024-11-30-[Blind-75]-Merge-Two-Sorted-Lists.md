---
layout: post
date: 2024-11-30
title: "[Blind 75] Merge Two Sorted Lists"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/merge-two-sorted-lists](https://leetcode.com/problems/merge-two-sorted-lists/)


이 문제는 각각 노드의 값을 비교한 후 더 작은 값을 가진 노드를 임의로 만든 노드에 이어준다. 



{% raw %}
```java

class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        
        ListNode dummy = new ListNode(-1);
        ListNode current = dummy;

        while(list1 != null || list2 != null){

            if(list1 == null){
                current.next = list2;
                return dummy.next;
            }

            if(list2 == null){
                current.next = list1;
                return dummy.next;
            }            

            if(list1.val <= list2.val){
                current.next = list1;
                list1 = list1.next;
            } else {
                current.next = list2;
                list2 = list2.next;
            }
            current = current.next;

        }

        return dummy.next;
    }
}
```
{% endraw %}


