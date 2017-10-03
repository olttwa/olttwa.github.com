---
layout: post
title: "Load balancing in gRPC for frontend backend communication Part:1"
date: 2017-10-02 23:51:56 +0530
comments: true
categories:
---

We needed a strategy for load balancing incoming requests from our user-facing applications (android and ios) for communication in [gRPC](http://grpc.io/). The reasons for choosing a strategy is mentioned here. Implementation details can be found in Part:2
<!-- more -->

### Need for gRPC

I work at Go-Jek as a product engineer. Here we have multiple use-cases wherein gRPC would make more sense compared to the traditional REST api for communication between frontend-backend. Examples: Customer application live tracking a driver's location, recording location of a driver, chat sessions, etc. We are building a small feature which can even be implemented using REST api. But we decided to use this as an opportunity to explore gRPC.[^1]

### Choosing a load balancing(LB) strategy

I started from the official [load balancing blog](https://grpc.io/blog/loadbalancing)

#### First decision

The first decision was choosing between proxy or client side LB.

In `Proxy LB`, the clients themselves do not know about the backend servers. Clients can be untrusted. This architecture is typically used for user facing services where clients from open internet can connect to servers in a data center. In this scenario, clients make requests to LB. The LB passes on the request to one of the backends, and the backends report load to LB.

In `Client side LB`, the client is aware of multiple backend servers and chooses one to use for each RPC. The client gets load reports from backend servers and the client implements the LB algorithms. In simpler configurations server load is not considered and client can just round-robin between available servers.

This was an easy choice. I chose `Proxy side LB`

Here are cons in `Client side LB`

- Have to implement same logic in multiple languages
- Client cannot be trusted
- Client has to take care of service discovery

For sake of balance, here are cons for `Proxy side LB`

- LB is in the data path
- Higher latency
- LB throughput may limit scalability

Sidenote: `Client Side Lookaside LB` may seem promising but still client will have a lot of logic which could easily be put into the LB.

#### Second decision

Now comes a very difficult choice: `Transport level LB` or `Application level LB`

I chose `Transport level LB` because:

- RPC load doesn't vary a lot among connections (atleast for the current feature)
- Latency is paramount. (Although for a frontend backend communication, I am sure a difference in a few milliseconds at LB level won't matter)
- Far more complex code base for `Application level LB`

Some cons of `Application level LB` are:

- Difficult to scale
- Requires very high performance hardware. (With the maturity of infrastructure at Go-Jek this is not an issue really, but is omttwa😅)

One major reason for choosing `Transport level LB` is that `Application level LB` would have been over-kill for us. For the current feature implementation, we don't need session stickiness which is one of the major reasons people choose `Application level LB`

These blogs helped me weigh pros-cons of `Transport level LB` vs `Application level LB` [^2]

#### Third decision

The highest amount of yak-shaving went in this decision. I knew in my heart all along that I'd use envoyproxy as a LB. To be thorough, I went through a whole lot of blogs[^3] just to be completely sure.

I won't mention the reasons for not choosing HAProxy or NGINX. [Envoyproxy](http://envoyproxy.github.io/) wins hands-down because it fit the following use-cases we needed:

- Our frontend application can switch to HTTP/1.1 based REST apis anytime it wants😍 Envoy supports a gRPC bridge filter that allows gRPC requests to be sent to Envoy over HTTP/1.1. Envoy then translates the requests to HTTP/2 for transport to the target server. The response is translated back to HTTP/1.1[^4]
- If we decide to switch to `Application level LB`, only envoy has support for that in HTTP/2.
- Future of Envoy is promising[^5]
- Has first class support for HTTP/2
- Hot restarts
- Multithreaded architecture
- Service discovery. (Go-Jek is rapidly moving towards an architecture where service mesh is inevitable)

In Part 2, I will illustrate a LB implemented using envoyproxy. WIP can be found here: [github link](https://github.com/olttwa/grpc-envoyproxy)

***
***
I hope this blog was helpful 😀. Please leave your thoughts in the comments section below. You can reach out to me on email: akshat.iitj⚽gmail.com
***
[^1]: Tech isn't putting business at risk just to explore new things. There is a fallback to REST incase gRPC fails. We are pretty mature that ways 😛
[^2]: <https://devcentral.f5.com/articles/why-layer-7-load-balancing-doesnrsquot-suck> <http://wtarreau.blogspot.in/2006/11/making-applications-scalable-with-load.html> <https://www.loadbalancer.org/blog/why-layer-7-sucks/> <https://serverfault.com/questions/233402/layer-4-vs-layer-7-load-balancing> <https://www.nginx.com/resources/glossary/layer-4-load-balancing/> <https://www.nginx.com/resources/glossary/layer-7-load-balancing/>
[^3]: <https://medium.com/@copyconstruct/envoy-953c340c2dca> <https://githubengineering.com/introducing-glb/> <https://githubengineering.com/glb-part-2-haproxy-zero-downtime-zero-delay-reloads-with-multibinder/> <https://www.microservices.com/talks/lyfts-envoy-monolith-service-mesh-matt-klein/> <http://blog.christianposta.com/microservices/00-microservices-patterns-with-envoy-proxy-series/> <https://eng.lyft.com/announcing-envoy-c-l7-proxy-and-communication-bus-92520b6c8191> <https://eng.lyft.com/envoy-7-months-later-41986c2fd443>
[^4]: <https://envoyproxy.github.io/envoy/intro/arch_overview/grpc.html#arch-overview-grpc>
[^5]: There are 42 people working on this actively <https://medium.com/@copyconstruct/envoy-953c340c2dca>

