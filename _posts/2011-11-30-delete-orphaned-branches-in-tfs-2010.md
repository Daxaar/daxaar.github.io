---
layout: post
title: Delete orphaned branches in TFS 2010
excerpt: 
author: daxaar
categories:
  - Team Foundation Server

tags:

draft: false
---
I recently found myself in a situation in our TFS Source Control where I wanted to convert a <em>main</em> folder into a branch.  However I was presented with an error message telling me that I couldn't do this as a branch already existed below this folder.  It turns out that a branch had previously been created incorrectly and then subsequently deleted.  However, if you delete a branch its relationship remains and prevents you from branching its current parent.

I found <a href="http://mkdot.net/blogs/latek/archive/2010/09/10/delete-orphaned-branch-relation-using-visual-studio-net-tfs-2010.aspx">the following blog post</a> provided me with the answer.  But more usefully it showed me the 'show deleted items' checkbox that gives you a much better historical view IMO of the Source Control structure.  Maybe this should be the default view with the option to turn it off rather than on?
