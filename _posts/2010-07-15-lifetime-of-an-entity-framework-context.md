---
layout: post
title: Lifetime of an Entity Framework Context
excerpt: 
author: daxaar
categories:
  - NET
  - Entity Framework

tags:

draft: false
---
<p>I'm currently working on an ASP.NET MVC application that uses Entity Framework 4 and Unity.  This project uses Unity for DI and the Repository and UnitOfWork patterns to abstract the EF as much as possible.  I won't cover any detail of the use of the latter two patterns within ASP.NET MVC here as it's been done to death across the internet, at least at a fairly high level.
</p><p>Each repository takes on its constructor a custom interface implementation reference to my models ObjectContext thus:
</p><p>Considerable name changing to protect the innocent!
</p><p><span style="font-size:10pt;"><span style="color:blue;">public</span>
			<span style="color:blue;">interface</span> IMyCustomContext<br />{<br />
			<span style="color:#2b91af;">IObjectSet</span>&lt;<span style="color:#2b91af;">Customer</span>&gt; Customers { get; set; }<br />
			<span style="color:#2b91af;">IObjectSet</span>&lt;<span style="color:#2b91af;">Order</span>&gt; Orders { get; set; }<br />}
</span></p><p>I extract this interface directly off the T4 generated MyCustomContext within Visual Studio and then create a partial class implementation of MyCustomContext and implement this interface.  Of course I don't have to do any implementation as this has already been taken care of in the T4 created MyCustomContext.  I do however then implement an IUnitOfWork interface on my partial implementation.  This has just one method on it called Save().  The implementation within my partial simply calls the SaveChanges() method on MyCustomContext.
</p><p>Ignoring the specifics of the repositories they each they take an implementation of this interface on their constructor.  There's another post I need to get done regarding why I send in the entire context rather than just the IObjectSet as many other samples have shown.
</p><p>OK that's a whole lot of text that's nothing to do with the title of this blog but I think it gives better context (geddit!) to the next section.
</p><p>The repository and context are used within my MVC site Controllers has constructor dependencies supplied by Unity and here's where we finally get to the LifetimeManager!
</p><p>Sample Controller:
</p><p><span style="font-size:10pt;"><span style="color:blue;">public class</span> <span style="color:#2b91af;">CustomerController</span> : <span style="color:#2b91af;">Controller</span><br />{<br />    <span style="color:blue;">private</span> <span style="color:blue;">readonly</span> <span style="color:#2b91af;">ICustomerRepository</span> _repository;<br />    <span style="color:blue;">private</span> <span style="color:blue;">readonly</span> <span style="color:#2b91af;">IUnitOfWork</span> _unitofwork;<br />
			<br />    <span style="color:blue;">public</span> CustomerController(<span style="color:#2b91af;">ICustomerRepository</span> repository, <span style="color:#2b91af;">IUnitOfWork</span> unitOfWork)<br />    {<br />        _repository = repository;<br />        _unitofwork = unitOfWork;<br />    }<br />
			<br />    [<span style="color:#2b91af;">HttpPost</span>]<br />    <span style="color:blue;">public</span> <span style="color:#2b91af;">ActionResult</span> Details(<span style="color:#2b91af;">Customer</span> customer)<br />    {<br />        <span style="color:blue;">if</span> (ModelState.IsValid)<br />        {<br />            _repository.Add(customer);<br />            _unitofwork.Save();<br />        }<br />
			<br />        <span style="color:blue;">return</span> <span style="color:red;">View</span>();<br />    }<br />}
</span></p><p>
 </p><p>Ignore the fact that there is actually only one piece of work (save) happening here.  The idea of the UnitOfWork is that it ties together multiple changes and commits these to your datastore as a single transaction (unit of work).  Imagine perhaps that we've saved an order also.
</p><p>So how are the repository and the unitofwork linked?  Well remember the unitofwork is just an interface into our MyCustomContext POCO class and the repository was passed an instance of MyCustomContext by Unity.  Within Unity configuration both IUnitOfWork and the IMyCustomContext constructor dependency for ICustomerRepository both resolve to MyCustomContext.  <strong>However, with the default TransientLifetimeManager used within Unity each will get its own instance of MyCustomContext.  This will almost certainly manifest itself as your code running successfully but nothing appearing in the database as the context called through unitofwork has no changes against it.  The changes are in the context held within the repository.
</strong></p><p>I first tried solving this problem by defining the LifetimeManager for the MyCustomContext as singleton.  However, this causes the context to throw an exception when you try and save due to a transaction issue.  What we needed was a way of telling Unity that for each Http Request we'd like it to use the same context.  This is achieved with the following custom Http Context Unity LifetimeManager:
</p><p>
 </p><p><span style="font-size:10pt;">    <span style="color:blue;">public</span> <span style="color:blue;">class</span> <span style="color:#2b91af;">HttpContextLifetimeManager</span>&lt;T&gt; : <span style="color:#2b91af;">LifetimeManager</span>, <span style="color:#2b91af;">IDisposable</span><br />    {<br />        <span style="color:blue;">public</span> <span style="color:blue;">override</span> <span style="color:blue;">object</span> GetValue()<br />        {<br />            <span style="color:blue;">return</span> <span style="color:#2b91af;">HttpContext</span>.Current.Items[<span style="color:blue;">typeof</span>(T).AssemblyQualifiedName];<br />        }<br />
			<br />        <span style="color:blue;">public</span> <span style="color:blue;">override</span> <span style="color:blue;">void</span> RemoveValue()<br />        {<br />            <span style="color:#2b91af;">HttpContext</span>.Current.Items.Remove(<span style="color:blue;">typeof</span>(T).AssemblyQualifiedName);<br />        }<br />
			<br />        <span style="color:blue;">public</span> <span style="color:blue;">override</span> <span style="color:blue;">void</span> SetValue(<span style="color:blue;">object</span> newValue)<br />        {<br />            <span style="color:#2b91af;">HttpContext</span>.Current.Items[<span style="color:blue;">typeof</span>(T).AssemblyQualifiedName] = newValue;<br />        }<br />
			<br />        <span style="color:blue;">public</span> <span style="color:blue;">void</span> Dispose()<br />        {<br />            RemoveValue();<br />        }<br />    }
</span></p><p>
 </p><p>The final piece in the puzzle for me was getting this to work with Unity design time configuration. The generic T in this code needs to represent MyCustomContext but how do you define generics in config.  QED it would seem as follows:
</p><p>
 </p><p><span style="color:blue;font-family:Consolas;">      &lt;<span style="color:#a31515;">register<span style="color:blue;"> <span style="color:red;">type<span style="color:blue;">=</span>"<span style="color:blue;">IMyCustomContext</span>"<span style="color:blue;"> <span style="color:red;">mapTo<span style="color:blue;">=</span>"<span style="color:blue;">MyCustomContext</span>"<span style="color:blue;">&gt;</span><br /><span style="color:blue;">        &lt;<span style="color:#a31515;">constructor<span style="color:blue;">/&gt;</span><br /><span style="color:blue;">        &lt;<span style="color:#a31515;">lifetime<span style="color:blue;"> <span style="color:red;">type<span style="color:blue;">=</span>"<span style="color:blue;">HttpContextLifetimeManager`1[MyCustomContext]</span>"<span style="color:blue;"> /&gt;</span><br /><span style="color:blue;">      &lt;/<span style="color:#a31515;">register<span style="color:blue;">&gt;</span>
															</span></span></span></span></span></span></span></span></span></span></span></span></span></span></p><p>
 </p><p>I hope this proves useful to someone.  Any questions, comments or berates feel free to drop me a line.</p>
