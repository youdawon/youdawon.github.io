---
layout: post
date: 2024-12-21
title: "[Python] FastAPI"
tags: [Python, ]
categories: [Python, ]
---


### FastAPI의 장점

- 고성능 : 비동기 기능을 지원하며 매우 빠름
- 자동 문서화 : swagger UI 및 reDoc을 통해 API를 자동으로 생성
- 타입 힌트 : Python의 타입 힌트를 적극 활용하여 코드의 가독성을 높이고 오류를 줄임
- 간편한 데이터 검증 : Pydantic을 활용해 입력 데이터를 쉽게 검증할 수 있음

#### 주요 구성 요소 

- Path Operation : @app.get()과 같은 데코레이터로 요청 메서드를 정의
- Dependency Injection :

#### FastAPI에서 이벤트 루프의 역할

- FastAPI는 내부적으로 uvicorn을 사용하여 이벤트 루프를 관리
- async def 함수는 이벤트 루프에서 실행되며 비동기 작업을 관리

[asyncio.run](http://asyncio.run/) vs await


FastAPI 내부에는 이미 실행 중인 이벤트 루프를 사용하므로 asyncio.run() 대신 await를 사용한다. 

