---
layout: post
date: 2024-12-01
title: "[Blind 75] Longest Consecutive Sequence"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/longest-consecutive-sequence](https://leetcode.com/problems/longest-consecutive-sequence/)


해당 문제는 배열 내 연속되는 숫자의 최대 크기를 구하는 것이다. UnionFind를 이용하면 연속되는 숫자들 중 가장 작은 값을 구할 수 있다. 문제는 같은 숫자가 있으면 연속되는 숫자의 크기가 정확히 나오지 않을 수 있다. 이를 방지하기 위해 HashMap을 이용해서 이미 계산한 숫자는 다시 반복하지 않도록 처리를 하였다. 이 문제는 UnionFind클래스를 만드는 방법이 너무 헷갈려서 다시 한번 풀어봐야겠다.


#### 풀이1



{% raw %}
```java
class UnionFind {

    private int[] parent;
    private int[] size;

    public UnionFind(int n, int[] nums){
        parent = new int[n];
        size = new int[n];

        for(int i=0; i<n; i++){
            parent[i] = i;
            size[i] = 1;            
        }
    }

    public int find(int num){
        if(num != parent[num]){
            parent[num] = find(parent[num]);
        }
        return parent[num];
    }

    public int union(int num1, int num2){
        int parentX = find(num1);
        int parentY = find(num2);

        if(parentX != parentY){
            size[parentX] += size[parentY];
            parent[parentY] = parentX;
        }

        return size[parentX];
    }
}
class Solution {
    public int longestConsecutive(int[] nums) {

        int result = 0;

        Map<Integer, Integer> numbers = new HashMap<>();
        int n = nums.length;
        UnionFind uf = new UnionFind(n, nums);

        for(int i=0; i<n; i++){
            if(!numbers.containsKey(nums[i])){
                numbers.put(nums[i], i);
                int currentSize = 1;
                if(numbers.containsKey(nums[i]-1)){                
                    currentSize = Math.max(result, uf.union(numbers.get(nums[i]-1), i));
                }
                if(numbers.containsKey(nums[i]+1)){
                    currentSize = Math.max(result, uf.union(i, numbers.get(nums[i]+1)));
                }
                result = Math.max(result, currentSize); 
            }
        }        
        return result;
    }
}
```
{% endraw %}


