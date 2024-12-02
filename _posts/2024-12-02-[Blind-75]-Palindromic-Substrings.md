---
layout: post
date: 2024-12-02
title: "[Blind 75] Palindromic Substrings"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/palindromic-substrings](https://leetcode.com/problems/palindromic-substrings/)


투 포인터를 이용해서 총 개수를 구하였다. 문자수가 홀수인 케이스와 짝수인 케이스가 존재하기 때문에 두 케이스 모두 고려해서 개수를 구해주어야 한다. 



{% raw %}
```java
class Solution {
    public int countSubstrings(String s) {

        int count = 0;

        for(int i=0; i<s.length(); i++){
            int left = i;
            int right = i;
            count += getPalindromicStringCount(left, right, s); 

            left = i;
            right = i+1;
            count += getPalindromicStringCount(left, right, s);             
        }

        return count;
    }

    private int getPalindromicStringCount(int left, int right, String s){
        int count = 0;
        while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)){
            count++;
            left--;
            right++;
        }
        return count;
    }
}
```
{% endraw %}


