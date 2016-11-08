---
layout: post
title: .NET Web Development – Now and Next
excerpt: 
author: daxaar
categories:
  - NET

tags:

draft: false
---
I recently received an email from a friend and ex-colleague asking about the state of play with respect to web development. Like many of us he's seen how you can quickly get lost down the rabbit hole with technologies such as JavaScript and all the OS frameworks, CSS, Mobile, HTML5 and ASP.NET MVC. Where are they all going and what's important right now and in the future. It's a difficult one and I can only really provide opinion.

Below is my reply which is essentially a cut and paste so it may lose context in some places, but hopefully others will get some use from it.

<h3>JavaScript</h3>

I believe JavaScript is going to gain hugely in popularity over the next 2 years to be a language way beyond just DOM manipulation.  At the moment the majority of developers, especially us .NET developers tend to use it as if it's the same as C#.  The only similarity though is the C like syntax.  JavaScript is prototypal, dynamic, functional and object oriented (what a mouthful!).  Essentially what that means is if you're writing JavaScript in the same way as you write C#, you're doing it wrong.  There are lots of good resources out there but I'd highly recommend reading anything by Elijah Manor especially this <a href="http://enterprisejquery.com/2010/10/how-good-c-habits-can-encourage-bad-javascript-habits-part-1/">http://enterprisejquery.com/2010/10/how-good-c-habits-can-encourage-bad-javascript-habits-part-1/</a>.  Also take a look at his presentations from MIX 2010 and 2011 on JQuery.  He's on the JQuery team and knows his onions but explains stuff in a way us mortals can understand.  I tweeted (see side bar) a link to a JavaScript patterns guidance repository on GitHub. Go look that up, it's good stuff.

Do we care about any of the above for DOM manipulation; probably not.  But when you get into using frameworks such as knockout.js for writing web based data-bound MVVM <strong>applications</strong> you soon realise there's a bit more to JavaScript than <em>document.getElementById</em>.  Single Page Applications (<a href="http://en.wikipedia.org/wiki/Single-page_application">http://en.wikipedia.org/wiki/Single-page_application</a>) ranging from Gmail through to what will eventually be JavaScript and possibly HTML5 Windows 8 solutions will require a reasonable knowledge of this stuff.
</span>

<h3>HTML5</h3>

You need to get past all the noise around things like geolocation and the audio and video tags.  HTML5 is about a rethink of what HTML should be.  No more daft doc types etc.  As an example, take a look at the data-* attribute feature as this is heavily used in things like unobtrusive validation in MVC.  If you're developing a site today how does HTML5 fit into that picture, what's the browser support?  Most people think we're not ready for it yet but in actual fact the spec is smart in terms of backward compatibility.  For example, the data-* attribute will simply be ignored by older browsers.  The JavaScript framework Modernizer will allow you to style new HTML 5 tags in older browsers simply by injecting these elements into the DOM during document load.  Cracking read on HTML5 here <a href="http://diveintohtml5.info/index.html">http://diveintohtml5.info/index.html</a>

<h3>AJAX</h3>

Get an understanding of how to use it from JQuery ( $.ajax, $.getJSON etc. )  The Microsoft Ajax libraries are dead and no longer supported.  This will be more useful going forward as people start writing web <strong>applications </strong>with frameworks like knockout.  You'll be presenting an entire API to the client browser predominantly accessed via ajax with JSON being the data format of choice.  Taking it to the furthest level your API will be RESTful, embracing HTTP rather than abstracting it as WebForms has for the past 10 years.  Microsoft is pushing several stacks for this in terms of OData and the WCF Web API.  A lot of people however are dismissing these in favour of using straight ASP.NET MVC and presenting the API through Controllers that only ever return JsonResult.  It's like MVC without the V!  No idea where we'll end up eventually with this one.

<h3>JSON</h3>

See above but essentially it's nothing more than a data format that's nice and lightweight over the wire in comparison to SOAP and also plays nicely in terms of being de-serialised into JavaScript objects on the client.

<h3>CSS</h3>

You may have already noticed but as soon as you get into using JQuery you realise you need a good handle on CSS selectors so let's do that one first.  You'll have no doubt in the past been down the road of just randomly editing the CSS, refreshing the browser and hoping the CSS gods are looking down upon you and everything now looks as expected.  Unfortunately not a fat lot's changed in this area but we're not alone in this camp so there are two OS frameworks called SASS and LESS (<a href="http://coding.smashingmagazine.com/2011/09/09/an-introduction-to-less-and-comparison-to-sass/">http://coding.smashingmagazine.com/2011/09/09/an-introduction-to-less-and-comparison-to-sass/</a>) which aim to alleviate some of the pain experienced with CSS.  Do you need to know these; probably not but again it doesn't do any harm to know they're there to help.

<h3>CSS3</h3>

Apart from the ubiquitous border-radius!  Media Queries are the big one here which you'll hear all about in the same sentence as "Responsive Web Design".  It's all about adapting the styles used on a web page based on the viewport (device-width) amongst other attributes.  The most common usage scenarios are therefore styling for desktop or mobile.  MVC 4 is rolling some of this stuff in but also allowing you to easily create media query based or device specific views.  Phil Haack did a decent talk on this at Build.  Search <a href="http://channel9.msdn.com">http://channel9.msdn.com</a> .

<h3>JQuery</h3>

Know it, learn it, and love it.  You'll be doing nothing without it.  As mentioned up there get your head around the $.ajax API and understand CSS selectors.  The best thing I've found about JQuery is it's so ubiquitous now that all you have to do is think about what you want to achieve, type it into Google and append jQuery to the end.  Cut, paste and job done.  Next level on from that is writing a plugin and then if you're so inclined JQueryUI which is all about widgets and presentation and finally JQueryMobile which is a mixture of JQueryUI and HTML5 for the mobile devices.  I knocked up a half decent iPad version of my LearnAndGame site (see below) literally in about 10 minutes. I'm over simplifying JQuery here as it's so much more but that'll do for now.

<h3>ASP.NET MVC</h3>

Get the HTML5 Boilerplate template off the extensions gallery within VS.  This shows you some great guidance on website best practice.  It's a bit over the top as a starting point for a site in my opinion but a good reference for learning.  Moving on nicely from that also go get the NuGet gallery source from GitHub as this is also a great reference site for MVC development.

<h3>WHAT NEXT</h3>

Take a deep breath and go grab a scotch! After that I'd recommend taking a look at knockout.js <a href="http://knockoutjs.com">http://knockoutjs.com</a> as mentioned above.  It's a fantastic framework and will really help you get to grips with writing JavaScript using best practice.  If you're anything like me you'll get terribly distracted when reading samples of code and not understanding what the JavaScript is doing.  You'll head off to find out more, spend a few hours in <a href="http://jsfiddle.net">http://jsfiddle.net</a> getting hopelessly lost and eventually find your way back to where you started.  This can be insanely frustrating but at the same time immense fun.  Personally, it's why I love being a developer.

If you're so inclined feel free to get your Git** and GitHub mojo on and fork my LearnAndGame repository here <a href="https://github.com/Daxaar">https://github.com/Daxaar</a> .  At the moment it's nothing more than a playground for my learning JavaScript but I've got some high aspirations for that as a learning platform for kids.  At the moment it's taking a serious dip in priorities.

** Quite simply the most bonkers and yet wonderful Distributed Version Control System (DVCS) known to man.  It makes working in TFS version control feel like seriously hard work.

Have fun
Daz
