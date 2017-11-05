---
layout: post
title: How to setup a High Availability Redis cluster
---
![Icon representing Redis](https://redis.io/images/redis-white.png)
## In this blog we will go through the steps to setup a [Redis](https://redis.io/) cluster with High Availability
---
### Redis is an in-memory datastore. When multiple instances of an application want to share data with each other, Redis can be a viable alternative. 
---
### This article is applicable for Redis 3.0 and above. Redis introduces a concept of _Sentinel_ which helps achieve High Availability. 

#### What is a Sentinel:
- I like to think of Sentinel as a **Watchman**. Someone who keeps a watch on a running Redis server. Sentinel is actually a Redis server which is run with the ```--sentinel flag```. We can start the regular redis server by firing ```redis-server nameOfConfigfile.conf```. When we want to start a _Sentinel_ we will issue a command ```redis-server pathToSentinelConfig.conf --sentinel ```
