---
layout: post
title: Obtaining Typescript Definition Files
excerpt:
author: daxaar
categories:
  - npm
  - Typescript

tags:

draft: false
comments: true
---
### typings or the types npm organisation?

In this post I'll look at the current options available to us for managing the definition files (d.ts) in our typescript projects.

I recently started looking at the new features in typescript 2.0 and was surprised to find that <code>tsd</code> has been deprecated.  The deprecation isn't part of the 2.0 release as <code>tsd</code> is/was just external tooling but it quickly became part of my refresher that I thought I'd share here.

As a quick update <code>tsd</code> was a command line tool that allowed you to pull type definition files for external libraries (lodash, jquery etc) into your project.

I discovered we now have two options available to us that initially caused me some confusion as I wasn't sure if they were related in some way.  They're not.

### typings

The typings project is a community supported option hosted on github that has been the primary replacement for tsd.  It allows you to pull in definition files from a number of sources and continues to be supported.  It has a solid upgrade path if you're moving a project from <code>tsd</code>.

View the <a href="https://github.com/typings/typings">README</a> on the project repository for more info.

<h3>@types (organisation on npm)</h3>

The @types organisation on npm has been created by Microsoft as a response to the communities feedback that obtaining definition files has been troublesome.  At the time of writing the organisation contains 2247 separate packages.  Since this is a regular npm repository you'll just install the definition files as regular npm packages using the @prefix for the org:

~~~
npm install @types\lodash
~~~

The repository is populated from a <a href="https://github.com/Microsoft/types-publisher">publisher service</a> that continues to pull the definitions from the <a href="https://github.com/DefinitelyTyped/DefinitelyTyped">DefinitelyTyped</a> repo.  You could use it for pulling into a private repo if required.

Going forward I think I'll be using @types.  However, the new angular-cli uses typings which is how I was introduced to it's existence.  It'll be interesting to see if they continue to use typings or move over to using @types.

I'll be publishing another post soon describing how to configure a new typescript project to use @types.

Further reading:

Microsoft Blog Post - <a href="https://blogs.msdn.microsoft.com/typescript/2016/06/15/the-future-of-declaration-files/">The Future of Declaration Files</a>
