---
layout: post
date: 2024-12-21
title: "[Python] async와 await"
tags: [Python, ]
categories: [Python, ]
---


### async:

- async는 비동기 함수를 정의할 때 사용하는 키워드이다.
- 비동기 함수는 다른 작업이 끝날 때까지 기다리지 않고 실행 가능한 작업으로 넘어갈 수 있다.
- 동작 방식 :
	- 일반 함수는 호출 즉시 실행되지만 async로 정의된 함수는 호출해도 바로 실행되지 않는다.
	- 대신 코루틴(coroutine) 객체를 반환하며, 실행은 이벤트 루프가 담당한다. 즉, 이벤트 루프가 실행 스케줄에 따라 작업을 처리하지 전까지는 실행되지 않는다.

#### await:

- await는 비동기 함수를 호출할 때 사용하는 키워드이다.
- 비동기 함수 호출은 작업이 완료될 때까지 대기하며, 그동안 다른 작업이 수행될 수 있다.

#### 이벤트 루프(Event loop):

- 정의 :
	- Python의 비동기 처리는 이벤트 루프라는 메커니즘으로 동작한다.
	- 이벤트 루프는 완료되지 않은 비동기 함수(코루틴)를 추적하며, 실행 가능한 상태가 되면 실행한다.
	- 주로 I/O 바운드 작업을 처리하는 데 유용하다.
- 작동 방식:
	- 비동기 작업(예 : fetch_data)을 등록
	- 작업이 완료될 때까지 대기하지 않고 다른 작업으로 넘어감
	- 대기 중인 작업이 완료되면 결과를 받아 다음 작업을 실행

	
{% raw %}
```python
	import asyncio
	
	async def fetch_data():
	    await asyncio.sleep(2)
	    return "Data fetched"
	
	async def main():
	    result = await fetch_data()
	    print(result)
	
	asyncio.run(main())
```
{% endraw %}



#### asyncio.Queue:

- Python 내장 비동기 큐
- 단일 프로세스 환경에서 사용

#### asyncio.run()과의 차이 

- asyncio.run()은 이벤트 루프가 없는 환경에서 새로운 이벤트 루프를 생성하여 비동기 코드를 실행할 때 사용한다.
- FastAPI같은 프레임워크는 자체적으로 이벤트 루프를 관리하므로 asyncio.run()을 사용하지 않아도 된다.
