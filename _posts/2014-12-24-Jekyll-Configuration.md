---
layout: post

title: Jekyll Install Quick Tips
subtitle: "Quick tips when installing Jekyll on a Mac"
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

When running rake publish you get an error stating you should try running `bundle install`.  I tried this but without success but if I just ran bundle this appeared to install a whole raft of gems but subsequently rake publish would then work...yay!

If you get an error that you cannot push to master when using `rake publish` change the url to your git repo to use http rather than ssh.