---
layout: post
title: WCF - Your process does not have access rights to this namespace
excerpt: 
author: daxaar
categories:
  - WCF

tags:
  - NET

draft: false
---
Hit this exception whilst trying to spin up a WCF test host in my Windows 7 build.  Looks like UAC wants to keep us pinned down but fear not.  Run the following at an elevated cmd to sort it:

netsh http add urlacl url=http://+:port/uri user=DOMAIN\user

Subbing in port, uri and in my case I used my logged in user account.

HTH
