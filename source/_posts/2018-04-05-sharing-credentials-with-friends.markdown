---
layout: post
title: "Sharing credentials with friends"
date: 2018-04-05 23:23:25 +0530
comments: true
categories:
---
While sharing credentials with our friends at work, we mostly use slack, mail or messaging platforms. For a more secure and speedy way, read ahead!

<!-- more -->

A few days back, I had to share a private key for our service account with a friend at my work. I used slack for that. Now my friend, slack and NSA 😱 all have our credentials!

A more secure and speedy alternative is to use `netcat`

To send credentials over a local network, put them in a file and use this:

For receiving data:
```
$ hostname -I (for linux)
'or'
$ ipconfig getifaddr en0 (for os X)
192.168.0.145
$ nc -l 9931 > secret
```

For sending data:
```
$ cat secret | nc 192.168.0.145 9931
```

After this, credentials will be saved to file on the receiver's machine. This will work for huge files with other content as well.

Thanks to Julia Evans for some extremely simple and helpful [blogs](https://jvns.ca/)

I hope this blog was helpful 😀. Please leave your thoughts in the comments section below. You can reach out to me on email: akshat.iitj⚽gmail.com
