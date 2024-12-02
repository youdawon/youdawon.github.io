---
layout: post
date: 2024-12-02
title: "[Blind 75] Longest Palindromic Substring"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/longest-palindromic-substring](https://leetcode.com/problems/longest-palindromic-substring/description/)


이 문제는 두가지 방법으로 풀이하였다.


#### 풀이1


 two pointer를 이용해서 left는 왼쪽으로 이동하고 right은 오른쪽으로 이동하면서 문자열을 비교하는 것이다. 이 풀이는 반복문을 두번 처리해줘야 하는데 그 이유는 aba와 같이 홀수길이의 문자열을 처리하기 위해서고 나머지는 abba와 같이 짝수 문자열을 처리하기 위해서다. 



{% raw %}
```java
class Solution {
    public String longestPalindrome(String s) {
        
        String result = "";

        for(int i=0; i<s.length(); i++){
            int left = i;
            int right = i;
            String currentStr = getLongestSubString(left, right, s);
            if(currentStr.length() > result.length()){
                result = currentStr;
            }

            left = i;
            right = i+1;
            currentStr = getLongestSubString(left, right, s);
            if(currentStr.length() > result.length()){
                result = currentStr;
            }
        }
        return result;

    }

    private String getLongestSubString(int left, int right, String s){
        while(left >= 0 && right < s.length() 
        && s.charAt(left) == s.charAt(right)){
            left--;
            right++;
        }        
        return s.substring(left+1, right);
    }
}
```
{% endraw %}



#### 풀이2


두번째 풀이는 DP를 사용하였다. DP는 내가 잘 못하는 부분이라 연습이 많이 필요해보인다. 어찌됐든 머리를 쥐어짜서 풀어보았다. 이 풀이의 방법은 문자열을 뒤에서 부터 반복문을 돌면서 비교한다는 점이다. 일단 해당 문자열의 dp를 이차원 배열로 만든다. 그리고 문자열이 같은 경우 true로 바꿔주면서 값을 찾아나간다. 예를 들어 cdbd라는 예제가 있다고 하자. 


|   | c | d | b | d |
| - | - | - | - | - |
| c | F | F | F | F |
| d | F | F | F | F |
| b | F | F | F | F |
| d | F | F | F | T |


|   | c | d | b | d |
| - | - | - | - | - |
| c | F | F | F | F |
| d | F | F | F | F |
| b | F | F | T | F |
| d | F | F | F | T |


|   | c | d | b | d |
| - | - | - | - | - |
| c | F | F | F | F |
| d | F | T | F | F |
| b | F | F | T | F |
| d | F | F | F | T |


i = 3이고 j=3일 경우 두 문자는 같고 문자열의 크기는 3보다 작다. 팰린드롬은 3보다 작을 경우 즉, a, bb일 경우 중간 문자열을 비교할 필요가 없기 때문에 해당 배열값을 true로 바꿔주고 maxLength와 문자열을 어디서부터 자를건지 저장할 start 값을 업데이트 해준다. 


i=2이고 j=3일 경우 bd이므로 팰린드롬이 될 수 없다.


i=1이고 j=3일 경우 같은 d이므로 팰린드롬이 될수 있지만 중간 문자열을 비교해야한다. 중간 문자열은 b가 되는데 dp배열에서 해당 값은 dp[2][2]가 된다. dp[2][2]는 true이기 때문에 maxLength와 start를 업데이트 해준다. 


마지막 응답값 전달 시 start는 문자열을 자를 index가 되고 maxLength에 start를 더해줌으로서 문자열을 자를 인덱스를 구한다. 



{% raw %}
```java
class Solution {
    public String longestPalindrome(String s) {

        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        int start = 0;
        int maxLength = 0;

        for(int i = n-1; i >= 0; i--){
            for(int j = i; j < n; j++){
                if(s.charAt(i) == s.charAt(j)){
                    if(j-i+1 < 3 || dp[i+1][j-1]){
                        dp[i][j] = true;
                        if(j-i+1 > maxLength){
                            maxLength = j-i+1;
                            start = i;
                        }
                    }
                }
            }
        }
        return s.substring(start, maxLength+start);
    }
}
```
{% endraw %}


