---
layout: post
title: "Proctor: An Automation Orchestrator"
date: 2018-07-25 21:54:56 +0530
comments: true
categories:
---

Amazon web store had an insane requirement. Every single item added to cart should never be amiss. Lo and Behold! DynamoDB was born.

```
Insane requirements drive the best innovation
```

Proctor, a developer friendly automation orchestrator, was born out of one such insane requirement:

- Centralize automation across org
- Enable developers' contribution to automation
- Enable developers' utilization of automation

<!-- more -->
***

### Conception of Proctor

Thus, proctor was born. Behold a demo of proctor. I need `proctor.gojek.com` domain to point to `10.1.2.3` IP address. Using just a binary, I can run automation to create domain name records. Behind the scenes, the automation creates a domain name in [AWS route53](link-to-route53).

```
video/gif of running above job
Caption: nslookup proctor.gojek.com
```

`Note that in order to create a domain name record, I needed neither access to AWS nor knowledge of route53.`


***

### Getting here

Go-Jek is a high growth startup [^1]. As Matt Klien correctly observes in [this blog](blog), Go-Jek too formed a systems team in the early days to cope with maddening infrastructure requirements. The result though good in the short-term, proved catastrophic in the long-term. We ended up with:

- A plethora of automation scripts spread across org.
`image: https://docs.google.com/presentation/d/1e1MY3QpIYvEg2R-ickE95Ui4M6kfu9dNCywTkuGvNZw/edit#slide=id.g35c40a82c9_0_259`
- Running above scripts required installing dependencies on each machine, not to mention access management for infra management tools
`image: https://docs.google.com/presentation/d/1e1MY3QpIYvEg2R-ickE95Ui4M6kfu9dNCywTkuGvNZw/edit#slide=id.g35c5a44ec9_0_0`

***

### Running into problems

##### Accidents

Using a kitchen knife you can cut vegetables and cook delicious food. Lose focus, and you end up hurting yourselves (sometimes others too). This goes without saying that widespread access to powerful tools like knife, AWS, gcloud has resulted in VMs being deleted and databases being dropped accidentally.

##### Maintenance of automation

Having automation spread across org resulted in:

- Difficult onboarding of users to use automation scripts
- Propogating changes in automation across org
- Same task automated in multiple ways aka duplication of effort

***

### Solving problems

##### Centralize automation across org

- central automation reservoir (1st component)
- since it's git, automation is versioned
- proctord (a web service) takes care of running this automation (2nd component)

##### Enable developers' contribution to automation

- automation is packaged inside docker images
- immutable infra
- No restraints. ruby, python, bash, perl choose whatever you'd like!

##### Enable developers' utilization of automation

- proctor binary sits on developers' machines. (3rd component)
- on executing an automation, the binary talks to proctord
- logs of automation script are streamed on the developer's machine from proctord to the binary
- developer is decoupled from addition/modification/deletion of automation. all changes in automation reservoir are registered to proctord. The binary reflects changes when it talks to proctord

***

### Impact

We've launched beta of Proctor at Go-Jek[^2]. Usage of automation across org has reduced ad-hoc tasks for our team by 70% over the past 3 months.

Instead of providing access to powerful infra management tools;  we now build the utilities as automation and distribute it using Proctor. We now have controlled access to powerful tools.[^3](safety increases product usage)

***

## Open sourcing Proctor

We've open sourced proctor. You can find the source code [here](https://github.com/gojektech/proctor)

In an upcoming blog, we'll take a deep dive into the architecture of Proctor. We'll answer questions such as why using rundeck for automation didn't work for us, how we scale proctor infinitely, how do we manage secrets required to access powerful tools using proctord, etc.



I hope this blog was helpful 😀. Please leave your thoughts in the comments section below. You can reach out to me on email: akshat.iitj⚽gmail.com

[^1]: [a blog citing growth of go-jek](https://a.com)
[^2]: Awaiting authentication before launching v1.0.0

