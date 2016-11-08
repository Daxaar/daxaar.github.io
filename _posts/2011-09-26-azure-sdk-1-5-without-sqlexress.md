---
layout: post
title: Azure SDK 1.5 without SQLEXRESS
excerpt: 
author: daxaar
categories:
  - Azure

tags:

draft: false
---
If you've come across the error in Visual Studio telling you it failed to initialise the development store you almost certainly don't have SQLEXPRESS installed or it's just stopped.  If it's the latter feel free to leave now and fire it up!

<img src="http://frozenorange.files.wordpress.com/2011/09/092611_2035_azuresdk15w1.png" alt="" />

Still here?  OK so you want development storage against the full SQL Server instead of SQLEXPRESS.  For this you'll need to run the SDK utility <strong>dsinit</strong> located under <em><strong>Program Files\Windows Azure SDK\v1.5\bin\devstore</strong>.
</em>

<img src="http://frozenorange.files.wordpress.com/2011/09/092611_2035_azuresdk15w2.png" alt="" /><em>
        </em>

You don't need to manually edit configuration any longer as per SDK 1.0. <em>
        </em>Double clicking the exe will display a GUI and attempt to initialise the development store which will of course fail.  In order to fix this open a prompt from the <strong>devstore</strong> folder (Shift-Right Click the <strong>devstore</strong> folder for the Open Command Window Here option) and run the command

<span style="font-family:Courier New;">dsinit /sqlinstance:.
</span>

<img src="http://frozenorange.files.wordpress.com/2011/09/092611_2035_azuresdk15w3.png" alt="" />

If all is well you'll see the dsinit GUI showing a successful init.  You can now return to Visual Studio, start debugging and enjoying the world of Azure.

 
