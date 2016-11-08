---
layout: post
title: Taking Team Foundation Service for a quick spin
excerpt: 
author: daxaar
categories:
  - Team Foundation Server

tags:

draft: false
---
Having just watched <a href="http://blogs.msdn.com/b/briankel/">Brian Keller's</a> talk at //Build online I decided to give the new <a href="http://tfs.visualstudio.com/">Team Foundation Service</a> offering a spin. It's free for teams of up to five users and whilst in preview also free for larger teams. No confirmed pricing plans yet so let's hope MS don't go silly if they really want to complete with the likes of GitHub and AppHarbor.

Setup is an absolute breeze having just created an account with my Live ID I was able to create a Team Project and start creating tasks in seconds. Make sure you pick your org name carefully as it cannot be changed at a later date. It also forms part of your URL so company name will be the obvious choice over a specific project name.

Hooking into Visual Studio 2012 is equally easy using the Team Explorer dialog to add a new server you just enter your URL http://xyz.visualstudio.com and you'll be prompted for Live ID and you're up and running. I just tried creating a task, pushing it to Outlook (2013) and following the link to view online and all went well. Having been through the pain of setting up an on-premise TFS environment including the SharePoint, SQL Reporting and Build Controllers this is a real step forward for smaller teams and I'll definitely be digging in a lot more.

In an upcoming post I'll be taking a closer look at the Azure Continuous Deployment Build Definition and comparing this with the new Continuous Deployment offering for GitHub and CodePlex integration introduced to Azure Websites recently.

If you want to try out any of the new Azure features head over to the <a href="http://windows.azure.com">Azure Website</a> and sign up for the 10 free Azure Websites offering. Alternatively, if you're a Microsoft Partner you can sign up for Cloud Essentials for your Azure access and whilst you're there why not get on board with CRM 2011 Online and Office 365 partner access.
