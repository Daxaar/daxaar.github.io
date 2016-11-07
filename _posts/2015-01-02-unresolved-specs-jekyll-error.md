---
layout: post
title: Fixing Jekyll "unresolved specs" error
draft: false
author: daxaar
---

My Jekyll installation recently stopped working with following error when I tried to run `jekyll serve watch`:

WARN: Unresolved specs during Gem::Specification.reset:
      redcarpet (~> 3.1)
      jekyll-watch (~> 1.1)
      classifier-reborn (~> 2.0)
WARN: Clearing out unresolved specs.

It would seem that there is an issue in one of the supporting gems.  As a workaround you can use the following command if you installed jekyll via bundler

`bunble exec jekyll serve`

There's a discussion of the issue [here](https://github.com/jekyll/jekyll/issues/3084)
