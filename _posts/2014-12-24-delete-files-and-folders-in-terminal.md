---
layout: post

title: Safely delete files and folders in terminal
subtitle: "The safe alternative to rm -rf *"
cover_image: blog-cover.jpg

excerpt: "Shooting yourself in the foot is better than blowing your leg off"

draft: false

author:
  name: Darren
  twitter: daxaar
  <!--gplus: 100687498195339762535 -->
  bio: Director, Software Hack
  image: ks.png
---

I discovered a useful command line tool today for OSX called trash.  It provides all the power of rm but without the ability to blow your leg off as it moves the affected files and folders to the trash rather than permanently deleting them.

There are many on the forums who believe the power of rm is a good thing as it makes you think before hitting enter.  You can of course always use the -i option too.  Well yes I agree to some extent but we're all human and I think the purists who hate to see GUI features creeping into the terminal need to take a step back sometimes. 

So, easiest way to get it is with homebrew:

`brew install trash`