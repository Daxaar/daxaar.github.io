---
layout: post
title: Configuring Azure Hybrid Connections
excerpt: How to configure Hybrid Connections for connecting to an on-premise SQL Server  
author: Daxaar
categories:
  - Azure
  - SQL Server
  - HowTo
tags:

draft: false
comments: true
---

The Hybrid Connector is an Azure solution provided by Microsoft for connecting to your Azure App Services to on-premise resource(s) without the need to configure a VPN etc.  It works over ports 80 and 443 so it's firewall friendly although it does require us to install some software on the machine that hosts the services we're looking to expose.

You can use this feature to connect to any TCP based service but in this post I'll be configuring it for what will likely be the most common scenario which is connecting to an on-premise SQL Server on the standard TCP port 1433.
  