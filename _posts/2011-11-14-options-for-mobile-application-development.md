---
layout: post
title: Options for Mobile Application Development
excerpt: 
author: daxaar
categories:
  - General

tags:

draft: false
---
This post is based on my interest recently in current mobile development offerings.  Not the specifics of implementation but more around what options are available to us as developers.  In this post I won't be going to go into any specifics as I'm just putting this post out there as a starter for where my current thinking lies.  Over the next few months I'm hoping to expand on this with more specifics on the choices available.

In an entirely fictitious scenario let's imagine our Business User proclaims <strong>"We need an app!"</strong>  This invariably leads to a conversation with the development/design team along the lines of:

<strong>Dev/Design:</strong> "App?  What kind of app?"

<strong>Business User:</strong> "An iPhone app of course!  What else could I possibly mean!?"

<strong>Dev/Design:</strong> "Maybe…
</p>

<p style="margin-left:108pt;">An iPhone app
</p>

<p style="margin-left:108pt;">An Android app
</p>

<p style="margin-left:108pt;">A Windows Phone 7 app
</p>

<p style="margin-left:108pt;">A Blackberry app 
</p>

<p style="margin-left:108pt;">A web app published on the app store/marketplace, i.e <em>Appcelerator</em> or <em>PhoneGap</em>
    </p>

<p style="margin-left:108pt;">A mobile version of our current content site
</p>

<p style="margin-left:108pt;">A mobile version for a specific new product offering"
</p>

<p style="margin-left:108pt;"><em>Skip ahead 12 months</em>…a Windows 8 Metro style app


<strong>Business User:</strong> "Ah…"


As a developer (.NET in particular) we've now got a plethora or choices at our disposal for the provision of a mobile offering.  The technology and platform choices we make are broader than that for our typical LOB applications.  Whilst it's ultimately down to the client's time and budgetary constraints, in the mobile world it's rarely an option for us to target a specific platform.


We need to consider the two ends of the mobile spectrum - given limitless time and budget we'll write native apps for each platform and excel at providing a compelling experience on each device.  Whilst at the other end of the spectrum we'll provide a modicum of time to prettify our content/services for the most common mobile platform.  For now let's ignore the psychology of an <em>app</em> on the App Store / Marketplace, there has to be a middle ground for those of us that aren't writing the next Angry Birds but do understand the significance of mobile going forward and therefore want to embrace it.


Given the above I think it's valuable for us as LOB developers to have a clear understanding of our options for getting the job done when mobile isn't (currently) our core target.  I believe these options lie in the capabilities of CSS3 and HTML5 and when a need for accessing device features such as the camera or accelerometer arise we can extend this through the use of frameworks such as <a href="http://phonegap.com/">PhoneGap</a>, <a href="http://www.appcelerator.com/">Appcelerator</a> and to some degree <a href="http://xamarin.com/monotouch">MonoTouch</a>.  <em>Having just confirmed the link to PhoneGap for this post I can't help but feel disappointment at learning of their acquisition by Adobe.  Good luck!</em>
    

If you're just dipping your toes into the mobile waters I'd also highly recommend looking at what are commonly known as <em>Web Apps.  </em>These are typically mobile versions of a current desktop content/service offering but served up in a very mobile centric way through frameworks such as jQuery Mobile.  These tend to go beyond that which can be achieved with a mobile skinning of existing content. 


I produced this quick and fairly flippant flowchart whilst thinking about this post and figured I'd add it here.  Some of these technologies can of course be intermixed in your mobile solution.  For example, jQuery Mobile can work quite nicely with the PhoneGap and Appcelerator frameworks.



 </p>

&lt;

p style="text-align:center;"&gt;<img src="http://frozenorange.files.wordpress.com/2011/11/111411_2255_optionsform13.png" alt="" />
