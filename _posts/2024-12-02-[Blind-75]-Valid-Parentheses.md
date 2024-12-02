---
layout: post
date: 2024-12-02
title: "[Blind 75] Valid Parentheses"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/valid-parentheses](https://leetcode.com/problems/valid-parentheses/)


stack을 사용하여 풀었다. 문자열이 (, [, { 인 경우 각 문자열과 대칭되는 ),],} 값을 넣어준다. 그리고 현재 문자열이 스택의 가장 위에 있는 문자열과 다른 경우 또는, 스택에 비교할 문자열이 존재하지 않는 경우 false로 전달한다.


#### 풀이1



{% raw %}
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(char c : s.toCharArray()){
            if(c == '('){
                stack.push(')');
            } else if(c == '{'){
                stack.push('}');                
            } else if(c == '['){
                stack.push(']');
            } else {
                if(stack.isEmpty() || c != stack.peek()){
                    return false;
                }
                stack.pop();
            }
        }
        return stack.isEmpty() ? true : false;
    }
}
```
{% endraw %}


