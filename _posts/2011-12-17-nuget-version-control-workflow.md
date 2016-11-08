---
layout: post
title: NuGet Version Control Workflow
excerpt: 
author: daxaar
categories:
  - NET

tags:
  - Nuget

draft: false
---
With the release of <a href="http://nuget.org">NuGet</a> 1.6 we now get the ability to control the importing of dependent packages at build time through the injection of a custom .target file into each project within the Visual Studio solution.  This may seem unusual for teams that use Team Foundation Server for version control as we typically like to see those binaries included as part of the check-in process into the usual lib/dependencies/third-party (<em>delete as appropriate</em>) folder.

So why have the NuGet team done this?  Well mainly for the DVCS teams as their repositories can grow quite large with all these binary check-ins causing merges to take significant amounts of time.  But even if you don't use a DVCS such as Git or Mercurial simply having this option available to us for any version control workflow is simply awesome in my opinion.  I think I'll be checking out how it works for comparison on an upcoming small project.

For now if you want to use the "source control free" workflow you can enable it <strong>at the solution level.</strong>

<img src="http://frozenorange.files.wordpress.com/2011/12/121711_2031_nugetversio1.png" alt="" />

 

<a href="http://nuget.org">NuGet</a> just continues to get better and better and with one of the Project Leads Phil Haack now working at GitHub I'm even more excited to see where the product goes.  Further information on this new feature is available on the NuGet docs site <a href="http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages">here</a>.
