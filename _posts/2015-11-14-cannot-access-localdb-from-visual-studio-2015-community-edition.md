---
layout: post
title: Cannot access LocalDb from Visual Studio 2015 Community Edition
excerpt: 
author: daxaar
categories:
  - NET
  - Visual Studio

tags:
  - Entity Framework
  - Visual Studio 2015

draft: false
---
Today I was trying to spin up a quick Web API for an angular project I'm working on in a fresh install of Visual Studio 2015 using Entity Framework Code First.  Unfortunately after creating a simple model, when I tried to <em>update-database</em> to make sure all the moving parts were in a good state I was seeing the following error:

<blockquote>
<p class="p1">A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 50 - Local Database Runtime error occurred. The specified LocalDB instance does not exist.)</p>
</blockquote>

<p class="p1">After some investigation and questioning of whether LocalDB was installed (it was).  I discovered this error is caused by the connection string created by Entity Framework targeting an instance called MSSQLLocalDB which won't exist.  I believe the error occurs because VS 2015 sees that LocalDB is already installed during installation and therefore doesn't create this new instance on install.  The fix is to simply replace the instance name of MSSQLLocalDB with v11.0 in DefaultConnection in web.config.</p>

<p class="p1"></p>
