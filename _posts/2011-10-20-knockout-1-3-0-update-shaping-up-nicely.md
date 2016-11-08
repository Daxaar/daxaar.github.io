---
layout: post
title: knockout 1.3.0 shaping up nicely
excerpt: 
author: daxaar
categories:
  - Knockoutjs

tags:

draft: false
---
Although <a href="http://knockoutjs.com">knockout 1.3.0</a> should be coming out of beta shortly I just wanted to put this post out there to express my delight in having seen the new features.&nbsp; In particular the containerless control flow (which doesn't strike me as a particularly intuative feature name) and access to the parent binding contexts.&nbsp; These features will inevitably result in cleaner markup and hopefully both will result in simpler viewModels in support of list based binding.

However, I'm currently not convinced on the use of the class attribute to declare actions against your observables via jQuery live though.&nbsp; That doesn't in my opinion lead to particularly semantic html.&nbsp; Couldn't we see an additional <em>data-</em> attribute such as <em>data-action</em>?

More information on 1.3.0 available over on <a title="More info on knockout 1.3.0 goodness!" href="http://blog.stevensanderson.com/2011/08/31/knockout-1-3-0-beta-available/">Steven Sanderson's blog</a>
