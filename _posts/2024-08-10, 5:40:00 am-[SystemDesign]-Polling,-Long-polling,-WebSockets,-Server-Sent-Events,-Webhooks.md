---
layout: post
date: 2024-08-10, 5:40:00 am
title: "[SystemDesign] Polling, Long-polling, WebSockets, Server-Sent Events, Webhooks"
tags: [SystemDesign, Architecture, ]
categories: [SystemDesign, Basics, ]
---


### 1. Polling


Polling is a standard technique where a client repeatedly requests a server to check for new or updated data. If no updates are available, the server sends an empty response.

1. **Technology Used**: AJAX (Asynchronous JavaScript and XML) or `setInterval` in JavaScript to repeatedly send HTTP requests to the server.
2. **Example**: A weather app that checks for updated weather information every 15 minutes.
3. **Pros**:
	- Simple and easy to implement on the client side.
4. **Cons**:
	- Generates a lot of unnecessary traffic if there are no new updates.
	- Delays in receiving updates.

#### 2. Long-Polling


In long-polling, the client requests data from the server, but if there is no new data, the server holds the connection open until an update is available, then sends the data.

1. **Technology Used**: AJAX or Fetch API in JavaScript with a technique to keep the connection open until the server has new data.
2. **Examples**:
	- Real-time notifications.
	- Chat applications.
	- Live updates (e.g., dashboards).
3. **Pros**:
	- Faster updates than regular polling.
	- Fewer requests than polling, reducing unnecessary traffic.
4. **Cons**:
	- Can be resource-intensive on the server, especially with many clients.

#### 3. WebSockets


WebSockets provide full-duplex communication channels over a single TCP connection, allowing both the client and server to send data at any time. The connection is established through a WebSocket handshake.

1. **Technology Used**: WebSocket protocol, supported by WebSocket API in JavaScript and WebSocket libraries on the server side (e.g., `ws` for Node.js, or built-in support in frameworks like Spring Boot).
2. **Examples**:
	- **Online Multiplayer Games**: Players’ movements and actions are sent and received in real-time.
	- **Live Financial Trading Platforms**: Stock prices and trading information are updated instantly for users.
3. **Pros**:
	- Real-time, bidirectional communication.
	- Efficient with low latency, suitable for live interactions.
4. **Cons**:
	- More complex to implement and manage than polling or long-polling.
	- Firewall and proxy issues can arise due to the persistent connection.

#### 4. Server-Sent Events (SSE)


With Server-Sent Events, the client establishes a persistent connection with the server, which the server uses to push updates. The client cannot send data back through the same connection and would need to use a separate channel for that.

1. **Technology Used**: Server-Sent Events (SSE) API in JavaScript, supported natively by most modern browsers, and server-side technologies like Node.js, Django, or Spring.
2. **Examples**:
	- **Live News Feeds**: A news website updating headlines in real-time as they are published.
	- **Stock Tickers**: Real-time stock price updates displayed on a web page.
3. **Pros**:
	- Simple to implement for unidirectional data flow.
	- Built-in support in modern browsers.
4. **Cons**:
	- Limited to one-way communication from the server to the client.
	- Not suitable for scenarios requiring two-way communication.

#### 5. Webhooks


Webhooks are user-defined HTTP callbacks triggered by specific events on a server. The server sends data to a pre-configured URL when an event occurs, without the client having to request it.

1. **Technology Used**: Standard HTTP/HTTPS protocol for sending POST requests to the client’s URL.
2. **Examples**:
	- **Payment Processors**: Notify your application when a payment is completed.
	- **Messaging Services**: Notify your application when a new message is received.
	- **CI/CD Systems**: Trigger a deployment process when new code is pushed to a repository.
	- **CRM Systems**: Sync customer data between different platforms when a new customer is added or updated.
3. **Pros**:
	- Provides real-time updates.
	- Reduces network traffic and server load.
4. **Cons**:
	- The client must be capable of receiving and processing incoming HTTP requests.
	- Security concerns, such as ensuring the authenticity of the incoming webhook data.
