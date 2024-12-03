---
layout: post
date: 2024-12-03
title: "[Blind 75] Container With Most Water"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/container-with-most-water](https://leetcode.com/problems/container-with-most-water/description/)


투포인터를 이용하여 값을 구하는 문제이다. left와 right이 양 끝에서 시작하여 값이 같아지면 반복문을 마친다.  


컨테이너의 물 양은 두 높이 중 더 작은 높이를 기준으로 사각형의 넓이를 구하는 것처럼 right-left를 곱해주면 된다. 


그 다음에 현재 저장된 최대 물 양과 현재 물 양의 크기를 비교하여 더 큰 값을 최대 물 양에 저장해준다. 


마지막으로 left와 ,right이 위치한 높이 중 더 작은 쪽의 인덱스를 증가시켜준다.


#### 풀이1



{% raw %}
```java
class Solution {
    public int maxArea(int[] height) {
        
        int left = 0, right = height.length-1;
        int maximumWater = 0;

        while(left < right){
            int currentWater = Math.min(height[left], height[right]) * (right-left);
            maximumWater = Math.max(maximumWater, currentWater);
            
            if(height[left] > height[right]){
                right--;
            } else {
                left++;
            }
        }

        return maximumWater;
    }
}
```
{% endraw %}


