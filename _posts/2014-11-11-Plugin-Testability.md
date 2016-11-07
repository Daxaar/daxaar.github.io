---
title: Plugin Execution Context
excerpt: "Keeping control of your plugin execution context"
author: daxaar
layout: post
categories:
- dynamics-crm
tags:
- dynamics-crm
comments: true
draft: true
---

In this post I'd like to explore an alternative way of orchestrating multiple plugins in a single execution context.

Consider the following plugin execution steps for the creation of a Case:

Pre-Operation:  
- `CalculateCaseCommencementDate`  
- `GenerateCaseReferenceNumber`  
- `CalculateCompletionDate`  

Post-Operation:  
- `UpdateSharePointFolders`

Consider the following User Story:

As a Sales Manager I want to track all Procurement Requests for my clients so that I can ensure the Accounts Team onboard any new clients in a timely manner.   

On creation of a new Procurement Request record:

1. Validate the Procurement record against the Procurement Template for the Sales Manager.
2. Send an email to the Sales Manager.
3. Create a Task for the Finance Team to create the new Account.

Don't worry about the specifics or even the validity of such a process.  The key thing is that there is more than one business rule to be forfilled in the creation of the Procurement record.  Typically we might create three plugins for this User Story thus:

Name: ValidateProcurementAgainstTemplatePlugin
Step: PreOperation


When developing an ASP.NET MVC solution it's considered a good design practice to keep your controllers "skinny".  There are plenty of resources on the web that cover this in more detail but what this essentially boils down to is your Controllers shouldn't contain domain layer business logic they should do nothing more than
