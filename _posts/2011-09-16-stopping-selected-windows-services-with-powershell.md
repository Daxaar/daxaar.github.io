---
layout: post
title: Stopping selected Windows Services with Powershell
excerpt: 
author: daxaar
categories:
  - Powershell

tags:

draft: false
---
<p>I set all of the VMWare services on my machine to be manual start recently and figured the easiest way to restart when I needed to spin up a VM was with a simple net start ... batch file.

That would be a perfectly good solution but I figured Powershell must provide another way and in one of those "I wonder if..." moments I tried executing the following in an elevated PS window and was pleased to see it work out perfectly.</p><blockquote><p>Stop-Service VM*</p></blockquote>
