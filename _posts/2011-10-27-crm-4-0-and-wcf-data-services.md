---
layout: post
title: CRM 4.0 and WCF Data Services
excerpt: 
author: daxaar
categories:
  - Dynamics Crm

tags:

draft: false
---
UPDATE: The below post has been sat in my drafts since March 2011.  Not sure why I didn't post it given the title of this site does contain the word musings!  Anyway, 6 months on and two projects later I can summarise the Advanced Developer Toolkit as it's known as follows:

<strong>It's considerably better than Fetch-Xml but still has limitations given that it is essentially talking directly to the Web Services.  Make fiddler your best friend and keep a close eye on the queries you're producing.  The expressions the API is building underneath are more than happy to produce pseudo select n+1 and given these are against the web servies this is very bad if you let it get out of control.

Managing the push of entity schema changes made in CRM into the typed entities produced by crmsvcutil can be a pain.  However with a suitable build process in place and having setup the deployment of the binary through a corporate NuGet feed I have the deployment workflow setup pretty slick for us now.</strong>

The original post I failed to post back in March follows:
I can see a requirement dropping on us in the near future for exposing the contacts in our new CRM 4.0 system to the wider world.  The wider world being other divisions within the organisation.

I'm not a CRM expert as we "got a man in" for that bit and one of the other devs on the team picked up the work with him.  I am familiar with the plug-in architecture and the WS- based Fetch XML API into CRM having written a replication service from one of our legacy databases.

So, back to the point.  We think we're going to see a need for some querying capability over our CRM data and having had experience of the web services exposed by CRM I immediately decided that pointing the development teams of our other divisions at that API probably wasn't ideal.

We need options and in this world of LINQ to absolutely everything I decided IQueryable needed to come to my rescue as there must surely be some form of LINQ provider available provided as either open source or better still through Microsoft.  A quick Google came up with a project on CodePlex that whilst flagged as deprecated I was pleased to see its reason for deprecation was that Microsoft's v4.0 of the CRM SDK included a LINQ to CRM Provider.  Superb!
