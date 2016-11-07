---
title: Fixing Angular injector unpr Unknown provider
author: daxaar
layout: post
excerpt: "Fixing another one of those rather cryptic angularjs error messages"
categories:
  - JavaScript
  - AngularJs
tags:
  - JavaScript
  - AngularJs
comments: true
draft: false
---

<span style="color:red;font-family:monospace">
Error: [$injector:unpr] Unknown provider: SomeServiceProvider <- SomeService <- MainController
</span>

TL;DR - Assuming you've checked you aren't duplicating the module definition.  Make sure you've included the service module in the dependencies for the module containing the controller you're unable to inject into.

~~~js
angular.module('MyApp',['other.module.here']).controller(...);
~~~

A little more detail...

You find yourself staring at this error in the dev console and every answer on stackoverflow points to having declared the module incorrectly by redefining it rather than importing.

Let's look at how we arrive at this error in the first place.

This is what you do to declare a new module and you must only do this once across your entire app.

~~~js
angular.module('MyApp',[]);
~~~

Note the [] at the end.  Their inclusion means you're defining a new module along with its dependencies that will be supplied in the brackets.  If the MyApp module has already been defined in another file **it will be overwritten** thereby removing any components defined in those files from the module.

So what is the correct way?

Once you know you've declared your module, subsequent references to the module to declare services, controllers etc must therefore use the following form; sans brackets for deps (unless there are some, which is the key to this post!):  

~~~js
angular.module('MyApp');
~~~

It's this common mistake that all my google searches suggested was the cause of my problem after creating my **first** service and trying to inject it into a controller.  However, after much investigation and head scratching this wasn't the case.

Here's my app.js containing my applications *single* controller and the *only* place where the module 'MyApp' was defined.  Believe me, I checked this several times before concluding the duplicate module definition wasn't my problem.

~~~ js
angular.module('MyApp',[])
  .controller('MainController',MainController);

MainController.$inject = ['SomeService'];

function MainController(someService){
  //...
};
~~~

And here's my myservice.js containing the *one* service in my app that I wish to inject.

~~~ js
angular.module('another.module')
  .service('SomeService',SomeService);

function SomeService(){
  //...
};
~~~

Strangely unit tests for verifying the injected service were passing.  It turns out, somewhat obviously after the fact (isn't that always the case) that I have to inject the service module into the 'MyApp' module as a dependency.  So many answers online talk about removing the dependency brackets from the module definition I couldn't see the woods for trees.

So, to fix this issue all I had to do was:

Change this:

~~~js
angular.module('MyApp',[])
~~~

to this:

~~~js
angular.module('MyApp',['another.module'])
~~~
