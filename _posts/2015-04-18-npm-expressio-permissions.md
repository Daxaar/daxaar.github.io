---
layout: post
title: EACCES error on npm install with mean-cli
draft: false
author: daxaar
---

When generating a new mean application using the mean-cli generator available from [http://mean.io](http://mean.io) you may get the following error:

`EACCES, mkdir '/Users/darren/tmp/npm-NNNNNNNN`

Where NNNNNNNN is a random alpha numeric.

This is caused by the tmp folder being owned by root when it should be owned by the user (darren).  To fix this execute the following in the terminal.

```sudo chown -R `whoami` ~/tmp```
