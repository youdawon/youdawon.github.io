---
layout: post
date: 2024-12-03
title: "[Blind 75] Missing Number"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/missing-number/description/](https://leetcode.com/problems/missing-number/description/)


이 문제는 bit 계산을 이용해서 계산한다. 진짜 맨날 헷갈리는 건데 XOR의 계산방식을 이용하면 쉽게 문제를 풀 수 있다. 


일단 n까지의 모든 수를 XOR를 이용해 비트계산을 한다. 그리고 나서 배열의 있는 값들과 또 XO을 처리한다. 이렇게 하는 이유는 XOR은 두 수가 다르면 1이 되는 성질이 있다. 그래서 이미 result에 연산이 되어있는 값이 배열에 존재한다면 그 수는 제거가 된다. 그렇게 하다보면 result에 더해지지 않은 값이 남게 된다. 



{% raw %}
```java
class Solution {
    public int missingNumber(int[] nums) {

        int n = nums.length;
        int result = 0;
        
        for(int i=0; i<=n; i++){
            result ^= i;            
        }

        for(int i=0; i<n; i++){
            result ^= nums[i];            
        }

        return result;
    }
}
```
{% endraw %}


