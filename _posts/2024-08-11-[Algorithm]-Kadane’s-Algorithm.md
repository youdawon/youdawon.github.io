---
layout: post
date: 2024-08-11
title: "[Algorithm] Kadane’s Algorithm"
tags: [Algorithm, ]
categories: [Algorithm, ]
---

1. 최대 연속 부분합을 효율적으로 찾는 알고리즘이다. 주어진 배열에서 연속된 원소들로 이루어진 부분 배열 중에서, 그 합이 최대가 되는 부분 배열의 합을 찾는데 사용된다.
2. 알고리즘
	1. 부분 합을 유지 : 현재 위치까지의 최대 부분합을 유지하면서 배열을 순회한다.
	2. 최대값 갱신 : 각 단계에서 현재 위치에서 끝나는 최대 부분합을 계산하고 이를 전체 배열에서의 최대부분합과 비교해 갱신한다.
	3. 부분합이 음수가 되면 초기화 : 현재 부분합이 음수가 되면 그 이전의 모든 합을 버리고 0으로 초기화하여 새로운 부분 배열을 시작하도록 한다.
3. 복잡도
	1. 시간 복잡도 : 배열 전체를 순회하므로 O(N)
	2. 공간 복잡도 : 배열과 같은 추가공간을 선언하지 않고 변수를 선언하여 사용하므로 O(1)
4. 참고 문제
	1. [https://leetcode.com/problems/maximum-subarray/?envType=problem-list-v2&envId=xi4ci4ig](https://leetcode.com/problems/maximum-subarray/?envType=problem-list-v2&envId=xi4ci4ig)
