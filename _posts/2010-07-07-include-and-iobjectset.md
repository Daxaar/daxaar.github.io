---
layout: post
title: Include and IObjectSet
excerpt: 
author: daxaar
categories:
  - NET
  - Entity Framework

tags:

draft: false
---
I recently came across the problem of eager loading some entities via EF when using IObjectSet.  I'm using IObjectSet for better test support with my POCO entities.  However, whilst ObjectSet implements Include IObjectSet doesn't.  The following blog post prevented me from having to craft a StackOverflow question!...

<a href="http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-5-iobjectset/">http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-5-iobjectset/</a>
