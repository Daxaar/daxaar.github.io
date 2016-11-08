---
layout: post
title: ASP.NET MVC ModelView objects
excerpt: 
author: daxaar
categories:
  - NET

tags:

draft: false
---
I'm still playing around with Mvc 2 and came across the issue of presenting a composite type within a ModelView object.  When creating the view from this type it won't use the T4 template to generate your view for you or prepopulate from the FormsCollection on subsequent postback (yes I get that this is technically a webforms term).

Lets assume we have a class called Person.  This is our entity we'd like to get a generated view for and hook the FormCollection values through the default model binder on post.  However, the view also requires several lookups so we're passing through a ViewModel object.  We'll imaginatively call this PersonViewModel, thus:

<code>
public class PersonViewModel
{
Person OurPersonEntity {get;set;}
IEnumerable Titles {get;set;}
IEnumerable Countries {get;set;}
}
</code>

We want to build the view using the T4 templating off the OurPersonEntity.  When I first tackled this I assumed I'd need to select the PerrsonViewModel object as my strongly typed class when creating the view.  This of course leaves me with two issues.  Firstly the view won't generate using the T4 template against my composite type OurPersonEntity and the corresponding [HttpPost] method I create in the controller won't populate the OurPersonEntity using the default model binder.

Well, if you're still with me this can be done.  Simply create the view by defining the strong type in the View creation dialog as the Entity type (Person).  This gives you the view then simply update the type in the Page register directive to use the PersonViewModel type.  All we now need to do is update the generated code to reference the composite type.

A typical slice of the generated view would be:

<code>
HtmlHelper.TextBox("FirstName",model.FirstName)
</code>

Just change this to:

<code>
HtmlHelper.TextBox("FirstName",model.OurPersonEntity.FirstName)
</code>


You could of course also update the T4 template (search for Scott Hanselmann dev days 2010 for more info) if you were going to adopt this as a more common pattern throughout your solution.

As for the postback method on the controller.  We can just accept as a parameter the entity type thus:

<code>
[HttpPost]
public ActionResult Edit(Person person)
{
	if(ModelState.IsValid)
	{
		PersonRepository.Save(person);
	}
}
</code>

The clever bit here is that the Mvc framework on postback will reflect over the entire PersonViewModel object defined in the view.  Determine 
that the composite type of OurPersonEntity is the same as the type Person defined as the parameter to the controller method 
and populate using the default model binder!
