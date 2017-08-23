---
layout: post
title: "[Article Summary] Time Clocks And The Ordering of Events in a Distributed System"
date: 2017-08-21 22:18:51 +0530
comments: true
categories: 
---
This scholarly article defines conditions for total ordering of events in a distributed system. Using the concept of total ordering, we see a way to build distributed systems. The article solves the problem of synchronisation in distributed systems.
<!-- more -->

The author of this article is Leslie Lamport

- First, we see "happened before" relation amongst events occuring in a distributed system. This is called partial ordering.
- Then, we see conditions for logical clocks. An abstract definition of a clock is to assign a number/time to an event at the time it occurred.
- Using the concept of partial ordering and logical clocks, we define total ordering of events. Prioritization of processes is used to break ties.
- Then we see concept of total ordering being used to solve a mutual exclusion problem. In the problem, a fixed collection of processes are sharing a single resource.
- We see how anomalous behaviours can break the algorithm mentioned to solve the above problem.
- One way to prevent anomalous behaviours is to introduce Strong Clocks in the system. The Strong Clock condition is: `If event a has happened before event b (partial ordering defined by special relativity), then timestamp of a is lesser than timestamp of b`
- To quote the paper: *One of the mysteries of the universe is that it is possible to construct a system of physical clocks which, running quite independently of one another, will satisfy the Strong Clock Condition.*
- Then we see conditions for Physical Clocks to ensure they don't go out of synchronization.


***
😀 Thank you for reading this blog. Please leave your thoughts in the comments section below. You can reach out to me on email: akshat.iitj⚽gmail.com
***

