---
layout: post
date: 2024-08-12
title: "[SystemDesign-Youtube] 설계 시 고려해야할 사항"
tags: [SystemDesign, Architecture, Youtube, ]
categories: [SystemDesign, Problems, Youtube, ]
---

1. 유투브의 썸네일은 어디에 저장되는 것이 좋을까?

당연히 Amazon S3를 생각했는데 Bigtable이라는 데이터베이스에 썸네일을 저장하여 빠르게 조회할 수 있도록 하는 방법이 있다. 여기서 썸네일을 저장한다는 것은 썸네일의 url이 아닌 썸네일 자체를 말하는 것이다. 


데이터베이스에 어떻게 썸네일을 저장할 수 있을까?


일단 각 썸네일은 5KB 미만의 크기를 가지고 있다고 가정하자. Bigtable은 데이터의 크기가 10MB 미만으로 정해져있기 때문에 이미지의 크기가 작을 경우 저장이 가능하다. 그렇다면 어떤 식으로 데이터가 저장되는 것일까?


Bigtable은 썸네일 이미지를 Base64로 인코딩하거나, 바이너리 데이터로 저장할 수 있다. 이 경우 각 행(row)에 해당하는 비디오 ID에 대해 썸네일 이미지 데이터가 하나의 열(column)에 저장된다. 

1. 비디오는 어디에 저장하는 것이 좋을까?

이것도 역시 Amazon S3를 생각했는데 비디오와 같은 대용량 파일을 저장할 수 있는 분산 저장 시스템이 존재한다. HDFS와 GlusterFS가 그것이다. 

undefined