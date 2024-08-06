---
layout: post
date: 2024-08-07
title: "The requested URL returned error: 403 에러 해결 방법"
tags: [git, ]
categories: [git, ]
---


매번 까먹는 것 같아서 정리해둠.


새로운 리포지토리 생성 후 push를 실행 하였더니 아래와 같은 에러가 발생했다.


1. 터미널에서 아래 명령어를 실행한다.


user-id, user-name, repository-name을 바꿔줘야 한다.


git remote set-url origin https://<user-id>@github.com/<user-name>/<repository-name>.git


2. 터미널에서 push를 실행한다.


git push -u origin main


3. 비밀번호를 입력하면 성공적으로 push가 완료된다.

