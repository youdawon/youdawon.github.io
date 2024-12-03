---
layout: post
date: 2024-12-03
title: "[Blind 75] Longest Common Subsequence"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/longest-common-subsequence/](https://leetcode.com/problems/longest-common-subsequence/)


이 문제는 DP를 이용하면 풀수 있다. 정말 어려운 DPㅠ


이차원 배열을 선언하고 text1의 현재 문자열과 text2의 현재 문자열이 같은 경우 [i-1][j-1]+1을 한다. 이렇게 하는 이유는 text1의 문자열(i-1)번째와, text2의 문자열(j-1)번째의 LCS값을 길이를 구할 수 있기 때문이다. 


두 값이 다를 경우 dp[i][j-1]과 dp[i-1][j]의 값을 비교해서 큰 숫자를 저장한다. 


그 이유는 예를 들어서 각 텍스트가 text1 : abcba, text2:abcbcba일때 abc와 a를 비교했을때 또는 ab와 ab를 비교했을 때 더 큰 수가 저장되어야 하기 때문이다. 



{% raw %}
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {

        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m+1][n+1];

        for(int i=1; i<=m; i++){
            for(int j=1; j<=n; j++){                
                if(text1.charAt(i-1) == text2.charAt(j-1)){
                    dp[i][j] = dp[i-1][j-1]+1;
                } else {
                    dp[i][j] = Math.max(dp[i][j-1], dp[i-1][j]);
                }
            }
        }
        
        return dp[m][n];
    }
}
```
{% endraw %}


