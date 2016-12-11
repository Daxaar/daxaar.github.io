---
layout: post
title: systemform With Id = {guid} Does Not Exist
excerpt:
author: daxaar
categories:
  - Dynamics Crm

tags:
  - Crm2013

draft: false
---
Solution Import Error systemform With Id = {guid} Does Not Exist

I was struggling with this error recently whilst trying to import a managed solution into a CRM 2013 SP1 integration environment.  It turns out that the form that it was telling me didn’t exist was a Quick Form that did!

Having confirmed the form existed in the org and solution I exported from I decided to open up the zip file to have a look through the customizations.xml file. I searched for the guid and could see that the Quick View form was as expected included correctly and the reference to it from the related form was also included.

The only thing I could think was that the form that referenced the quick view form was included in the Xml before the actual form that contained the quick view definition. I moved the element containing the quick view form above the that was referencing it, repackaged and tried again. This time the import work successfully!

So:

<ol>
<li>Open up your solution zip and edit the customizations.xml file searching for the guid provided in the solution import error log.</p></li>
<li><p>For each <em>&lt;Entity&gt;</em> that uses the Quick Form you'll see it contains a <em>&lt;QuickFormIds&gt;</em> element similar to that shown below.  You need to make sure that the <em>&lt;Entity&gt;</em> element for the entity it refers to (xyz_entityName in this case) appears in the file BEFORE the <em>&lt;Entity&gt;</em> that is referencing it via the QuickFormIds element.</p></li>
</ol>

~~~ xml
<QuickFormIds>
  <QuickFormId entityname="xyz_entityName">33d82ce4-0648-477c-a1b8-08ddd4b6e5be</QuickFormId>
</QuickFormIds>
~~~

<p>Looks like a bug that will hopefully get sorted in the next rollup.
