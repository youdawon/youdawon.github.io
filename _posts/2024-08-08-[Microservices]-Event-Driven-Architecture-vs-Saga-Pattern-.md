---
layout: post
date: 2024-08-08
title: "[Microservices] Event-Driven Architecture vs Saga Pattern "
tags: [Microservices, ]
categories: [Microservices, ]
---


예전 Microservices 구조의 프로젝트를 할 때 공부했던 부분을 다시 정리해봤다. 공부할 땐 사실 무슨말인지 잘 몰랐는데 실제로 서비스에 적용해보고 공부하면서 서비스 구조를 생각해보니 더 잘 이해가 된다. Saga Pattern이랑 Event-Driven Architecture의 차이가 헷갈렸는데 내가 개발한 부분은 Event-Driven Architecture에 가까운 것으로 보인다. 


### 1. Saga Pattern


The Saga is a design pattern for managing distributed transactions. Instead of a single monolithic transaction, a Saga splits the transaction into a series of smaller, isolated steps, each with its own compensating transaction to undo the operation if necessary.


#### 1.1 Use Cases

- Financial transactions involving multiple services (e.g., order processing in e-commerce).

#### 1.2 Example

1. **Order Service** creates an order.
2. **Payment Service** processes the payment.
3. **Inventory Service** reserves the items.
4. **Shipping Service** prepares for shipment.
5. If any step fails, compensating actions are taken to undo the previous steps.

### 2. Event-Driven Architecture


Event-Driven Architecture is a design pattern where services communicate through events. An event is a significant change in state, such as an item being added to a shopping cart. Services react to these events asynchronously, enabling loose coupling and high scalability.


#### 2.1 Use Cases

- Real-time data processing (e.g., IoT applications, user activity tracking).
- Systems requiring high scalability and flexibility (e.g., microservices architectures).

#### 2.2 Example

1. **User Service** creates a user account and publishes a `UserCreated` event.
2. **Email Service** listens for `UserCreated` events and sends a welcome email.
3. **Analytics Service** listens for `UserCreated` events and updates user statistics.
