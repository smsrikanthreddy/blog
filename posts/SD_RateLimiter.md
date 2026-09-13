---
aliases:
- /markdown/2026/09/13/RateLimiter
categories:
- SD
date: '2026-09-13'
description: Rate Limiter
image: /images/SD/RateLimiter.png
layout: post
title: System Design Rate Limiter
toc: true

---


## What is Rate Limiter
Rate Limiter is one of the classic System Design interview question. It is a very important concept in system design and it is used in many real world applications. Rate Limiter helps in controlling the client's rate of requests to the server to prevent the server from being overwhelmed by too many requests.

Example :- 
1. to limit password change trials for 3 times in a day
2. To allow customer to query/search for 2 times in a second like google search etc.
3. To limit number of requests for a client to twitter for 1000 requests per day. etc.

Rate limiter helps in DOS (Denial of Service) attacks, if allowed unrestricted requests, the resources will get exhausted by the number of client requests. The backend systems may crash under heavy loads, leading to system downtime and poor user experience. 

Where to implement Rate Limiter :- 

Rate Limiter can be implemented in many levels, each has its own advantages and disadvantages.

1. Client Level :- 
    - Advantages :- 
        - Easy to implement
        - No additional overhead on the server
    - Disadvantages :- 
        - Not reliable as clients can bypass the rate limiter

2. Server/App Level :- 
    - Advantages :- 
        - More reliable than client level
        - Can handle complex rate limiting logic
    - Disadvantages :- 
        - Additional overhead on the server

3. Middleware/API Gateway Level :- 
    - Advantages :- 
        - Most reliable and the best way
        - Can handle complex rate limiting logic
    - Disadvantages :- 
        - Most complex to implement
        - Additional overhead on the API Gateway

4. Database Level :- 
    - Advantages :- 
        - Most reliable
        - Can handle complex rate limiting logic
    - Disadvantages :- 
        - Most complex to implement
        - Additional overhead on the Database

Without Rate Limiter Architecture : -

