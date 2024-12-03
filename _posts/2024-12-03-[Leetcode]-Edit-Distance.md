---
layout: post
date: 2024-12-03
title: "[Leetcode] Edit Distance"
tags: [Algorithm, Dynamic Programming, ]
categories: [Algorithm, Dynamic Programming, ]
---


[https://leetcode.com/problems/edit-distance/description/](https://leetcode.com/problems/edit-distance/description/)


이 문제는 꽤 까다롭다. 왜냐면 케이스가 3가지가 있기 때문이다. 이 문제도 DP로 풀어주어야 한다. 


중요한건 이거다. 


dp[i][j-1]는 삽입, dp[i-1][j-1]는 교체, dp[i-1][j]은 삭제이다. 



{% raw %}
```java
class Solution {
    public int minDistance(String word1, String word2) {

        int m = word1.length(), n = word2.length();
        int[][] dp = new int[m+1][n+1];

        for(int i=0; i<=m; i++){
            dp[i][0] = i;
        }

        for(int j=0; j<=n; j++){
            dp[0][j] = j;
        }        

        for(int i=1; i<=m; i++){
            for(int j=1; j<=n; j++){
                if(word1.charAt(i-1) == word2.charAt(j-1)){
                    dp[i][j] = dp[i-1][j-1];                    
                } else {
                    dp[i][j] = Math.min(Math.min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]) + 1;                    
                }
            }
        }

        return dp[m][n];
    }
}
```
{% endraw %}


