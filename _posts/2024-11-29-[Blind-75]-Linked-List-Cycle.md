---
layout: post
date: 2024-11-29
title: "[Blind 75] Linked List Cycle"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/linked-list-cycle/description/](https://leetcode.com/problems/linked-list-cycle/description/)


이 문제를 풀기 위해서는 Floyd’s cycling Finding Algorithm을 알아야한다. 


이 알고리즘은 두개의 포인터를 이용해서 노드를 이동한다. 하나의 노드는 두번을 이동하고 나머지 하나는 하나씩 이동하는 것이다. 


이렇게 노드를 이동하다보면 서로 만나는 노드가 있는데 그 노드가 사이클의 시작점이 된다.


만약에 두번씩 이동하던 노드의 next 값이 null 일 경우엔 사이클이 존재하지 않은 것으로 판단한다. 


예) 3 → 0 → 1 → 4 이고 4에서 0으로 사이클이 반복되는 경우 아래와 같이 4에서 만나게 된다. 


slow pointer : 3→ 0 → 1 → 4 


fast pointer : 3→ 1 → 0 → 4



{% raw %}
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        
        ListNode slow = head;
        ListNode fast = head;

        while(fast.next != null){
            slow = slow.next;
            fast = fast.next.next;

            if(slow.val == fast.val){
                return true;
            }
        }

        return false;
    }
}
```
{% endraw %}


