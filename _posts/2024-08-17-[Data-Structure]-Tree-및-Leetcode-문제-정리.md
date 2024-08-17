---
layout: post
date: 2024-08-17
title: "[Data Structure] Tree 및 Leetcode 문제 정리"
tags: [DataStructure, Tree, LeetCode, ]
categories: [DataStructure, ]
---


### 1. 기본 개념

- **트리(Tree)**: 계층적 데이터 구조로, 하나의 루트 노드에서 시작해 자식 노드로 연결되는 구조를 가짐.
- **노드(Node)**: 트리의 각 요소로, 데이터와 자식 노드를 가리키는 포인터(혹은 참조)를 포함.
- **루트 노드(Root Node)**: 트리의 최상위 노드.
- **리프 노드(Leaf Node)**: 자식 노드가 없는 노드.
- *부모 노드(Parent Node)**와 **자식 노드(Child Node)**: 특정 노드가 다른 노드를 가리킬 때, 가리키는 노드를 자식 노드, 가리키는 노드를 부모 노드라 함.
- **서브트리(Subtree)**: 트리의 부분 트리, 특정 노드와 그 하위 노드들이 서브트리를 이룸.
- **높이(Height)**: 노드에서 리프까지의 가장 긴 경로의 길이.
- **깊이(Depth)**: 루트에서 특정 노드까지의 경로의 길이.

#### 2. 트리의 종류


#### 2.1 **이진 트리 (Binary Tree)**

- **개념**: 각 노드가 최대 두 개의 자식을 가지는 트리.
- **예시 그림**:


{% raw %}
```text
    1
   / \
  2   3
 / \   \
4   5   6
```
{% endraw %}



#### 2.2 **완전 이진 트리 (Complete Binary Tree)**

- **개념**: 마지막 레벨을 제외한 모든 레벨이 완전히 채워진 이진 트리.
- **예시 그림**:


{% raw %}
```text
      1
    /   \
   2     3
  / \   /
 4   5 6
```
{% endraw %}



#### 2.3 **이진 탐색 트리 (Binary Search Tree, BST)**

- **개념**: 왼쪽 자식 노드의 값이 부모보다 작고, 오른쪽 자식 노드의 값이 부모보다 큰 이진 트리.
- **예시 그림**:


{% raw %}
```text
    4
   / \
  2   6
 / \ / \
1  3 5  7
```
{% endraw %}



#### 2.4 **균형 이진 트리 (Balanced Binary Tree)**

- **개념**: 모든 서브트리의 높이 차이가 1 이하인 이진 트리.
- **예시 그림**:


{% raw %}
```text
      4
    /   \
   2     6
        / \
       5   7
```
{% endraw %}



#### 2.5 **레드-블랙 트리 (Red-Black Tree)**

- **개념**: 자가 균형 이진 탐색 트리로, 삽입과 삭제 시 트리의 균형을 유지하는 트리. 최악의 경우에도 O(log n) 시간 복잡도를 보장함.
- **예시 그림**: (노드 색상: R = Red, B = Black)


{% raw %}
```text
      7B
     /  \\
   3R    10B
  / \\    / \\
 1B  5B 8R  12B
```
{% endraw %}



#### 2.6 **트라이 (Trie)**

- **개념**: 문자열 검색을 위한 특수한 트리 구조. 각 노드가 문자열의 한 문자를 나타내며, 단어의 접두사를 공유하는 문자열들을 효율적으로 저장하고 탐색할 수 있음.
- **예시 그림**: (단어: "cat", "car", "dog")


{% raw %}
```text
        (root)
        /  |  \\
       c   d   a
      /    |    \\
     a     o     t
    /      |     |
   t(R)    g(R)  r(R)
    \\      |
     r(R)  s(R)
```
{% endraw %}



(R = 단어의 끝을 표시)


#### 2.7 **세그먼트 트리 (Segment Tree)**

- **개념**: 배열의 특정 구간에 대한 쿼리(합, 최소/최대값)를 효율적으로 처리하기 위한 트리 구조.
- **예시 그림**: (배열: `[2, 1, 5, 3]`에 대한 세그먼트 트리)


{% raw %}
```text
          11
         /  \
       3      8
      / \    / \
     2   1  5   3
```
{% endraw %}



#### 2.8 **이진 힙 (Binary Heap)**

- **개념**: 최대 또는 최소 값을 효율적으로 추출하기 위한 완전 이진 트리.
- **예시 그림**: (최대 힙의 예시)


