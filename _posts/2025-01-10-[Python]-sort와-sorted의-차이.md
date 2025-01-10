---
layout: post
date: 2025-01-10
title: "[Python] sort와 sorted의 차이"
tags: [Python, ]
categories: [Python, ]
---

1. sorted

정렬대상 : 리스트


특징 : 리스트 객체의 메서드로 원본 리스트를 직접 정렬한다. 따라서 반환값이 None이다. 



{% raw %}
```python
numbers = [3, 1, 4, 1, 5, 9]
numbers.sort()  # 원본 리스트가 정렬됨
print(numbers)  # [1, 1, 3, 4, 5, 9]
```
{% endraw %}


1. sorted 함수

정렬 대상 : 모든 반복 가능한 객체 (리스트, 튜플, 문자열, 딕셔너리 등)


특징 : 원본 데이터를 변경하지 않고 정렬된 새로운 리스트를 반환한다. 



{% raw %}
```python
numbers = [3, 1, 4, 1, 5, 9]
sorted_numbers = sorted(numbers)  # 정렬된 새로운 리스트 반환
print(sorted_numbers)  # [1, 1, 3, 4, 5, 9]
print(numbers)  # 원본 리스트는 변경되지 않음
```
{% endraw %}


