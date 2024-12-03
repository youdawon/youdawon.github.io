---
layout: post
date: 2024-12-03
title: "[Blind 75] Spiral Matrix"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/spiral-matrix/description/](https://leetcode.com/problems/spiral-matrix/description/) 


행의 양끝쪽과 열의 양끝쪽의 변수를 선언해서 반복문으로 통해 차례대로 데이터가 추가되도록 한다. 여기서 문제는 행의 끝 인덱스가 행의 시작 인덱스보다 작거나 또는 열의 끝 인덱스가 행의 시작 인덱스보다 작아지는 상황이 나타나는데 이러한 점을 방지하기 위한 조건문을 추가해주어야 한다.



{% raw %}
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {

        List<Integer> result = new ArrayList<>();
        
        int row_begin = 0, row_end = matrix.length-1;
        int col_begin = 0, col_end = matrix[0].length-1;

        int n = matrix.length * matrix[0].length;

        while(row_begin <= row_end && col_begin <= col_end){
            
            for(int j=col_begin; j<=col_end; j++){
                result.add(matrix[row_begin][j]);
            }
            row_begin++;
            for(int i=row_begin; i<=row_end; i++){
                result.add(matrix[i][col_end]);
            }
            col_end--;            

            if(col_begin > col_end || row_begin > row_end){
                break;
            }
            for(int j=col_end; j>=col_begin; j--){
                result.add(matrix[row_end][j]);
            }
            row_end--;
            for(int i=row_end; i>=row_begin; i--){
                result.add(matrix[i][col_begin]);
            }
            col_begin++;
        }
        return result;        
    }
}
```
{% endraw %}


