---
layout: post
title: How to setup a High Availability Redis cluster.
---

## In this blog we will go through the steps to setup a [Redis](https://redis.io/) cluster (Redis 2.8+) on Windows with High Availability.![Icon representing Redis](https://redis.io/images/redis-white.png)
---
##### Redis is an in-memory datastore. When multiple instances of an application want to share data with each other, Redis can be a viable alternative. 
---
##### Redis introduces a concept of _Sentinel_ which helps achieve High Availability. 

##### What is a Sentinel?
![Image of a guard Dog](../images/dog-security-guard.jpg)

- I like to think of Sentinel as a **Watchman**. Someone who keeps a watch on a running Redis server. Sentinel is actually a Redis server which is run with the ```--sentinel flag```. We can start the regular redis server by firing ```redis-server nameOfConfigfile.conf```. When we want to start a _Sentinel_ we will issue a command ```redis-server pathToSentinelConfig.conf --sentinel ```

##### What does a Sentinel do?
- Keep an eye on the Redis servers

- Provides the details(host and port) of the current Redis Server and current Redis slaves

- Be in touch with other Sentinels (Watchmen). There will generally be multiple instances of Sentinels running on different machines. All the Sentinels will be in touch with each other and all of them are equal. There is no _master_ or _slave_ Sentinel.

- When a particular Redis server fails( goes down):
  -  Sentinels decide that the current Redis Server which is a master has gone down. Just as there is a concept of quorum in elections, there is a _quorum_ while evaluating if the Redis master is down.
  -  Sentinels start a process called as _electing the new master_ where an existing slave is promoted to a master and other slaves are configured to talk to this newly elected master.
  
