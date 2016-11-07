---
layout: post
title: Fixing a broken npm update
excerpt: "Be careful when updating npm if you installed with homebrew"
draft: false
author: daxaar
---

If you install node and npm using homebrew and later attempt to update npm using the following command you may find yourself "losing" your npm installation at the terminal.

`npm update -g npm`

The problem is caused by npm not playing well with the homebrew installation when trying to update itself.  After finding myself in this situation and following various accepted answers on StackOverflow without success, I eventually came across [this gist](https://gist.github.com/DanHerbert/9520689) on github that worked for me.  There's a great explanation of the details of the issue or you can just dive straight into the solution.
