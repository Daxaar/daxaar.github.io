---
layout: post
title: AppFabric and WAS 1 Windows Service 0
excerpt: 
author: daxaar
categories:
  - General

tags:

draft: false
---
We recently received a proposal from a supplier for their integration into our backend stock control system.  A requirement of the solution is asynchronous communication in both directions so MSMQ was recommended as expected.  However, I was surprised to see the implementation their side for processing messages was a Windows Service.  The platform is entirely Windows Server 2008 and .NET 4.0 so the choice of a Windows Service which carries with it all of the responsibilities of appropriate application management is in my opinion the wrong choice.

The "better" solution in the absence of a full Service Bus (Biztalk etc) would be implemented using <a href="http://technet.microsoft.com/en-us/library/cc735229(WS.10).aspx">Windows Activation Service</a> (WAS) hosted WCF/WF Services enriched by AppFabric.  This feature set provides so many functional and operational benefits; I struggle to see where a valid use case exists for implementing any messaging solution via a Windows Service.  That's a broad statement that can't hold true for all requirements but I believe architecturally when the discussion turns to a Windows Service we should be asking the question <strong>"Why shouldn't we do this in IIS/WAS and AppFabric?"</strong> rather than <strong>"Why should we?"
</strong>

Below are some of the benefits (not just limited to message queuing) of WAS and AppFabric you can leverage without writing a line of additional code
</p>

<ol style="margin-left:54pt;"><li>Leverage common deployment practices through MSDeploy
</li><li>WAS alone (via the IIS Process Model) will provide significantly enhanced Process Management through built in and easily configurable:
</li></ol>

<ul style="margin-left:72pt;"><li>Recycling
</li><li>Throttling
</li><li>Security
</li><li>Scalability (shared worker process where appropriate)
</li></ul>


 

<ol style="margin-left:54pt;"><li>AppFabric will provide (again through easy configuration):
</li></ol>

<ul style="margin-left:72pt;"><li>IIS Management Console integration giving visibility into configurable searchable metrics via the AppFabric dashboard.
</li><li>Workflow Persistence including idle time management
</li><li>Caching Services (additional install)
</li><li>Configurable Service Auto Start (requires Server 2008 R2)
</li><li>WCF Endpoint Management
</li><li>Easy configuration of WCF/WF Event Tracing
</li><li>Easier integration of custom monitoring services (i.e. a custom system reporting website)
</li><li>Pluggable tracking/tracing profiles
</li><li>Easier integration for reporting into SCOM (additional install pack)
</li></ul>

Significantly, AppFabric Server will also provide you with a head start (albeit a small one) into the runtime framework of <a href="http://www.microsoft.com/windowsazure/appfabric/">Azure AppFabric</a> as the two offerings begin to converge over the next few years.

I hope this post has proven useful to someone looking at delivering application services that might otherwise have considered a Windows Service to be their only option. AppFabric is available through the Web Platform Installer and further information on Windows Server AppFabric can be found <a href="http://msdn.microsoft.com/en-us/windowsserver/ee695849">here</a>.
