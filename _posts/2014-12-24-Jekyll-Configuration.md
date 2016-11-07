---
layout: post
title: Jekyll Install Quick Tips
excerpt: "Quick tips when installing Jekyll on a Mac"
draft: false
categories:
tags:
author: daxaar
---

When running rake publish you get an error stating you should try running `bundle install`.  I tried this but without success but if I just ran bundle this appeared to install a whole raft of gems but subsequently rake publish would then work...yay!

If you get an error that you cannot push to master when using `rake publish` change the url to your git repo to use http rather than ssh.
