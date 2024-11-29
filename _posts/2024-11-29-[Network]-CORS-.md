---
layout: post
date: 2024-11-29
title: "[Network] CORS "
tags: [Network, ]
categories: [Network, ]
---

1. CORS(Cross-Origin Resource Sharing)

The browser restricts access to resources from a different origin for security reasons.


An origin is considered different if the **protocol**, **domain**, or **port** differs.

1. Preflight Request?

The browser issues an OPTIONS request, known as preflight request, to verify the allowed methods, headers, and origins.


**"How did you solve CORS problems?"**


> "In the systems I worked on, PUT and DELETE methods were restricted, likely configured at the infrastructure level, such as Nginx or Apache. While this wasn’t directly about CORS, it helped avoid Preflight Requests and simplified API usage. Instead, we used POST for updates and deletions, ensuring smooth cross-origin communication."


**"I have seen CORS issues resolved in our system by adding the** **`Access-Control-Allow-Origin "*"`** **configuration in the Apache server. While I didn't configure it myself, the infrastructure team implemented it, and I understood how this allowed cross-origin requests during development."**

