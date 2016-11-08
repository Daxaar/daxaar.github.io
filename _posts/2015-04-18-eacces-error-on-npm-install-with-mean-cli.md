---
layout: post
title: EACCES error on npm install with mean-cli
excerpt: 
author: daxaar
categories:
  - Express
  - MEAN
  - NPM

tags:

draft: false
---
When generating a new mean application using the mean-cli generator available from <a href="http://mean.io">http://mean.io</a> you may get the following error:

<code>EACCES, mkdir '/Users/darren/tmp/npm-NNNNNNNN</code>

Where NNNNNNNN is a random alpha numeric.

This is caused by the tmp folder being owned by root when it should be owned by the user (darren). To fix this execute the following in the terminal.

<code>sudo chown -R `whoami` ~/tmp</code>
