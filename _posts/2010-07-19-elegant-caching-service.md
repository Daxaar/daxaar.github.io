---
layout: post
title: Elegant Caching Service
excerpt: 
author: daxaar
categories:
  - NET

tags:

draft: false
---
I was looking for common data caching patterns recently and came across a rather simple but imo very elegant solution for caching on Stack Overflow. The source is below and I've included a link to ensure the original author gets full credit.

<code>public class InMemoryCache: ICacheService</code>
<code>{</code>
<code>  public T Get&lt;T&gt;(string cacheID, Func&lt;T&gt;; getItemCallback) where T : class</code>
<code>  {</code>
<code>    T item = HttpRuntime.Cache.Get(cacheID) as T;</code>
<code>    if (item == null)</code>
<code>    {</code>
<code>      item = getItemCallback();</code>
<code>      HttpContext.Current.Cache.Insert(cacheID,item);</code>
<code>    }</code>
<code>    return item;</code>
<code>  }</code>
<code>}</code>

As you can see this method takes as a second param a Func&lt;T&gt;; delegate that will be called if the requested item is not in the cache. So the call from my MVC Controller now looks like:
<code>model.Countries = _cacheService.Get(
</code><code>"countries&gt;, () =&gt; _referenceDataRepository.GetCountries());</code>
<code>model.Genders = _cacheService.Get("genders",() =&gt; _referenceDataRepository.GetGenders());</code>
<code>model.Titles = _cacheService.Get("titles",() =&gt; _referenceDataRepository.GetTitles());</code>

<a href="http://stackoverflow.com/questions/343899/how-to-cache-data-in-a-mvc-application">Original StackOverflow Post</a>
