---
layout: post
title: IIS 7 Powershell Provider under Windows Server 2008 R2
excerpt: 
author: daxaar
categories:
  - IIS
  - Powershell

tags:
  - IIS
  - Powershell

draft: false
---
I recently wanted to get access to the IIS Powershell cmdlets on a Windows Server 2008 R2 machine.  I initially thought I needed to install the Provider that can be downloaded from <a href="http://www.iis.net/powershell">iis.net</a>.  However, I soon realised this wasn't correct as running the MSI gave me the error "The Powershell Snapin is part of the Windows Operating System...".

After a quick google it turns out this feature is baked into R2 and installed through the <em>IIS Management Scripts and Tools</em> Service Role which is part of the Web Server Role (I always get confused if I should be looking in Features or Roles every time I go into the Server Manager snap-in).

With these installed there is one more step you need to take to get access to all the IIS goodness and that's to bring the module into your current Powershell session.  This can be achieved with the command <code>import-module WebAdministration</code>.

I hope this helps save others some time when accessing IIS through Powershell on a Windows Server 2008 <strong>R2 </strong>machine. 
