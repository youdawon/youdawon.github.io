---
layout: post
date: 2024-11-27
title: "[Operating System] Page and Segment"
tags: [Operating System, ]
categories: [Operating System, ]
---


**What is Paging?** 

1. Paging
	1. Paging divides memory into fixed size blocks.
	2. Page : Logical memory is divide into these blocks.
	3. Frames : Physical memory is also divided into blocks of the same size.

**Where is it used?**

1. Virtual Memory :
	1. When a program needs more memory than the system has, the operating system uses paging to move pages between the disk and memory.
	2. Algorithms like FIFO and LRU help decide which page to replace.
2. Operating Systems:
	1. Modern operating systems (like Linux and Windows) use paging to manage memory efficiently and avoid memory waste.

**What is Segmentation?**


Segmentation divides memory into variable size sections, called segments. 


Each segment has a specific purpose, like storing code, data, or the stack. 


**Where is it used?**

1. Compliers : When a program is complied, segmentation helps separate code, data, and stack into different sections.
2. Logical Memory Organization : Programs are easier to understand and manage segments match their logical structure.
