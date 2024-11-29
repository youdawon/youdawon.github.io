---
layout: post
date: 2024-11-27
title: "[Network] DNS(Domain Name System)"
tags: [Network, ]
categories: [Network, ]
---


What is DNS?


It translate domain name to IP address


The process of DNS Resolution

1. A user enters a website’s domain name in their browser.
2. The browser sends a request to the DNS resolver to retrieve the corresponding IP address
3. The DNA resolver attempts to find IP address
	1. Searches its cache for a matching IP address
	2. If the IP address is not found, the resolver queries DNS servers step by step:
		1. Root server : Directs the query to the Top Level Domain Server
		2. TLD server : Directs the query to the authoritative server for the domain
		3. authoritative server : Provides the IP address for the requested domain
4. The resolver returns the IP address to the browser, which then sends a request to the website’s server.
