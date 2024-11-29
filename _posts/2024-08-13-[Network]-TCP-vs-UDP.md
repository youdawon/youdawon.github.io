---
layout: post
date: 2024-08-13
title: "[Network] TCP vs UDP"
tags: [Network, ]
categories: [Network, ]
---


### **1. TCP (Transmission Control Protocol)**

- **Reliable**: Makes sure the client gets all packets in the correct order.
- **Handshake**: Uses **3-way handshake** to connect.
- **Disconnect**: Ends with **4-way handshake** after sending data.
- **Example**: File transfer, web browsing.

#### **1. TCP (User Diagram Protocol)**


ex) streaming website, online game

1. **Fast**: Faster than TCP, no connection setup.
2. **Unreliable**: Doesn't guarantee all packets arrive or stay in order.
3. **Example**: Online games, live video streaming.

#### 3. TCP 3-Way handshake

1. step 1 : Client → Server(SYN)
	1. The client sends a SYN packet to the server, requesting to establish a connection.
2. step 2 : Server → Client(SYN + ACK)
	1. The server acknowledges the client’s request by sending a SYN packet back, along with an ACK to confirm it received the client’s SYN
3. step 3 : Client → Server(ACK)
	1. The client acknowledges the server’s response by sending an ACK packet.
	2. At this point, the connection is established, and data transfer can begin.

#### 4. TCP 4-Way handshake

1. step 1 : Client → Server(FIN)
	1. The client sends a FIN packet to the server, requesting to terminate a connection.
2. step 2 : Server → Client(ACK)
	1. The server acknowledges the client’s request by sending an ACK packet. At this point, the client stops sending data.
3. step 3 : Server → Client(FIN)
	1. Once the server is ready to terminate its connection, it sends its own FIN packet to the client.
4. step 4 : Client → Server(ACK)
	1. The client acknowledges the server’s FIN packet by sending an ACK. The connection now fully terminated.
