---
layout: post
title: Entity Framework and WCF - Three ways to play nice together
excerpt: 
author: daxaar
categories:
  - NET
  - Entity Framework
  - WCF

tags:

draft: false
---
Below are the three common issues that always seem to initially catch me out on projects that involve Entity Framework and WCF.  They usually manifest themselves with the really helpful error message "The underlying connection was closed...".  You can spin up WCF tracing but generally they all relate to an issue with the serialisation of the types which should be fixed by one of the following:

1) Lazy Loading - Turn it off (YourContext.ContextOptions.LazyLoadEnabled == false).
2) Dynamic Proxies - They don't play nice over the wire - Turn these off too (ContextOptions.ProxyCreationEnabled == false).
3) Cyclic references - This one is a bit more complicated but nothing that can't be fixed through a custom attribute on your Operation or Service Contracts.  It's explained in excellent detail with full source code over <a href="http://chabster.blogspot.com/2008/02/wcf-cyclic-references-support.html">here</a>.

Remember folks the best way to mitigate these issues is <strong>"Integrate early.  Integrate often."</strong><em>
