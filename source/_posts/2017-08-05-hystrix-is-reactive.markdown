---
layout: post
title: "Hystrix is reactive"
date: 2017-08-05 08:45:12 +0530
comments: true
published: false
categories: 
---
While using hystrix in your client, you are assuming the downstrea service might misbehave, so it is better to protect your app by setting reasonable timeouts and circuit breakers.
Well, why should the downstream service misbehave at all? Pass along the expected timeout, it should stop wasting/using all the resources once the timeout is reached, and raise an error.
Now, you are not worried about timeouts anymore. So you should only put a check on connection establishment. If you aren't able to establish connection (service is down?) then fail fast.
