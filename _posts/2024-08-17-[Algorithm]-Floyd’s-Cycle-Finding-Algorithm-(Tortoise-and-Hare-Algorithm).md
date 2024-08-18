---
layout: post
date: 2024-08-17
title: "[Algorithm] Floyd’s Cycle-Finding Algorithm (Tortoise and Hare Algorithm)"
tags: [Algorithm, ]
categories: [Algorithm, LInkedList, ]
---


**Floyd’s Cycle-Finding Algorithm**, 흔히 **Tortoise and Hare 알고리즘**으로 알려진 이 알고리즘은 연결 리스트나 다른 순환 데이터 구조에서 사이클을 감지하는 효율적인 방법이다. 이 알고리즘은 두 개의 포인터를 사용하여 리스트를 순회하면서 사이클의 존재를 확인한다.


#### **알고리즘 개요**

- **목적**: 연결 리스트나 그래프 등의 데이터 구조에서 사이클이 존재하는지 확인한다.
- **핵심 아이디어**: 두 개의 포인터를 사용해 리스트를 순회하는데, 한 포인터는 한 번에 한 단계씩 이동하고(느린 포인터, **tortoise**), 다른 포인터는 두 단계씩 이동한다(빠른 포인터, **hare**). 사이클이 존재할 경우, 두 포인터는 결국 같은 노드에서 만나게 된다.

#### **알고리즘 동작 과정**

1. **포인터 초기화**:
	- 느린 포인터 `tortoise`와 빠른 포인터 `hare`를 모두 리스트의 첫 번째 노드에 위치시킨다.
2. **포인터 이동**:
	- `tortoise`는 한 번에 한 칸(한 노드)씩 이동하고, `hare`는 두 칸(두 노드)씩 이동한다.
3. **사이클 감지**:
	- 두 포인터가 같은 노드에서 만나면, 리스트에 사이클이 존재한다고 결론짓는다.
	- 만약 `hare`가 리스트의 끝에 도달하면(즉, `null`에 도달), 사이클이 존재하지 않는다고 판단한다.

#### **코드 구현 (Python 예시)**



{% raw %}
```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

def hasCycle(head: ListNode) -> bool:
    if not head or not head.next:
        return False

    tortoise = head
    hare = head

    while hare and hare.next:
        tortoise = tortoise.next          # 느린 포인터는 한 칸 이동
        hare = hare.next.next             # 빠른 포인터는 두 칸 이동

        if tortoise == hare:
            return True                   # 두 포인터가 만난다면 사이클이 존재

    return False                          # 리스트 끝에 도달하면 사이클이 없음
```
{% endraw %}



#### **알고리즘의 작동 원리**

- **사이클이 없는 경우**:
	- 빠른 포인터(`hare`)가 리스트의 끝에 도달(`null`)하면 반복문이 종료되고, 사이클이 존재하지 않는다는 것을 의미한다.
- **사이클이 있는 경우**:
	- `hare`는 `tortoise`보다 두 배 빠르게 움직이므로, 사이클 내에서 두 포인터가 반드시 만나게 된다. 이는 두 포인터가 동일한 노드에서 교차하게 되는 결과로 이어진다.

#### **시간 및 공간 복잡도**

- **시간 복잡도**: O(N)
	- 포인터가 리스트를 한 번 순회하며, 최대 N번의 비교 후에 사이클의 존재 여부를 판단할 수 있다.
- **공간 복잡도**: O(1)
	- 추가적인 메모리를 사용하지 않으며, 오직 두 개의 포인터만 사용한다.

#### **사이클의 시작점을 찾는 방법**


만약 사이클이 존재한다면, 사이클의 시작점을 찾을 수 있는 방법도 있다:

1. **사이클이 발견되었을 때**: `tortoise`를 리스트의 시작점으로 옮기고, `hare`는 그대로 두고, 두 포인터를 한 칸씩 이동시킨다.
2. **두 포인터가 다시 만나는 지점**: 이 지점이 사이클의 시작점이 된다.


{% raw %}
```python
def detectCycle(head: ListNode) -> ListNode:
    if not head or not head.next:
        return None

    tortoise = head
    hare = head

    while hare and hare.next:
        tortoise = tortoise.next
        hare = hare.next.next

        if tortoise == hare:
            break
    else:
        return None  # 사이클이 없다면 None을 반환

    tortoise = head
    while tortoise != hare:
        tortoise = tortoise.next
        hare = hare.next

    return hare  # 사이클의 시작점을 반환
```
{% endraw %}



#### **활용 사례**

- **링크드 리스트에서 사이클 감지**: 무한 루프 방지를 위한 연결 리스트의 사이클 감지.
- **그래프 이론**: 그래프 내에서의 순환 탐지.
- **컴퓨터 네트워크**: 패킷 순환 감지 및 네트워크 안정성 평가.
