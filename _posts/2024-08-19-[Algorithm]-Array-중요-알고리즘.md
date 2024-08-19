---
layout: post
date: 2024-08-19
title: "[Algorithm] Array 중요 알고리즘"
tags: [Data Structure, Array, ]
categories: [Data Structure, ]
---


### 1. **슬라이딩 윈도우 (Sliding Window)**

- **개념**: 배열이나 리스트의 연속된 부분 집합을 탐색하거나 계산할 때 사용된다. 윈도우의 크기를 고정하거나 가변적으로 설정한 후, 윈도우를 한 칸씩 이동하면서 값을 계산한다.
- **예시 문제**:
	- 최대 길이의 부분 배열 구하기 (예: 최대 합을 가진 부분 배열)
	- 고정된 길이의 부분 배열에서 최대/최소 값 찾기
- **대표 문제**: [LeetCode - Maximum Sum Subarray of Size K](https://leetcode.com/problems/maximum-average-subarray-i/)

#### 2. **이진 탐색 (Binary Search)**

- **개념**: 정렬된 배열에서 원하는 값을 O(log n) 시간 복잡도로 찾는 알고리즘이다. 배열을 반씩 나누어 탐색 범위를 좁혀나간다.
- **예시 문제**:
	- 정렬된 배열에서 특정 값 찾기
	- 가장 가까운 값 찾기
	- 이진 탐색을 활용한 최적화 문제 (예: 페인팅 문제)
- **대표 문제**: [LeetCode - Binary Search](https://leetcode.com/problems/binary-search/)

#### 3. **투 포인터 (Two Pointers)**

- **개념**: 배열에서 두 개의 포인터를 사용해 문제를 해결하는 기법이다. 포인터를 배열의 양 끝이나 특정 위치에 놓고 조건에 맞게 이동시킨다.
- **예시 문제**:
	- 두 수의 합 (Two Sum) 문제
	- 중복 제거 (예: 중복된 요소 제거 후 배열 길이 반환)
	- 특정 조건을 만족하는 부분 배열 찾기
- **대표 문제**: [LeetCode - Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

#### 4. **병합 정렬과 퀵 정렬 (Merge Sort & Quick Sort)**

- **개념**: 정렬 알고리즘으로, 배열을 효율적으로 정렬할 수 있다.
	- **병합 정렬**: 배열을 분할한 후 병합하면서 정렬하는 O(n log n) 알고리즘.
	- **퀵 정렬**: 피벗을 기준으로 분할 정복 기법을 사용하는 O(n log n) 평균 시간 복잡도 알고리즘.
- **예시 문제**:
	- 큰 배열을 정렬하기
	- 병합 정렬을 이용한 Inversion Count 문제
- **대표 문제**: [LeetCode - Sort an Array](https://leetcode.com/problems/sort-an-array/)

#### 5. **카데인 알고리즘 (Kadane's Algorithm)**

- **개념**: 연속된 부분 배열의 최대 합을 찾는 데 사용되는 알고리즘. O(n) 시간 복잡도로 해결할 수 있다.
- **예시 문제**:
	- 최대 합을 가진 연속된 부분 배열 찾기
- **대표 문제**: [LeetCode - Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

#### 6. **정렬된 배열에서의 합 문제 (Sum Problems in Sorted Arrays)**

- **개념**: 주어진 정렬된 배열에서 특정 합을 만족하는 두 수를 찾는 문제. 투 포인터 기법을 자주 사용한다.
- **예시 문제**:
	- 두 수의 합 문제
	- 세 수의 합 문제
- **대표 문제**: [LeetCode - 3Sum](https://leetcode.com/problems/3sum/)

#### 7. **해시를 이용한 중복 검사 (Hashing for Duplicate Checking)**

- **개념**: 배열에서 중복된 요소를 찾거나 제거할 때 해시맵이나 해시셋을 사용하는 방법.
- **예시 문제**:
	- 배열에 중복된 요소가 있는지 검사하기
	- 배열에서 k 거리 내의 중복 요소 찾기
- **대표 문제**: [LeetCode - Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

#### 8. **로테이션 알고리즘 (Rotation Algorithms)**

- **개념**: 배열을 특정 방향으로 회전시키는 알고리즘.
- **예시 문제**:
	- 배열을 k번 오른쪽으로 회전시키기
	- 배열을 왼쪽으로 회전시키기
- **대표 문제**: [LeetCode - Rotate Array](https://leetcode.com/problems/rotate-array/)

#### 9. **부분 합 및 Prefix Sum (Prefix Sum & Subarray Sum)**

- **개념**: 배열에서 부분 합을 계산하거나 특정 조건을 만족하는 부분 배열을 찾는 알고리즘. Prefix Sum은 배열의 부분 합을 효율적으로 계산할 수 있게 해준다.
- **예시 문제**:
	- 주어진 합을 갖는 부분 배열 찾기
	- 배열의 구간 합을 구하기
- **대표 문제**: [LeetCode - Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

#### 10. **누적 합 알고리즘 (Cumulative Sum)**

- **개념**: 배열의 모든 요소의 누적 합을 구하여 각 위치의 합을 계산하는 알고리즘.
- **예시 문제**:
	- 특정 구간의 합 구하기
	- 배열을 구간별로 분할하여 합을 계산하기
- **대표 문제**: [LeetCode - Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/)

#### 면접 팁

1. **알고리즘의 시간 복잡도와 공간 복잡도**를 항상 염두에 두고, 최적화된 방법을 설명할 수 있어야 한다.
2. **기본적인 배열 연산**(삽입, 삭제, 탐색)에 대한 이해와 구현 능력을 보여줘야 한다.
3. **패턴 인식**: 문제를 다양한 패턴으로 분석하여 가장 적합한 알고리즘을 적용하는 능력을 키워야 한다. 예를 들어, 슬라이딩 윈도우 패턴을 언제 사용하는지 명확히 이해해야 한다.
4. **코딩 연습**: 손코딩 연습을 통해 각 알고리즘의 구현 능력을 강화하라. 특히, 경계 조건과 예외 처리를 항상 고려해야 한다.
5. **다양한 문제를 풀어보라**: LeetCode, HackerRank, Codeforces와 같은 플랫폼에서 다양한 배열 관련 문제를 풀어보며 실력을 다져야 한다.

배열은 기본적이면서도 다양한 문제 유형에서 활용되는 중요한 자료구조이므로, 이러한 알고리즘들을 깊이 이해하고 연습하는 것이 면접에서 좋은 결과를 얻는 데 중요하다.

