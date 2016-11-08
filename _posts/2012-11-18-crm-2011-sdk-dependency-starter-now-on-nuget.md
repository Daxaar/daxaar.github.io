---
layout: post
title: CRM 2011 SDK Dependency Starter now on Nuget
excerpt: 
author: daxaar
categories:
  - Dynamics Crm

tags:
  - Nuget Crm 2011

draft: false
---
Each time I want to create a quick project in Visual Studio to connect to CRM 2011 I head to the SDK and pull in Microsoft.Xrm.Sdk then the source code for the helper classes and finally resolve all the missing framework dependencies IdentityModel, DirectoryServices etc.  The latter being made considerably easier with Resharper.

I've been meaning to package up this process that I've now repeated far too many times and throw it up on Nuget.  I finally managed to find the huge 10 minute commitment it eventually took to get this done tonight.

Available <a title="Nuget Gallery Link" href="http://nuget.org/packages/CRM2011SDKDependencyStarter" target="_blank">on the gallery</a> or to install the package in Visual Studio just open up the Package Manager console and type:

install-package CRMSDKDependencyStarter

or for those of us averse to typing you can shorten this with:

install-p [tab] crm [tab] 
