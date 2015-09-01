---
layout: post

title: Fixing a broken npm update
subtitle: "Be careful when updating npm if you installed with homebrew"
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

If you install node and npm using homebrew and later attempt to update npm using the following command you may find yourself "losing" your npm installation at the terminal.

`npm update -g npm`

The problem is caused by npm not playing well with the homebrew installation when trying to update itself.  After finding myself in this situation and following various accepted answers on StackOverflow without success, I eventually came across [this gist](https://gist.github.com/DanHerbert/9520689) on github that worked for me.  There's a great explanation of the details of the issue or you can just dive straight into the solution.