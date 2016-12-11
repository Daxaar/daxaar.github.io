---
layout: post
title: Fixing Jekyll "unresolved specs" error
excerpt:
author: daxaar
categories:
  - Jekyll

tags:

draft: false
---
My Jekyll installation recently stopped working with following error when I tried to run

`jekyll serve watch`

~~~ text
WARN: Unresolved specs during Gem::Specification.reset:
redcarpet ( &gt; 3.1)
jekyll-watch ( &gt; 1.1)
classifier-reborn ( &gt; 2.0)
WARN: Clearing out unresolved specs.
~~~

It would seem that there is an issue in one of the supporting gems. As a workaround you can use the following command if you installed jekyll via bundler

`bunble exec jekyll serve`

There's a discussion of the issue <a href="https://github.com/jekyll/jekyll/issues/3084">here</a>
