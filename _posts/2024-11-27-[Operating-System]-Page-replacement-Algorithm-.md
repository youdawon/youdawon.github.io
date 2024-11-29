---
layout: post
date: 2024-11-27
title: "[Operating System] Page replacement Algorithm "
tags: [Network, ]
categories: [Network, ]
---


**If a page fault occurs in virtual memory, the operating system removes an existing page to load the required page.**


Page Replacement Algorithm

1. FIFO

	Remove the oldest memory page fist


	Disadvantage: Frequently used pages might be removed.

2. LRU (Least Recently Used)

	Remove the least recently used memory page first. 


	Implementation : Track recently used pages. 


	Disadvantage : Require additional memory to track the record and is expensive to maintain usage records. 

3. Optimal

	Remove the memory page that the will be used the least in the future.


	Disadvantage : Requires knowledge of future page references, which is impossible to predict in practice. 

4. Clock(Second Chance)

	Remove the oldest memory page first, but use a reference bit to check if the page has been recently used. 


	If the reference bit is 1(recently used), give the page a “second chance” by resetting the bit to 0 and moving to the next page. 


	If the reference bit is 0(not recently used, the page is replaced. 


	Advantage : Combines simplicity of FIFO with some efficiency of LRU


	Disadvantage : Still requires a circular scan, which adds overhead. 

