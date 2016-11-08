---
layout: post
title: Changing the scope of the AssignedTo field in TFS 2010 Work Items
excerpt: 
author: daxaar
categories:
  - Team Foundation Server

tags:

draft: false
---
<span style="font-family:Cambria;font-size:12pt;">This post is related to changes for Team Foundation Server 2010 but a similar process can also be followed for TFS 2008.
</span>

<span style="font-family:Cambria;font-size:12pt;">For so long I've been meaning to sort out the list of names that appear in the AssignedTo dropdown list when creating work items.  This evening I've been making some changes to our work item <em>Status</em> workflow following some positive feedback from the QA team and so finally got around to fixing this.
</span>

<img src="http://frozenorange.files.wordpress.com/2012/01/011812_2142_fixingthesc11.png" alt="" /><span style="font-family:Cambria;font-size:12pt;">
        </span>

<span style="font-family:Cambria;font-size:12pt;">By default it will show all of the Active Directory users that have access to the project.  That unfortunately includes all of the system administrators and service accounts, TFS related or otherwise that will be imposed upon you through group policy.
</span>

<span style="font-family:Cambria;font-size:12pt;">What we need is the ability to restrict this list to only those people pertinent to the project.  At the simplest level that would be those people within the TFS Project Contributors group.  In a future post I'll look at filtering this list further based on additional attributes of the work item. For example, subsequent to setting the status to Triaged, you may only want to assign to members of the development team.  For now let's keep it simple.
</span>

<span style="font-family:Cambria;font-size:12pt;">I'm going to assume you're comfortable with the TFS Power Tools (available as an Extension in VS 2010) as it's through the Process Editor available in this extension that we'll be making our change.
</span>

<span style="font-family:Cambria;font-size:12pt;">You have a couple of choices here.  You can either edit the Work Item Template against a Process Template or as I'm doing directly for now, against the WIT for an existing project.
</span>

<img src="http://frozenorange.files.wordpress.com/2012/01/011812_2142_fixingthesc21.png" alt="" /><span style="font-family:Cambria;font-size:12pt;">
        </span>

<span style="font-family:Cambria;font-size:12pt;">Select the Work Item Type from the appropriate project in the dialog that pops up and you'll be presented with the Work Item Editor screen thus:
</span>

<img src="http://frozenorange.files.wordpress.com/2012/01/011812_2142_fixingthesc31.png" alt="" /><span style="font-family:Cambria;font-size:12pt;">
        </span>

<span style="font-family:Cambria;font-size:12pt;">Double click Assigned To and select the <strong>Rules </strong>tab on the dialog
</span>

<img src="http://frozenorange.files.wordpress.com/2012/01/011812_2142_fixingthesc41.png" alt="" /><span style="font-family:Cambria;font-size:12pt;">
        </span>

<span style="font-family:Cambria;font-size:12pt;">You won't have ALLOWEDVALUES in your list.  It's the setup of this rule that filters the list of displayed names.
</span>

<span style="font-family:Cambria;font-size:12pt;">Click New and enter the name of the TFS group you want to restrict the list to.
</span>

<img src="http://frozenorange.files.wordpress.com/2012/01/011812_2142_fixingthesc51.png" alt="" /><span style="font-family:Cambria;font-size:12pt;">
        </span>

<span style="font-family:Cambria;font-size:12pt;">In our case I'm restricting to the Contributors group for the current project.  Note the highlighted [project] should be as is and <strong>not</strong> substituted for your own project name.
</span>

<span style="font-family:Cambria;font-size:12pt;">Close down all the dialogs and save the template (either import if you exported or just save).  If you did this against an existing project go in and create a Work Item of the modified type and hopefully you'll see a much cleaner list.  If your AD is setup correctly it'll pull in Full Name otherwise you'll get just the login name.
</span>

<span style="font-family:Cambria;font-size:12pt;">I hope this is of some use and please don't be afraid to get stuck into modifying your process templates and work items.  Whilst it's always a good idea to start with the OOB template never be afraid to modify it to suit your own needs.  Especially if in our case it helps in getting some real usage out of TFS
</span>

<span style="font-family:Cambria;font-size:20pt;"><strong>Summary
</strong></span>

<span style="font-family:Cambria;font-size:12pt;">You can restrict the names that appear in the AssignedTo list by adding an ALLOWEDVALUES rule to the attribute within the Work Item Template.</span>
