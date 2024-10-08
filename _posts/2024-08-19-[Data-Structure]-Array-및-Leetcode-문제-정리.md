---
layout: post
date: 2024-08-19
title: "[Data Structure] Array 및 Leetcode 문제 정리"
tags: [Data Structure, Array, ]
categories: [Data Structure, ]
---


### 배열(Array) 개념 및 주요 특징

1. **정의**:
	- 배열(Array)은 동일한 데이터 타입의 요소들을 순차적으로 나열한 데이터 구조다. 배열은 메모리에서 연속된 공간을 차지하며, 각 요소는 인덱스를 통해 접근할 수 있다.
2. **주요 특징**:
	- **고정된 크기**: 대부분의 배열은 생성 시 크기가 고정된다. 배열의 크기를 초과하는 요소를 저장할 수 없다.
	- **빠른 접근 시간**: 인덱스를 사용하여 요소에 O(1) 시간 복잡도로 접근할 수 있다.
	- **메모리 효율성**: 연속된 메모리 공간을 사용하므로 메모리 효율이 높다.
	- **동일한 데이터 타입**: 배열에 저장된 모든 요소는 동일한 데이터 타입을 가져야 한다.
3. **배열의 연산**:
	- **탐색(Search)**: 특정 요소를 찾기 위해 배열의 모든 요소를 순회해야 할 수 있으며, 시간 복잡도는 O(n)이다.
	- **삽입(Insertion)**: 배열의 중간에 요소를 삽입하려면 요소들을 이동시켜야 하므로 평균 시간 복잡도는 O(n)이다.
	- **삭제(Deletion)**: 배열의 요소를 삭제한 후, 그 뒤에 있는 요소들을 이동시켜야 하므로 평균 시간 복잡도는 O(n)이다.
	- **접근(Access)**: 특정 인덱스의 요소에 접근하는 시간 복잡도는 O(1)이다.
4. **배열의 유형**:
	- **1차원 배열**: 단일 차원의 배열로, 선형적으로 데이터가 나열된다.
	- **2차원 배열**: 행과 열로 구성된 배열로, 주로 행렬을 표현하는 데 사용된다.
	- **다차원 배열**: 2차원 이상의 배열로, 복잡한 데이터 구조를 표현할 수 있다.
	- **동적 배열**: 크기가 고정되지 않고, 필요에 따라 크기를 조절할 수 있는 배열(예: Python의 리스트, Java의 ArrayList).

#### 면접에서 자주 나오는 배열 관련 질문 유형

1. **배열 탐색 문제**:
	- 예시: "정렬된 배열에서 특정 요소를 찾는 방법은?", "배열에서 가장 큰/작은 요소를 찾는 방법은?"
	- **팁**: 이진 탐색 알고리즘을 사용하는 방법과 O(n) 탐색의 차이점 및 시간 복잡도를 이해하고 설명할 수 있어야 한다.
2. **배열 회전 및 반전 문제**:
	- 예시: "배열을 오른쪽으로 k번 회전시키는 방법은?", "배열을 반전시키는 방법은?"
	- **팁**: 배열 회전 문제에서는 브루트포스와 최적화된 방법을 설명할 수 있어야 하며, 공간 복잡도에 대해서도 논의할 준비를 해야 한다.
3. **중복 요소 찾기 문제**:
	- 예시: "배열에서 중복된 요소를 찾는 방법은?", "중복을 제거하고 배열을 정렬하는 방법은?"
	- **팁**: 해시맵, 해시셋 등을 사용해 효율적으로 중복을 찾거나 제거하는 방법을 알고 있어야 한다.
4. **슬라이딩 윈도우**:
	- 예시: "슬라이딩 윈도우를 사용해 배열 내 연속된 요소들의 합이 최대인 부분 배열을 찾는 방법은?"
	- **팁**: 슬라이딩 윈도우 기법을 통해 O(n) 시간 복잡도로 문제를 해결하는 방법을 이해하고 있어야 한다.
5. **다차원 배열 문제**:
	- 예시: "2D 배열에서 특정 요소를 찾는 방법은?", "2D 행렬을 시계방향으로 회전시키는 방법은?"
	- **팁**: 다차원 배열에서 행과 열을 탐색하는 방법 및 행렬 회전의 알고리즘을 숙지해야 한다.
6. **배열과 관련된 정렬 문제**:
	- 예시: "배열을 정렬하는 가장 효율적인 방법은?", "퀵 정렬과 병합 정렬의 차이점은?"
	- **팁**: 기본적인 정렬 알고리즘(퀵 정렬, 병합 정렬, 버블 정렬 등)의 시간 및 공간 복잡도, 그리고 각 알고리즘의 장단점을 설명할 수 있어야 한다.

#### 면접 팁

1. **기본 개념을 확실히 이해하라**:
	- 배열의 기본 연산(탐색, 삽입, 삭제 등)과 그 시간 복잡도(O(1), O(n) 등)를 명확히 이해하고 있어야 한다.
2. **다양한 문제 유형에 익숙해져라**:
	- 배열과 관련된 다양한 문제를 많이 풀어보는 것이 중요하다. 이를 통해 다양한 문제 해결 방법을 학습하고, 알고리즘적 사고를 길러야 한다.
3. **효율성과 최적화를 고려하라**:
	- 배열 문제에서는 종종 시간과 공간의 효율성을 고려해야 한다. 브루트포스 접근법과 최적화된 방법을 비교하여 설명할 수 있어야 한다.
4. **코딩 연습**:
	- 배열 문제는 손으로 코딩하는 연습이 필수다. 특히, 시간 안에 정확히 코드 작성하는 연습을 많이 해야 한다.
5. **경계 조건을 고려하라**:
	- 배열 문제에서는 배열이 비어있거나, 크기가 매우 클 때 발생할 수 있는 경계 조건을 반드시 고려해야 한다. 이로 인해 발생할 수 있는 예외 처리도 생각해 두어야 한다.
6. **구조와 패턴을 파악하라**:
	- 반복되는 패턴(예: 슬라이딩 윈도우, 투 포인터, 정렬 후 이진 탐색 등)을 파악하여 효율적인 문제 해결 방법을 찾는 능력을 키워야 한다.

#### 리트코드 문제

- [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
- [Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)
- [Two Sum](https://leetcode.com/problems/two-sum/)
- [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- [Encode and Decode Tinyurl](https://leetcode.com/problems/encode-and-decode-tinyurl/description/)
- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
- [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
- [Best Time to Buy And Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- [3Sum](https://leetcode.com/problems/3sum/)
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
