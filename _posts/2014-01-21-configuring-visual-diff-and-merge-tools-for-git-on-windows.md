---
layout: post
title: Configuring visual diff and merge tools for git on Windows
excerpt:
author: daxaar
categories:
  - GIT

tags:

draft: false
---
There's plenty of information available on the net for configuring your visual diff/merge tool of choice for git. However, a lot of it is out of date. As of Jan 2014 using git v 1.8.4 this is the concise guide to setting up your visual diff and merge tool(s) of choice.

Add the following to your .gitconfig. If you don't know what that is <a href="http://git-scm.com/book/en/Customizing-Git-Git-Configuration">go here</a>.

~~~
[diff]
   external = C:\Program Files\Perforce\p4merge.exe
    tool = p4merge
[difftool "p4merge"]
    cmd = p4merge.exe $LOCAL $REMOTE
[difftool]
    prompt = false
[merge]
    tool = p4merge
[mergetool "p4merge"]
    cmd = p4merge.exe $BASE $LOCAL $REMOTE $MERGED
~~~

I'm using p4merge by <a href="http://perforce.com/product/components/perforce-visual-merge-and-diff-tools">Perforce</a>. It's free and supports the git three way merge well. If you want to use any other tool of choice add it to your path and replace the references to the .exe accordingly.
