---
layout: post
title: Making data available to all express views
excerpt: 
author: daxaar
categories:
  - Express
  - Javascript 2

tags:

draft: false
---
In this post I'm going to show you how to make data available to all of your views in an express 4 website. I'll be using jade in my sample code but this solution is not specific to any view engine.

Imagine we want to display the name of the logged in user in the top right hand corner of the screen on every page. One way you could do this is to include the user object in every route handler that returns a view like so:

[code lang=text]
res.render(&#039;viewname&#039;,{user:&#039;Joe Bloggs&#039;})
[/code]

This approach is cumbersome and error prone as the developer is sure to forget to pass this data in at some point.

The logical place to put this is in the layout view which is shared by all your other views. Think <code>_ViewStart.cshtml</code> in an ASP.NET MVC application.

[code lang=text]
doctype html
html
head
title= title
body
div(style=&quot;float:right&quot;) Hi #{user.name}
block content
[/code]

In the code above you can see that we are referencing a user object to output the name of the currently logged in user. All views in an express application have access to an implicit variable called locals which hangs off the response object. Jade allows us to access data hanging off locals without referencing it directly.

So <code>#{user.name}</code> is equivalent to <code>#{locals.user.name}</code>

We need to load up this data for all routes and we can do this in our express startup file, app.js, index.js etc.

[code lang=js]
var app = express();
app.use(function(req, res,next){
//locals is available to all our views including layout and because this middleware is fired for all routes we are therefore setting up the user for every view.
res.locals.user = {name: &#039;Joe Bloggs&#039;};
});
[/code]

That's it, you now have shared data accessible from all your views.

I hope this post has been of some use. An incredibly simple solution but if like me you're often switching between ASP.NET MVC and Node/Express, you sometimes need to take a step back and remember to "think inside the framework".
