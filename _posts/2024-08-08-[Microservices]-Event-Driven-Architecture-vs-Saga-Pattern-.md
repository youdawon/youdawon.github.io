---
layout: post
date: 2024-08-08
title: "[Microservices] Event-Driven Architecture vs Saga Pattern "
tags: [Microservices, ]
categories: [Microservices, ]
---


## 1. Saga Pattern


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