{% raw %}
```text
      10
     /  \
    9    8
   / \  / \
  7  6 5   4
```
{% endraw %}



#### 3. 트리의 주요 연산 및 알고리즘

- **트리 순회(Tree Traversal)**:
	- **전위 순회(Preorder Traversal)**: 루트 -> 왼쪽 서브트리 -> 오른쪽 서브트리.
	- **중위 순회(Inorder Traversal)**: 왼쪽 서브트리 -> 루트 -> 오른쪽 서브트리.
	- **후위 순회(Postorder Traversal)**: 왼쪽 서브트리 -> 오른쪽 서브트리 -> 루트.
	- **레벨 순서 순회(Level-Order Traversal)**: 루트부터 레벨별로 순차 탐색 (BFS).
- **삽입(Insertion)**: 새로운 노드를 트리에 추가하는 과정.
- **삭제(Deletion)**: 트리에서 노드를 제거하는 과정.
- **탐색(Search)**: 트리에서 특정 값을 찾는 과정.

#### 4. 트리 관련 리트코드 문제

- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal)
- [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
- [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)
- [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree)
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree)

#### 5. 트리와 관련된 면접 질문 유형


#### **기본 개념 이해**

1. 트리란 무엇이며, 트리의 구성 요소를 설명해라.
2. 이진 탐색 트리(Binary Search Tree)의 정의와 특성을 설명해라.
3. 이진 트리와 이진 탐색 트리의 차이점은 무엇인가?

#### **트리 순회(Traversal)**

1. 트리 순회의 종류(전위, 중위, 후위, 레벨 순서)에 대해 설명해라.
2. 이진 트리의 중위 순회(Inorder Traversal)를 재귀적 방식과 반복적 방식으로 구현해라.
3. 레벨 순서 순회(Level-Order Traversal)를 구현해라.

#### **트리의 높이 및 깊이**

1. 트리의 높이와 깊이의 차이점을 설명해라.
2. 이진 트리의 최대 깊이(Maximum Depth)를 계산하는 방법을 설명해라.

#### **이진 탐색 트리(BST)**

1. 이진 탐색 트리의 삽입(Insertion)과 삭제(Deletion) 연산을 설명하고 구현해라.
2. 주어진 트리가 이진 탐색 트리인지 확인하는 코드를 작성해라.
3. 이진 탐색 트리에서 최소값 또는 최대값을 찾는 방법을 설명해라.
4. 이진 탐색 트리에서 두 노드의 공통 조상(Lowest Common Ancestor)을 찾는 방법을 설명해라.

#### **트리의 변형 및 균형 유지**

1. AVL 트리와 레드-블랙 트리의 차이점을 설명해라.
2. AVL 트리에서 균형을 유지하기 위한 회전 연산(Rotation)을 설명해라.
3. 트라이(Trie)를 사용하여 문자열을 저장하고 검색하는 방법을 설명해라.

#### **힙(Heap)**

1. 최소 힙(Min-Heap)과 최대 힙(Max-Heap)의 차이점을 설명해라.
2. 힙 정렬(Heap Sort)을 설명하고, 이를 구현해라.
3. 이진 힙에서 삽입(Insertion)과 삭제(Deletion) 연산을 설명해라.

#### **트리의 활용**

1. 트리를 사용하여 계층적 데이터를 표현하는 예를 들어 설명해라.
2. 이진 탐색 트리를 사용해 데이터를 효율적으로 검색하는 상황을 설명해라.
3. DFS(깊이 우선 탐색)와 BFS(너비 우선 탐색)를 트리에서 구현하는 방법을 설명해라.

#### **실전 문제 해결**

1. 주어진 이진 트리에서 두 노드 간의 경로를 찾는 방법을 설명해라.
2. 이진 트리의 직경(Diameter)을 구하는

방법을 설명해라.
3. 트리에서 노드를 삭제할 때, 그 과정에서 발생할 수 있는 문제점과 이를 해결하는 방법을 설명해라.


#### 6. **면접 팁**

- **기본기를 다져라**: 트리의 기본 개념과 각종 트리의 특징을 확실하게 이해하라.
- **경계 조건을 고려하라**: 트리 문제에서는 경계 조건(예: 트리가 비었을 때, 단일 노드 트리 등)을 잘 고려하도록 연습하라.
- **트리 순회를 연습하라**: 전위, 중위, 후위, 레벨 순서 순회를 구현할 수 있도록 연습하라.
