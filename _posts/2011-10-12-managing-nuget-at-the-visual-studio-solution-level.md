---
layout: post
title: Managing NuGet at the Visual Studio Solution Level
excerpt: 
author: daxaar
categories:
  - Nuget

tags:

draft: false
---
A particularly useful feature of the NuGet Package Manager extension within Visual Studio 2010 is the ability to manage your packages at the solution level.  This can be really useful when you're creating a new solution containing several projects and you want to share common packages across them all.

With the initial project structure as below let's say we want to add <a href="http://logging.apache.org/log4net/">log4net</a> to both <em>DaxaarInc.BlogSite.Web</em> and <em>DaxaarInc.BlogSite.Data</em> projects.

<img src="http://frozenorange.files.wordpress.com/2011/10/101211_1810_managingnug1.png" alt="" />

We can achieve this by selecting Manage NuGet Packages… at the Solution level rather than at the project level.

<img src="http://frozenorange.files.wordpress.com/2011/10/101211_1810_managingnug2.png" alt="" />

As you can see below we now get the option to select which projects this package will be installed into.  Whichever you choose they will all share the same version of the package held within a shared packages folder.  Each project continues to get its own <em>packages.config</em> file so they can diverge on version if you really needed to.

<img src="http://frozenorange.files.wordpress.com/2011/10/101211_1810_managingnug3.png" alt="" />

Notice how our packages folder is now stored at the solution level and not at the project level on disk.

<img src="http://frozenorange.files.wordpress.com/2011/10/101211_1810_managingnug4.png" alt="" />

Finally, if the existing solution and projects are under TFS Version Control the packages folder is now also added automatically.  I'm not sure which release of NuGet this arrived in as I haven't kicked off a new solution for a few months now but it's a welcome addition.  I'm also unsure if this integration works when you have a different version control provider such as SVN integrated into VS.  I'll maybe give that a try in the near future using AnkhSVN.

<img src="http://frozenorange.files.wordpress.com/2011/10/101211_1810_managingnug5.png" alt="" />

 

Hope this proves useful.  In an upcoming post I'm going to be looking at the Workflow for creating a new solution structure including setting up in TFS Version Control, Solution structure and creating your own Corporate NuGet Feed for providing an easy install process for your own common libraries.
