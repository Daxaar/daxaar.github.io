---
layout: post
title: Forget the Spec it’s the revenge of the Shiv
excerpt: Embrace HTML5.  Having to support older browsers shouldn't be holding you back.
author: daxaar
categories:
  - General

tags:

draft: false
---
<p style="text-align:center;"><img src="http://frozenorange.files.wordpress.com/2011/11/111111_2302_forgetthesp13.png" alt="" />
    </p>

Are you about to embark on a new website (re)design?  <a href="http://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-html5-features-you-should-be-using-right-now/">Do yourself a favour</a> and embrace HTML5. 

<blockquote>"But I need to support older browsers and this HTML5 stuff won't be getting a ratified spec until 2022.  That's no use for me!  <a href="http://www.ie6countdown.com/"><em>Damn you IE6!</em></a>"
</blockquote>

This is a common misconception of HTML5 and whilst there are many features that are still <a href="http://html5labs.interoperabilitybridges.com/">experimental</a>, a lot are now <a href="http://caniuse.com/">fully supported</a> in all of the modern <strong>and older</strong> browsers.

When it comes to your markup, if you're still using the div tag for anything other than a styling placeholder you're doing it <em>wro…in a less than ideal way</em>.  HTML5 introduces a significant number of more semantic tags such as <strong>&lt;header&gt;, &lt;section&gt;, &lt;article&gt;</strong> and <strong>&lt;footer&gt;</strong> to name a few, but where you'll run into problems is in styling these tags or even getting them to display within old IE.

Older versions of IE will at best fail to style these elements or worse still simply not display them at all.  However, this problem is easily overcome with what's known as a <a href="http://ejohn.org/blog/html5-shiv/"><strong>shiv</strong></a>.  Essentially you can add all of the new HTML5 elements to the DOM within older versions of IE simply by calling <span style="font-family:Courier New;">document.createElement("insert html5 tag name here")</span>.  Older versions of IE will now happily applying your CSS to these tags for which it previously knew nothing.  Sure, you need javascript enabled for this to work but we have to draw the line somewhere.

Of course every web developer faces the same challenges with IE and so common libraries for achieving the <strong><em>revenge of the shiv</em></strong> are prolific to say the least.  However, if you're a Microsoft web developer and using ASP.NET MVC 3 with the latest tools update, you already have ALL of this functionality built right into your new projects compliments of the team including the <a href="http://www.modernizr.com/">modernizr</a> javascript library.  If you haven't done so already I highly recommend having a read of the modernizr docs.  It does far more than help you achieve rounded corners without CSS3 (of course you'll quickly learn it doesn't actually do that at all!).  If you're not using ASP.NET MVC no problem, as with all the awesome sauce nowadays you can also get it through <a href="http://nuget.org/List/Packages/Modernizr">NuGet</a>.

BTW apologies for the insanely cheesy title, despite not being an SW fan at all I strangely couldn't resist.
