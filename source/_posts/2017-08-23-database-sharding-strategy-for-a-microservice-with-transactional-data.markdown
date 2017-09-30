---
layout: post
title: "Database Sharding Strategy for a Microservice with Transactional Data"
date: 2017-08-23 14:30:40 +0530
published: false
comments: true
categories: 
---

- What is transactional data? Examples of applications with transactional data.
- Describe strategy at Go-Jek to take care of such data.
- There are 2 strategies for it. 1 is application level sharding. The other is db level sharding.
- Briefly describe application level sharding used in abs-go.
- List reasons for decision of application level sharding in abs-go
- Describe the process for db level sharding using pg_partman.
- Discuss the problems with queries in DFS.
- check mail of Ranjan.
- You can use optimize_query_constraint when the query is time based.
- Application level sharding - the underrated weapon and assumed to be super complex to implement compared db level sharding.
- Remember that this problem can be solved in simpler ways using nosql db like cassandra.
