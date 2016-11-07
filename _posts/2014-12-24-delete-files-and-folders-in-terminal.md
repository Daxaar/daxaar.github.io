---
title: Safely delete files and folders in terminal
excerpt: "The safe alternative to rm -rf *"
author: daxaar
layout: post
categories:
  - Terminal
  - Bash
  - OSX
tags:
- Terminal
- Bash
- OSX
comments: false
draft: false
---

I discovered a useful command line tool today for OSX called trash.  It provides all the power of rm but without the ability to blow your leg off as it moves the affected files and folders to the trash rather than permanently deleting them.

There are many on the forums who believe the power of rm is a good thing as it makes you think before hitting enter.  You can of course always use the -i option too.  Well yes I agree to some extent but we're all human.

So, easiest way to get it is with homebrew:

`brew install trash`
