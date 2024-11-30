---
layout: post
date: 2024-11-30
title: "[Blind 75] Word Search"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/word-search](https://leetcode.com/problems/word-search/)


이 문제는 조금 헷갈리는 부분이 있었다. word의 index의 값과 board[i][j]의 값이 같으면 해당 배열의 주변에 다음 word index값과 같은지를 비교해야한다. 배열 이동은 상하좌우만 가능하다. 헷갈렸던 점은 예를 들어 내가 C를 방문했을 경우 그 주변도 방문하게 되는데 방문한 배열이 다음word index과 다르지 않을 경우를 예상해서 visited[i][j] = false 처리를 해줘야하는지 하지 않았다는 점이다. 



{% raw %}
```java
class Solution {
    public boolean exist(char[][] board, String word) {     

        int m = board.length;
        int n = board[0].length;

        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                boolean[][] visited = new boolean[m][n];
                if(dfs(board, i, j, word, 0, visited)){
                    return true;
                }
            }
        }
        return false;
    }

    public boolean dfs(char[][] board, int i, int j, String word, int index, boolean[][] visited){

        if(index == word.length()){
            return true;
        }

        if(i < 0 || j < 0 || i >= board.length || j >= board[0].length || visited[i][j]){
            return false;
        }

        if(board[i][j] != word.charAt(index)){
            return false;
        }

        visited[i][j] = true;

        boolean res =(dfs(board, i-1, j, word, index+1, visited) ||
        dfs(board, i+1, j, word, index+1, visited) || 
        dfs(board, i, j-1, word, index+1, visited) || 
        dfs(board, i, j+1, word, index+1, visited));     
        
        visited[i][j] = false;                                   

        return res;
    }
}
```
{% endraw %}


