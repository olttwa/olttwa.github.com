---
layout: post
title: "Merits of Pair Programming - Part 1"
date: 2017-12-03 23:31:40 +0530
comments: true
published: false
categories:
---

read atleast 5 blogs talking about pair programming.
read rajeev & ranjan's discussion about it on slack

first of all, there is no silver bullet.

why to pair program?
- rotation is the most important reason.
- dependency reduction is another. there'll be atleast 1 other person to look at prod issues or take project ahead in your absence.
- you are training/getting trained  as you work.
- free me you get to teach/get taught.
- for teacher, the ideas get clearer in their minds. abstraction of ideas becomes stronger.
- for student, questions start getting refined. for some questions, you get answers, for others, you are asked to google them yourselves.
- two sets of eyes are always better. even sherlock holmes needed john watson; you are just a programmer.
- your work gets refined. if you are novice (which we all are), there is a very high chance that the first solution that comes to mind isn't the best. when somebody pokes holes in that idea, there is a very high chance that the idea changes/evolves.

why/where not to pair program
- this is a very broad problem.
- in current company we have people normally assigned for a week. so the idea is that whatever comes up, you'll pair.
- if there is a bug, pair on it. first, if other pair hasn't context, he/she will develop some. second, if other pair has context, maybe you'll think of a solution so that this bug never comes up again.
- the team velocity might be affected if you pair even for bugs, but then the motive of pairing is taken care of.
- pair programming is indeed a lot of effort for juniors. i used to open tabs. couldn't/wouldn't study at night. and at end of 2 weeks, i'd have 500 tabs open on my firefox.
- as a senior member in pair programming, i've faced questions i didn't knew answers to, i thought i knew but couldn't explain, etc. that time i had to go home and study up on those topics so i could explain to my pair.
- i've learnt about trivial stuff such as editor short-cut, debugging in gogland/intellij; to major stuff like abstraction at package level, best practices for web servers, (read mail to platform team)

How to pair program?

- keep in mind the motive of pair programming. 'you will work on same problem at same time; arrive at solution at same time; both of you will have complete context of the task accomplished. by complete context, i mean in absence of one, the other should be able to add further developments to the project or debug an issue.
- if above motive isn't met, the responsibility is on entire pair. please do an RCA if above isn't met.
- going from top to bottom in order of importance in my opinion.
- one screen, 2 monitors, 2 keyboards and mice is mandatory. however small or large the bug, stick to one screen.
- healthy switch between navigator and driver.
- decide upon core working hours. this might seem trivial, but is very important. my example of roy: we are in at 9:30 together, and are able to stay till 7:30-8. that's not the case with married people. you have to check with them, make sure there are atleast 5 hours you've coded in a day. (excluding lunch, play breaks)
- check in code by eod so other can continue if you are late to office by whatsoever reason.
- should you work on a issue you left at work at home? it is entirely upto you. if you are concerned about velocity of team, have time, then go ahead and try to debug the issue. but next day please tell your pair what debugging you did, how you arrived at the solution. basically the other guy/girl should know why each and every decision was taken.
- you should have project setup on both your laptops. so you can work on some bug at home.
- the editor choice should be mutually beneficial so as to not slow the other person down.
