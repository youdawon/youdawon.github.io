---
layout: post
date: 2024-08-09
title: "[SystemDesign-Facebook Messenger] System flows"
tags: [SystemDesign, Architecture, FacebookMessenger, ]
categories: [SystemDesign, Problems, FacebookMessenger, ]
---

1. **User Interaction**:
	- **Users** connect to the system via WebSockets, with connections managed by a **Load Balancer** that directs traffic to the appropriate **Chat Servers**.
2. **Connection Management**:
	- A **WebSocket handshake** is performed to establish the connection.
	- **Heartbeat messages** are periodically sent by the **Chat Servers** to ensure the connection remains active.
3. **Real-Time Communication**:
	- **Chat Servers** handle the sending and receiving of messages, and manage real-time communication between users.
	- **Presence Servers** track user status (online/offline) and update other users accordingly.
4. **Message Processing and Storage**:
	- **Message Sync Queue** ensures messages are processed in the correct order before being stored.
	- **Databases** (HBase for messages and SQL for metadata) store the processed data, with a **Cache** used for quick access to frequently used data.
5. **Notification Handling**:
	- **Notification Servers** send push notifications to offline users to alert them of new messages.

![0](/assets/img/2024-08-09-[SystemDesign-Facebook-Messenger]-System-flows.md/0.png)

