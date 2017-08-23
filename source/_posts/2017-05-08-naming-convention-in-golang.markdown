---
layout: post
title: "Naming convention in golang"
date: 2017-05-08 10:12:08 +0530
comments: true
published: false
categories: 
---
A blog on how to name variables in golang to improve readability and expressiveness of your code.

- This is the naming convention specified in go Docs (link to the place)
receivers should always be 2-3 lettered if body of method doesn't excede 15 lines or so
use short forms for standard names like responseWriter, request etc.
I am against this type of naming
There are 3 reasons I am against this:
1. It reduces readability. Everytime you are jumping across func definitions, you have to look at the func declaration to understand what the full form is in order to recollect the receiver's type. I suggest you should use full form then and there itself so you don't have to do up/down in order to know what the receiver object type is
2. Mostly, you'll be a polyglot if you are in a high-paced environment. In that case, it becomes very difficult to remember the small nuances of a programming language even if you have worked on the language for a long time* (like 2 years)*. To make my point, I will give an example of my friend who has worked on golang for more than 2 years, but during our recent discussion he incorrectly said r stands for Request. 
3. If you are writing a microservice/library in golang, it is likely you'll work on more than just five projects. So, let me list down all the short forms used in our company: ctr -> counter, on, ls, cd, ud, cfg, w, r, *(all other short forms used in anonymization service)*. This makes it very difficult everytime you come accross a short form to grasp what it really means.
I have heard an absurd comment on using full forms in golang. That is: "It looks like java code if you don't use short forms." So what??? One of the main principles of writing software is readability. During our bootcamp at Go-Jek, we were specifically asked to give more preference to readability over number of lines and convention.
So to sum it up, keep your code expressive and fuck this bad convention of golang.


=> P.S.: My friend said r stands for responseWriter(w is used as short form for this *(huge fan of last week tonight)* and this is the point I am trying to make. Even if you'd have worked in golang for sometime, you'd have gotten confused whether r is responseWriter or request when you read this above. Instead if we use full forms, we can get rid of all this.
