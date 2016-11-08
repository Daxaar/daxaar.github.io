---
layout: post
title: Error when saving URL addressed record in CRM 2011 (Rollup 5)
excerpt: 
author: daxaar
categories:
  - Dynamics Crm

tags:

draft: false
---
<span style="font-family:Cambria;">If you're on Rollup 6 or higher you can <a href="http://social.microsoft.com/Forums/ur-PK/crm/thread/f5e4da83-e8ba-442b-b893-9ab4b7acb282">ignore this</a> post.
</span>

<span style="font-family:Cambria;">I came across a problem today when loading a record using the URL addressable form feature as documented over on the Microsoft site <a href="http://msdn.microsoft.com/en-us/library/gg328483.aspx">here</a>.  The record would load fine but when I tried saved the record the page wouldn't refresh correctly.  I would end up with a disabled ribbon and no other page content!  The save operation was however succeeding.
</span>

<span style="font-family:Cambria;">I traced this down to an exception being thrown from within the platform JavaScript code.  It was making the assumption that the querystring value <strong>extraqs</strong> was available and calling <em>string</em>.startsWith()which was throwing the null exception.
</span>

<span style="font-family:Cambria;">If you take a look at the URL for any entity loaded via a hyperlink in CRM they all contain this parameter which is typically used to pass attribute values to a form so those values can be pre-populated on load.  The value of this parameter must be URL encoded.
</span>

<span style="font-family:Cambria;">Here's a contact loaded from the default Homepage grid:
</span>

<span style="font-family:Cambria;font-size:10pt;"><em>http://server/org/main.aspx?etc=2&amp;extraqs=%3f_gridType%3d2%26etc%3d2%26id%3d%257b0F837B6D-249A-E111-902A-000C2945F65C%257d%26rskey%3d667293691&amp;pagetype=entityrecord
</em></span>

<span style="font-family:Cambria;">Here's the sample URL provided for loading an account on the MSDN article linked above:
</span>

<span style="color:black;font-family:Cambria;font-size:10pt;"><em>http://<span style="color:#1f497d;">myorg.crm.dynamics.com<span style="color:black;">/main.aspx?etn=account&amp;pagetype=entityrecord&amp;id=%7B<span style="color:#1f497d;">91330924-802A-4B0D-A900-34FD9D790829<span style="color:black;">%7D
</span></span></span></span></em></span>

<span style="color:black;font-family:Cambria;">Switching out the values in blue for environment specific values you'll see that the record will load correctly.  However, if you then make a change and click save the page will hang as show below.
</span>

<img src="http://frozenorange.files.wordpress.com/2012/05/051812_2049_errorwhensa11.png" alt="" /><span style="color:black;">
        </span>

 

<span style="color:black;font-family:Cambria;">Reformatting the sample URL as follows (<strong>bolded</strong>) will fix the issue when saving the record.
</span>

<span style="font-family:Cambria;font-size:10pt;"><em>http://myorg.crm.dynamics.com/main.aspx?etn=account&amp;pagetype=entityrecord&amp;id=%7B91330924-802A-4B0D-A900-34FD9D790829%7D<strong>&amp;extraqs=anyvalueyoulikeorempty</strong>
            </em></span>

<span style="color:black;">
        </span> 
