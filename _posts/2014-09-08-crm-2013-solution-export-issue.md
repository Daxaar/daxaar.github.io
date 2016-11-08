---
layout: post
title: CRM 2013 Solution Export Issue
excerpt: 
author: daxaar
categories:
  - Dynamics Crm

tags:

draft: false
---
Recently I was having problems exporting a solution from an on-premise CRM 2013 organisation.  Unusually there was no additional log to download and turning on verbose logging allowed me to see the exception being thrown on export but there was no indication to the source of the error.

I eventually resolved the problem by process of elimination, removing likely candidates from the solution until I could export successfully.  It turned out to be an errant Routing Rule Set which was configured for forwarding to a queue but the queue wasn't defined.  Since you can't create a rule and forward to a queue without defining the queue, I assume it must be due to the solution having originally been imported unmanaged and the queue name defined in the Rule Set not existing on import.

If you're struggling with a solution export, import or delete I'd recommend verifying the Routing Rule Sets and Case Creation Rules first.
