---
layout: post
title: What is __proto__ in JavaScript?
excerpt: 
author: daxaar
categories:
  - Javascript 2

tags:

draft: false
---
If nothing else it has an amusing name, it's pronounced "dunder proto" due to the double underscore notation it borrows from python.

The <code>__proto__</code> property is used to access the prototype chain for an object instance.  Don't know what a prototype chain is?  Go take a look <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype">here</a>.

So where does it come from? It gets created on any new instance during construction.  If construction is done using a constructor function i.e by using the new keyword <code>var a = new Person()</code> it will point to the prototype of the constructor function, in this instance <code>Person.prototype</code>.  If done using object literal notation <code>var b = {}</code> it will point to <code>Object.prototype</code>.  Note that as everything in JavaScript is an object, all objects can follow their prototype chain back to <code>Object.prototype</code>

You can also gain access to the prototype using <code>Object.getPrototypeOf(...)</code>.  MDN provides <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf">more on this</a>.  You should give this a read if you haven't already to understand the history of this property.

The following code demonstrates the setup of two very simple object literal and constructor function prototype chains.

[code lang=text]
//Object literal
var o = {};
o.__proto__ === Object.prototype; //true
o.prototype === undefined;   //true

//Constructor function
function Shape(){}
var circle = new Shape();

circle.__proto__ === Shape.prototype;   //true
circle.__proto__.__proto__ == Object.prototype; //true
Shape.__proto__ === Function.prototype;   //true
[/code]

More reading.

I've already linked them above but as always the <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/proto">MDN docs</a> are a good place to start.  There is a great <a href="http://stackoverflow.com/questions/9959727/proto-vs-prototype-in-javascript">stackoverflow post</a> that has some really valuable insight amongst the many answers and comments.
