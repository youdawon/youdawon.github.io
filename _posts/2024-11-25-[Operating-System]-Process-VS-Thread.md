---
layout: post
date: 2024-11-25
title: "[Operating System] Process VS Thread"
tags: [Operating System, ]
categories: [Operating System, ]
---


### **1. 프로세스란?**

- 독립적인 실행 단위로, 서로 다른 프로세스 간에는 메모리를 공유하지 않음.
- CPU, 메모리 같은 시스템 자원을 사용함.
- **예**: 크롬 브라우저, 스포티파이 등의 실행 중인 애플리케이션.

---


#### **2. 스레드란?**

- 프로세스 내에서 실행되는 작은 실행 단위.
- 하나의 프로세스 안에는 여러 개의 스레드가 존재할 수 있음.
- 같은 프로세스 내의 스레드는 메모리를 공유함.

---


#### **3. 멀티스레드의 장점**

- **CPU를 효율적으로 사용**.
- **여러 작업을 동시에 실행 가능**.
- **예**:
	- 웹 브라우저에서 한 스레드는 페이지 렌더링, 다른 스레드는 사용자 입력 처리.

---


#### **4. 교착 상태 (Deadlock)**

- 교착 상태는 둘 이상의 프로세스나 스레드가 서로 자원을 기다리며 **무한 대기하는 상황**.

#### **교착 상태가 발생하는 4가지 조건**

1. **상호 배제 (Mutual Exclusion)**:
	- 자원이 동시에 여러 프로세스에 의해 사용될 수 없음.
2. **점유 대기 (Hold and Wait)**:
	- 자원을 점유한 상태에서 다른 자원을 요청하며 대기.
3. **비선점 (No Preemption)**:
	- 자원을 강제로 회수할 수 없음.
4. **순환 대기 (Circular Wait)**:
	- 프로세스 간 자원을 원형 구조로 대기.

---


#### **5. 교착 상태 해결 방법**

1. **교착 상태 예방 (Prevention)**:
	- 교착 상태의 발생 조건(4가지) 중 하나를 제거.
		- **예**: 점유 대기를 방지하기 위해, 프로세스가 실행되기 전에 모든 필요한 자원을 미리 할당.
2. **교착 상태 회피 (Avoidance)**:
	- 교착 상태가 발생하지 않도록 시스템 상태를 사전에 분석.
		- **예**: 은행가 알고리즘(Banker's Algorithm)을 사용해 자원을 안전하게 할당.
3. **교착 상태 탐지 및 복구 (Detection and Recovery)**:
	- 교착 상태가 발생했는지 탐지하고, 해결하기 위한 조치를 취함.
		- **탐지**: 자원의 상태를 지속적으로 모니터링.
		- **복구**: 프로세스를 종료하거나 자원을 강제로 회수.
4. **자원 할당 전략 변경**:
	- 자원 요청 순서를 정하여 순환 대기를 방지.
		- **예**: 항상 특정 순서대로 자원을 요청하도록 설계.
