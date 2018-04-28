---
layout: post
title: "To Log Or Not To Log"
date: 2018-04-28 21:23:08 +0530
comments: true
categories:
---
Anyone who has been on production support can testify that time taken to resolve issues is indirectly proportional to effectiveness of application logs. To understand what to log and more importantly what **not**, read ahead!

<!-- more -->

Logging is to engineers as X-ray is to doctors. With respect to an application, logging brings visibility under the hood.

Understanding what to log and what **not** is paramout. An application at my company handling throughput of 250k rpm was logging every request. Converging on the root cause of an issue from logs would be like finding a needle in a haystack.

To Log or Not To Log is an objective question if looked from a production support standpoint. Log levels help us maintain sanity. Let's understand the role of levels in logging.

## Log Levels

When an application logs, it's sending a message to it's owners. Messages have different meanings and warrant different actions under different levels.

The severity of log levels in increasing order is: [debug](#debug) < [info](#info) <[warn](#warn) <[error](#error) <[fatal](#fatal) < [panic](#panic). Levels can be configured for an application to maintain sanity of logs. Application will only log messages of higher severity than configured log levels.

We'll take example of an `Order Management Service aka OMS` to understand what should be logged. It handles orders for a ride-hailing service. The flow of OMS is: customer requests for a ride -> OMS assigns driver to the ride -> ride reaches completion -> driver gets payment for the ride.

#### Info

These messages are lifecycle events. They highlight the progress of an application.

`Example:` *application start/stop*; *order completion in OMS*

#### Debug

These messages help in figuring out weird stuff. Logging at *debug* level means tracking state changes at every step of an application.

`Example:` Let's say a driver accepts order ABC, but OMS assigns order DEF. To find root cause of issues, log all events: *creation of order*, *list of eligible drivers for an order*, *acceptance of booking by a driver*, *saving state in OMS*

#### Warn

These messages are potentially harmful situations. These issues need to be fixed but may not require immediate intervention.

`Example:` Let's say OMS talks to a payment service for paying drivers. On breach of SLA with payment service, OMS will timeout and retry the request. Log at warning level: *payment service SLA breached. Retrying*

#### Error

These messages are of considerable importance. Log at *error* level when normal flow of execution is blocked, and fixing the issue requires human intervention. You should keep an eye out for error logs; so you can fix issues manually to maintain consistency in system.

`Example:` If OMS has exhausted driver payment retries to payment service, Log *Error paying driver XYZ for order ABC*. Later pay the driver manually.

#### Fatal

These messages are severe events that might cause the application to terminate. There should be immediate action when application logs at fatal level.

`Example:` *Running out of disk space*, *total loss of network connectivity*

#### Panic

These messages are exceptional scenarios which should be fixed immediately. Log this when application panics and terminates or recovers

`Example:` *database wasn't configured*, *number divided by by 0*

## Plan of Action

In production environment, ideally, application should only log on severity of **warn level** and above. Application should log at **debug and info level** only in staging, integration and UAT environment for the benefit of engineers and QAs.

**warn level** issues should be tracked and fixed. **error level** issues should be fixed ASAP. **fatal and panic level** issues warrant immediate attention.

## Log Retention

Retaining logs beyond 3 days defeats the purpose of logs. Ideally logs shouldn't be retained beyond 24 hours, but considering no work on weekends, adding 48 hours should be more than enough.

***
***

I hope this blog was helpful 😀. Please leave your thoughts in the comments section below. You can reach out to me on email: akshat.iitj⚽gmail.com

***
#####References

https://www.ibm.com/support/knowledgecenter/en/SSEP7J_10.2.2/com.ibm.swg.ba.cognos.ug_rtm_wb.10.2.2.doc/c_n30e74.html

https://stackoverflow.com/questions/7839565/logging-levels-logback-rule-of-thumb-to-assign-log-levels
