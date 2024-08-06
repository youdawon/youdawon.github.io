---
layout: post
date: 2024-08-07
title: "The requested URL returned error: 403 에러 해결 방법"
tags: [git, ]
categories: [git, ]
---


새로운 리포지토리 생성 후 Push를 실행하였더니 아래와 같은 에러가 발생했다. 이를 해결하기 위한 방법을 정리했다.


### 단계별 해결 방법

1. **터미널에서 아래 명령어를 실행한다.**

	`user-id`, `user-name`, `repository-name`을 바꿔줘야 한다.


	
{% raw %}
```shell
	git remote set-url origin <https://<user-id>@github.com/><user-name>/<repository-name>.git
```
{% endraw %}


2. **터미널에서 Push를 실행한다.**

	
{% raw %}
```shell
	git push -u origin main
```
{% endraw %}


3. **비밀번호를 입력하면 성공적으로 Push가 완료된다.**
