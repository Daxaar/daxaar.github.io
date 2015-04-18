---
layout: post

title: EACCES error on npm install with mean-cli 
subtitle: ""
cover_image: blog-cover.jpg

excerpt: ""

draft: false

author:
  name: Darren
  twitter: daxaar
  <!--gplus: 100687498195339762535 -->
  bio: Director, Software Hack
  image: ks.png
---

When generating a new mean application using the mean-cli generator available from [http://mean.io](http://mean.io) you may get the following error:

`EACCES, mkdir '/Users/darren/tmp/npm-NNNNNNNN`

Where NNNNNNNN is a random alpha numeric.

This is caused by the tmp folder being owned by root when it should be owned by the user (darren).  To fix this execute the following in the terminal.

```sudo chown -R `whoami` ~/tmp```
