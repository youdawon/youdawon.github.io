---
layout: post
date: 2024-12-01
title: "[Blind 75] Longest Increasing Subsequence "
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/longest-increasing-subsequence/description/](https://leetcode.com/problems/longest-increasing-subsequence/description/)


DP는 정말 어렵다ㅠ 이 문제는 값이 차례로 증가하는 subsequence중에 최장길이를 구하는 문제이다. 일단 각 배열 값의 길이를 저장할 dp 배열을 만든다. 나 자신을 포함한 길이이므로 array들의 값의 디폴트는 1로 설정한다. 현재 내 배열의 값과 내 이전의 값들을 비교하려면 for문을 써서 값을 비교해야한다. 현재 내가 위치한 배열을 이전의 값들과 하나씩 비교한다. 만약에 내가 위치한 배열의 값이 이전의 값보다 클 경우 dp를 업데이트한다. 근데 여기서 생각을 해보아야하는게 예를 들어 문제가 아래과 같을 경우 현재 내 위치가 101일때 최장 길이는 2, 5, 101 이 되어야한다. 그러나 차례로 증가 하는 값들의 subsequence는 2, 101도 존재한다. 그말은 즉, 각 값을 비교할때마다 내 현재 dp의 값을 계속 최대 값으로 갱신해줘야한다는 소리이다. 


모든 값 비교가 끝난 후 한번 더 maxLength와 dp[i]값을 비교해준다. 이것도 앞의 내용과 비슷하게 이전에 가장 긴 값이 2, 5였기 때문에 2, 5, 101인 3으로 업데이트 해주는 작업이 필요하기 때문이다.


nums = [10,9,2,5,4,2,101,18]


시간복잡도는 O(N^2)


#### 풀이1



{% raw %}
```java
class Solution {
    public int lengthOfLIS(int[] nums) {

        int maxLength = 0;

        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);

        for(int i=0; i<nums.length; i++){
            for(int j=0; j<i; j++){
                if(nums[j] < nums[i]){             
                    dp[i] = Math.max(dp[i], dp[j]+1);
                }
            }
            maxLength = Math.max(maxLength, dp[i]);
        }
        return maxLength;
    }
}
```
{% endraw %}



#### 풀이2


이건 Binary Search를 이용한 방법이다. Binary Search를 이용해서 이렇게 풀수 있는 방법이 있는지 몰랐는데 솔직히 쳇지티피 힌트보고 풀어보았다. 리스트 하나를 만들고 각 배열의 값을 하나하나 비교하면서 리스트의 값을 업데이트 하는 것이다. 시간복잡도는 Binary Search가 O(logN)이니까 O(NlogN)이다. 이렇게 푸는 방법은 다른 문제를 풀어서 적응을 해봐야할 것 같다. 



{% raw %}
```java
class Solution {
    public int lengthOfLIS(int[] nums) {

        List<Integer> list = new ArrayList<>();

        for(int num : nums){
            int left = 0;
            int right = list.size();

            while(left<right){
                int mid = left + (right-left)/2;
                if(list.get(mid) < num){
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }

            if(list.size() == left){
                list.add(num);
            } else{
                list.set(left, num);
            }
        }
        return list.size();
    }
}
```
{% endraw %}


