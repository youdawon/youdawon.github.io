---
layout: post
date: 2024-12-03
title: "[Blind 75] Rotate Image"
tags: [Algorithm, Blind75, ]
categories: [Algorithm, Blind75, ]
---


[https://leetcode.com/problems/rotate-image/](https://leetcode.com/problems/rotate-image/) 


이 문제는 일단 배열의 위 아래를 바꿔줘야 한다. 배열의 크기가 홀수 이므로 가운데 4, 5, 6은 바꿔줄 필요가 없다. 


![0](/assets/img/2024-12-03-[Blind-75]-Rotate-Image.md/0.png)


이렇게 바꿔주면 아래와 같이 배열이 만들어지는데 저 값들을 서로 교체만 해주면 된다. 


![1](/assets/img/2024-12-03-[Blind-75]-Rotate-Image.md/1.png)


자세히 보면 규칙을 알 수 있는데 i의 값이 배열의 row수만큼 반복할 동안 j의 값은 0에서 i보다 작은 수만큼 반복하면 된다. 그렇게 하면 방문하게 되는 배열의 인덱스는 (1,0),(2,0),(2,1)이 되는데 이걸 (0,1),(0,2),(1,2)와 바꿔주면 된다.


![2](/assets/img/2024-12-03-[Blind-75]-Rotate-Image.md/2.png)



{% raw %}
```java
class Solution {
    public void rotate(int[][] matrix) {

        int middle = matrix.length / 2;
        int m = matrix.length-1, n = matrix[0].length-1;        

        for(int i=0; i<middle; i++){
            int[] temp = matrix[m-i];
            matrix[m-i] = matrix[i];
            matrix[i] = temp;
        }

        for(int i=0; i<=m; i++){
            for(int j=0; j<i; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
    }
}
```
{% endraw %}


