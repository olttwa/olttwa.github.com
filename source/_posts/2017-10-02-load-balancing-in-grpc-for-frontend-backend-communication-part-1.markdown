---
layout: post
title: "Load balancing in gRPC for frontend backend communication Part:1"
date: 2017-10-02 23:51:56 +0530
comments: true
categories:
---

We needed a strategy for load balancing incoming requests from our user-facing applications (android and ios) for communication in gRPC (http2). The reasons for choosing a strategy is mentioned here. Implementation details will be found in Part:2
<!-- more -->

### Need for gRPC

I work at Go-Jek as a product engineer. Here we have multiple use-cases wherein gRPC would make more sense compared to the traditional REST api for communication between frontend-backend. Examples: Customer application live tracking a driver's location, recording location of a driver, chat sessions, etc. We are building a small feature which can even be implemented using REST api. But we decided to use this as an opportunity to explore gRPC.

### Choosing a load balancing(LB) strategy

#### First decision

I obviously started from the official load balancing blog: https://grpc.io/blog/loadbalancing

The first decision was choosing between proxy or client side LB.

Proxy LB can be defined as: `The clients themselves do not know about the backend servers. Clients can be untrusted. This architecture is typically used for user facing services where clients from open internet can connect to servers in a data center. In this scenario, clients make requests to LB. The LB passes on the request to one of the backends, and the backends report load to LB.`

Client side LB can be defined as: `the client is aware of multiple backend servers and chooses one to use for each RPC. The client gets load reports from backend servers and the client implements the load balancing algorithms. In simpler configurations server load is not considered and client can just round-robin between available servers.`

This was an easy choice. I chose Proxy side LB.

Here are cons in client side LB:

- have to implement same logic in multiple languages
- client cannot be trusted
- client has to take care of service discovery

For sake of balance, here are the cons for proxy side LB:

- LB is in the data path
- Higher latency
- LB throughput may limit scalability

#### Second decision

Now comes a very difficult choice: Transport level LB or Application level LB

I chose transport level LB because:

- RPC load doesn't vary a lot among connections as of now
- Latency is paramount. (Although for a frontend backend communication, I am sure a latency difference in a few milliseconds at LB level won't matter)
- Far more complex code base for Application level LB

Some cons of Application level LB are:

- Difficult to scale.
- Requires very high performance hardware. (Not that with the maturity of infrastructure at Go-Jek this is an issue)

Another main reason for choosing Transport level LB is that Application level LB would have been over-kill for us. For the current feature implementation, we don't need session stickiness which is one of the major reasons people choose Application level LB.

These blogs helped weigh pros-cons of Transport level and Application level LB - https://devcentral.f5.com/articles/why-layer-7-load-balancing-doesnrsquot-suck http://wtarreau.blogspot.in/2006/11/making-applications-scalable-with-load.html https://www.loadbalancer.org/blog/why-layer-7-sucks/ https://serverfault.com/questions/233402/layer-4-vs-layer-7-load-balancing  https://www.nginx.com/resources/glossary/layer-4-load-balancing/  https://www.nginx.com/resources/glossary/layer-7-load-balancing/  

#### Third decision

The highest amount of yak-shaving went in this decision. I knew in my heart all along that I'd use envoyproxy as a LB. To be thorough, I went through a whole lot of blogs just to be completely sure.

I won't mention the reasons for not choosing HAProxy or nginx. Envoyproxy wins hands-down because it fit the following use-cases we needed:

- Our frontend application can switch to HTTP/1 based REST apis anytime it wants. :heart-eyes Envoy's grpc-bridge will translate client's request to HTTP/2 and communicate to the relevant backend; then translate response from backend to HTTP/1 and respond to client.
- Future of Envoy is promising. There are 42 people (from Lyft+Google) working on this actively
- Has first class support for HTTP/2
- hot restarts
- multithreaded architecture
- Service discovery

Blogs for envoy: https://medium.com/@copyconstruct/envoy-953c340c2dca   https://githubengineering.com/introducing-glb/  https://githubengineering.com/glb-part-2-haproxy-zero-downtime-zero-delay-reloads-with-multibinder/  https://www.microservices.com/talks/lyfts-envoy-monolith-service-mesh-matt-klein/    http://blog.christianposta.com/microservices/00-microservices-patterns-with-envoy-proxy-series/   https://eng.lyft.com/announcing-envoy-c-l7-proxy-and-communication-bus-92520b6c8191 https://eng.lyft.com/envoy-7-months-later-41986c2fd443


In Part 2, I will illustrate a LB implemented using envoyproxy. WIP can be found here: github-link

- talking to team: gopay bola solve 2 problems: lb and http conn pooling. acc to me, frontend needs to check 2 problems: battery effect and slow internet speed issues. should we implement backend in golang? java has most support and documentation around it. FYI. i tried implementing a transport level load balancing between the client and server mentioned here: github-grpc-example. Here is as far as I could reach: github link (Fair warning for anybody trying to enhance it: documentation of envoy sucks!)

***
***
I hope this blog was helpful 😀. Please leave your thoughts in the comments section below. You can reach out to me on email: akshat.iitj⚽gmail.com
***
