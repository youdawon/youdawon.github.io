---
layout: post
date: 2024-08-07
title: "[SystemDesign-Instagram] Capaity Esitmation"
tags: [SystemDesign, Architecture, Instagram, ]
categories: [SystemDesign, Problems, Instagram, ]
---


total users : 500,000,000


active users: 1,000,000 per day


23 new photos every second, 2M new photos every day


average photo file size : 200KB

1. Data Storage Estimation

	
{% raw %}
```text
	total space for 1 day of photos : 200KB * 2,000,000 = 400,000,000KB(400GB)
	total space required for 10 years : 400GB * 30 * 12 * 10 = 1440TB
```
{% endraw %}


2. Database requirements

	(1) Users


	
{% raw %}
```text
	daily : user_id(4bytes) + name(20bytes) + email(32bytes) 
	+ date_of_birth(4bytes) + creation_date(4bytes) 
	+ last_login_date(4bytes) = 68 bytes
	68(bytes) * 500,000,000(total users) = 34GB
```
{% endraw %}



	(2) photo


	
{% raw %}
```text
	daily : photo_id(4bytes) + user_id(4bytes) + photo_path(100bytes) 
	+ creation_date(4bytes) = 112bytes 
	112bytes * 2,000,000 = 224MB
	for 10 years : 224 * 365 * 10 = 0.8TB
```
{% endraw %}



	(3) UserFollow


	
{% raw %}
```text
	on average of each user follows 500 users
	500,000,000 * 500 * 8 = 2TB
```
{% endraw %}


