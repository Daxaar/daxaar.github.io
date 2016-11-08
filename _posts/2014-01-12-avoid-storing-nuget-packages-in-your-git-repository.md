---
layout: post
title: Avoid storing Nuget packages in your Git Repository
excerpt: 
author: daxaar
categories:
  - GIT

tags:
  - GIT
  - Nuget

draft: false
---
Git is a fantastic version control system but it was never designed for storing binary files. They clutter the history and even if removed that history must still be maintained. Ideally a remote pull should be a fast and pain free operation; one of the core tenets of git is speed. Something that anyone who has spent any amount of time within TFS will appreciate.

The screenshot below shows the packages folder of a newly created ASP.NET MVC 4 project. I appreciate some of these are scripts but that's 47MB (before adding any project specific packages such as DI or Mocking) of binary data your git repo needs to maintain history for, <strong>binary</strong> history that you're unlikely to ever care about.

<img alt="" src="http://frozenorange.files.wordpress.com/2014/01/011214_2155_avoidstorin1.png" />

You may now be thinking "What if we need to revert to an earlier build?".  You can still do this using the exact same binary versions as when you created the commit. Simply check out the commit and build the solution as normal. Your packages will be restored to the exact versions at the time of the commit because the packages.config file which defines the versions of those packages is stored in your repo.

Let's fix this…

<ol>
    <li>Enable NuGet Package Restore by right clicking on your VS solution. This will as the name suggests ensure on build of the solution that all package dependencies are pulled in from the configured nuget repositories. What to restore is defined in the packages.config file which is stored in the root of each project in the the solution. As mentioned earlier these will be version controlled which is what allows us to always restore source and package dependencies for any commit in the history. More info on this feature is available on the <a href="http://docs.nuget.org/docs/reference/package-restore">NuGet website</a>.</li>
</ol>

<img alt="" src="http://frozenorange.files.wordpress.com/2014/01/011214_2155_avoidstorin2.png" />

<ol>
    <li>Add the line <strong><em>packages/ </em></strong>to your <a href="http://git-scm.com/docs/gitignore">gitignore</a> file. This is the important bit and something a lot of people forget to do.</li>
    <li>Commit the changes to the repo.</li>
    <li>That's it we're done!</li>
</ol>

<strong>Make sure you do this BEFORE the initial commit to the repo.</strong>
