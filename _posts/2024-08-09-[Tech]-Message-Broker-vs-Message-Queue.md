---
layout: post
date: 2024-08-09
title: "[Tech] Message Broker vs Message Queue"
tags: [MessageQueue, MessageBroker, ]
categories: [Tech, ]
---


Dropbox 설계 문제 풀면서 갑자기 헷갈려서 정리해보았다. 


#### **1. Message Broker**


Stores and forwards messages from producers to consumers, ensuring reliable delivery even when consumers are not immediately available. Operates mainly on a First-In-First-Out (FIFO) basis.


#### **2. Message Queue**


Extends the functionality of a message queue by routing, transforming, and filtering messages. It manages complex communication patterns like Publish/Subscribe, directing messages to the appropriate consumers based on predefined rules.


#### **3. Example: E-commerce Order Processing**


In an e-commerce platform:

1. **Message Queue**: When an order is placed, an "Order Created" message is sent to the queue, ensuring it’s stored until services are ready to process it.
2. **Message Broker**:
	- Routes the "Order Created" message to the payment service.
	- Sends the same message to inventory management to update stock.
	- Once payment is confirmed, it forwards a "Payment Completed" message to the shipping service and triggers an email notification to the customer.

#### **4. Common Tools**

- **Message Brokers**: RabbitMQ, Apache Kafka, ActiveMQ, Amazon SNS, Azure Service Bus
- **Message Queues**: Amazon SQS, Redis, Azure Queue Storage
