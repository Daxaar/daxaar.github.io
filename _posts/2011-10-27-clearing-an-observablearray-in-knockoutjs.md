---
layout: post
title: Clearing an observableArray in knockoutjs
excerpt: 
author: daxaar
categories:
  - Knockoutjs

tags:

draft: false
---
I recently had the need to remove all items from a multidimensional observable array and discovered that doing this by reinitialising means you need to call ko.applyBindings(...) again.  For performance reasons this isn't something you want to be doing to often.  The correct way to do this is call the RemoveAll() method directly on the observableArray itself.

[sourcecode language="javascript"]

var viewModel = {
    customers: ko.observableArray([]),
    moreprops: ko.observable('whatever');
}

ko.applyBindings(viewModel);

//If we now need to clear down the array (in our case this was to restart a quiz) 
//you do the following
viewModel.customers.removeAll();

//You can now add items back into the array without needing to call applyBindings again.
[/sourcecode]
