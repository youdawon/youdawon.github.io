---
layout: post
date: 2024-08-13
title: "[SystemDesign - Typeahead Suggestion] Scale Estimation"
tags: [SystemDesign, Architecture, Typeahead Suggestion, ]
categories: [SystemDesign, Problems, Typeahead Suggestion, ]
---


5,000,000,000 searches everyday. 



{% raw %}
```text
5,000,000,000 % (24*60*60) = 57,780(abouth 60K queries/sec)
```
{% endraw %}



#### 1. Storage Estimation 


3words, length of a word is 5 characters, 2 bytes to store a character, 100,000,000 unique terms



{% raw %}
```text
3words * 15length * 2bytes * 100,000,000 = 3GB
```
{% endraw %}



If it grow every day about 2% new queries



{% raw %}
```text
3GB + (0.02 * 3GB * 365days) = 25GB
```
{% endraw %}


