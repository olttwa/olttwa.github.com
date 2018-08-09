---
layout: post
title: "Proctor: An Automation Orchestrator"
date: 2018-07-25 21:54:56 +0530
comments: true
categories:
---

Amazon had an insane requirement. Every product added to cart should never be missed. Lo and Behold! DynamoDB was born.

`Insane requirements drive the best innovation`

Proctor, a developer friendly automation orchestrator, was born out of similar requirements:

- Centralize automation across org
- Democratize contribution to automation
- Democratize utilization of automation

<!-- more -->

****

### Conception

Thus, Proctor was born. Using Proctor, let's point proctor.gojek.com domain to *2.0.1.8* IP address. Using *proctor binary*, we can run *Procs -aka automation* to create domain name records. Behind the scenes, `dns-creation` *Proc* creates a domain name record in [AWS route53](aws.amazon.com/route53).

![running-procs](/images/running-procs.gif)

`NOTE: To create a domain name record, we needed neither access to AWS nor knowledge of route53`

****

### Getting here

Go-Jek is a high growth startup [^1]. As Matt Klein correctly observes in [this blog](https://medium.com/@mattklein123/the-human-scalability-of-devops-e36c37d3db6a), Go-Jek too formed a small team in the early days to cope with maddening infrastructure requirements. The result, though good in the short-term, proved catastrophic in the long-term. We ended up with:

- A plethora of scripts spread across org
- A nightmare of managing dependencies of scripts
- Managing access for scripts' tools

![plethora-scripts](/images/plethora-scripts.png)
![scripts-dependencies](/images/scripts-dependencies.png)

****

### Running into problems

#### Accidents

Using a kitchen knife you can cut vegetables and cook delicious food. Lose focus, and you end up hurting yourselves (sometimes others too). This goes without saying that widespread access to powerful tools like knife, AWS, gcloud has resulted in VMs being deleted and databases being dropped accidentally.

#### Maintenance

Having automation spread across org resulted in:

- Multiple ways of performing similar tasks - *duplication of effort*
- Dependency installation for using scripts painful - *onboarding issues*
- Propagating changes in scripts across org almost impossible

****

### Solving problems

#### Centralize automation across org

- All *Procs* reside in a central automation reservoir
- *Procs* are under version control
- *proctord, a web service,* facilitates running of *Procs*

#### Democratize contribution to automation

- *Procs* are packaged inside docker images[^2]
- Dockerized *Procs* means __no restraints__ for delopers contributing to automation. AWS, gcloud, chef, ansible choose whichever tools you like! ruby, python, bash, perl choose whichever language you like!
- *proctord* provisions access to tools needed by *Procs* during runtime

`For building automation, your imagination is the limit!`

#### Democratize utilization of automation

- Using *proctor binary*, developers execute *Procs* from their CLI
- *proctord* spins up *Procs* as jobs in a kubernetes cluster[^3]
- *proctord* streams logs of *Procs* to user's CLI for feedback

****

### Impact

We've launched beta of Proctor at Go-Jek[^4]. Usage of automation across org has reduced ad-hoc tasks for the systems team by 70% over the past 3 months.

We now build the utilities of powerful tools as automation and distribute it using Proctor, enabling *controlled access*.[^5]

****

### Conclusion

It took 3 components - *Procs, proctord and a binary* to solve automation at Go-Jek. To the end-user, using automation only requires a binary and an internet connection 😍

****

## Open sourcing Proctor

We've open sourced Proctor. You can find the source code [here](https://github.com/gojektech/proctor)

In an upcoming blog, we'll take a deep dive into the architecture of Proctor. We'll answer questions such as why using rundeck didn't work for us, how we scale Proctor, how we manage secrets and access to tools required by *Procs*, etc.

***

I hope this blog was helpful 😀. Please leave your thoughts in the comments section below. You can reach out to me on email: akshat.iitj⚽gmail.com

[^1]: https://www.techinasia.com/gojek-insider-account-of-scaling-900x-doubling and https://blog.gojekengineering.com/200-engineers-261-million-people-go-jeks-impact-in-indonesia-b8f87934e6c1
[^2]: Immutable infrastructure provides Proctor an edge over competing open source automation solutions
[^3]: A k8s cluster helps us scale the automation orchestrator infinitely
[^4]: Authentication is a blocker for v1.0.0 release
[^5]: Adoption of product is inversely propotional to risk. Reference: [https://ieeexplore.ieee.org/document/7476689/](https://ieeexplore.ieee.org/document/7476689/)
