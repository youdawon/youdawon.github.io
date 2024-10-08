---
layout: post
date: 2024-08-16
title: "[SystemDesign] Kafka 백프레셔(Back Pressure) 해결 방안"
tags: [System Design, Kafka, ]
categories: [System Design, Basics, ]
---


백프레셔(Backpressure)는 데이터 처리 시스템에서 생산자가 소비자보다 더 빠르게 데이터를 생성할 때 발생하는 현상으로, 데이터가 처리되지 않고 쌓이면서 시스템에 과부하가 걸리는 상황을 말한다.


#### Kafka에서의 백프레셔


Kafka에서도 백프레셔가 발생할 수 있는데, 주로 다음과 같은 상황에서 발생한다:

1. **프로듀서가 너무 빠르게 메시지를 전송할 때**:
	- 프로듀서가 Kafka 브로커로 메시지를 너무 빨리 보내면, 브로커의 큐에 메시지가 쌓이게 된다. 브로커가 한계에 도달하면 더 이상 메시지를 받아들이지 못하고, 프로듀서에서 오류가 발생할 수 있다.
2. **컨슈머가 느리게 처리할 때**:
	- 컨슈머가 메시지를 처리하는 속도가 느리면, 브로커의 큐에서 메시지가 처리되지 않고 쌓이게 된다. 시간이 지나면서 큐가 가득 차게 되고, 결국 프로듀서가 메시지를 더 이상 전송하지 못하게 된다.

#### 백프레셔 대응 전략


Kafka에서는 백프레셔를 관리하기 위해 몇 가지 전략을 사용할 수 있다:

1. **프로듀서 측에서의 조절**:
	- **배치 전송 크기 조절**: 프로듀서가 한 번에 전송하는 메시지 배치 크기를 줄여서 브로커에 과부하가 걸리지 않도록 할 수 있다.
	- **재시도 설정**: 전송 실패 시 재시도하는 횟수와 간격을 조절하여 백프레셔를 완화할 수 있다.
2. **브로커 측에서의 조절**:
	- **큐 크기 제한**: 브로커의 큐 크기를 적절하게 설정하여 과부하를 방지하고, 큐가 가득 찼을 때 메시지 전송을 거부하는 방식으로 대응할 수 있다.
3. **컨슈머 측에서의 조절**:
	- **병렬 처리**: 컨슈머가 더 많은 파티션에서 동시에 메시지를 소비하게 하여 처리 속도를 높일 수 있다.
	- **오프셋 관리**: 느린 컨슈머는 오프셋을 잘 관리하여 재처리할 메시지의 양을 줄이고, 처리 속도를 높일 수 있다.
4. **스루풋 조절(Throttling)**:
	- 프로듀서나 컨슈머의 처리 속도를 제한하여, 시스템이 감당할 수 있는 수준으로 조절할 수 있다. 이를 통해 브로커가 과부하에 걸리지 않도록 예방할 수 있다.
5. **모니터링 및 자동 스케일링**:
	- Kafka 클러스터와 컨슈머 그룹의 상태를 모니터링하고, 필요시 자동으로 확장하여 더 많은 리소스를 사용해 백프레셔를 완화할 수 있다.
