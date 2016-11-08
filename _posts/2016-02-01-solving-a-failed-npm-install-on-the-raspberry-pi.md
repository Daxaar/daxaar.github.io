---
layout: post
title: Solving a failed npm install on the Raspberry Pi
excerpt: 
author: daxaar
categories:
  - NET
  - NPM

tags:

draft: false
---
TL;DR If you are struggling with <code>npm install</code> failing on a package you are convinced is no longer a dependency of your current package.json structure. Try clearing out your node_modules folder or take a look at the <code>npm prune</code> command.

I know this post is quite a long one but most of the content was created in realtime as I was working the problem. I'm a voracious note taker so figured I'd just write up my notes as a blog post as I went along.

I have a little express website running on my raspberry pi B+ from home. I deploy to this site using a post-receive git hook that deploys the master branch and runs <code>npm install --production</code> to ensure the latest dependencies are installed. Notice that I use the --production switch to ensure devDependencies are not installed.

After trying to access this site following a push I found the site to be unavailable. I use forever to maintain the node process so I checked the logs and noticed a number of errors indicating new dependencies had not been installed.

I ssh'd into the server and run <code>npm install --production</code> manually and saw that it was taking an unusually long time to complete eventually failing due to native module compilation failure.

Here are the new packages my latest commit has introduced:

<ul>
<li>dependencies</li>
<li>passport</li>
<li>passport-local</li>
<li>devDependencies</li>
<li>browser-sync</li>
<li>gulp</li>
<li>gulp-nodemon</li>
</ul>

As you can see, passport and passport-local are the only packages that should be installed. However, after I traced the failed module up the dependency tree shown below you can see that npm was trying to install browser-sync whose dependency graph relies on native modules.

<code>bufferutil</code> -&gt; <code>ws</code> -&gt; <code>engine.io</code> -&gt; <code>socket.io</code> -&gt; <code>http-proxy</code> -&gt; <code>foxy</code> -&gt; <code>browser-sync</code>

At this point I checked online to see if there were any known issues but only came up with <a href="https://github.com/npm/npm/issues/1434">this github issue</a> which is old and closed.

Let's see what the status of the <code>--production</code> switch is in the <a href="https://docs.npmjs.com/cli/install">current npm docs</a>

<blockquote>
  With the --production flag (or when the NODE_ENV environment variable is set to production), npm will not install modules listed in devDependencies.
</blockquote>

That seems consistent with my understanding. So let's make sure we're on the latest version of npm and see if that fixes it.

My npm version (at the the time of posting) is <code>3.3.12</code>, let's update with the utter brain f*ck that is self updating software.

<code>sudo npm install npm -g</code>

The update has taken us to <code>3.6.0</code> but having tried to run <code>npm install --production</code> again I'm getting the same result with a failed compile.

So I know that the dependency causing the problem is browser-sync. Let's confirm this by removing it from package.json. When I now run <code>npm install</code> it shouldn't matter whether it does or doesn't install devDependencies as the package causing the problem isn't in either section.

To my surprise this still fails! OK <code>npm install</code> is clearly not just running through the package.json and installing the specified packages and their dependencies as I expected.

The next logical step (yes I know, many of you may have arrived at this point long ago) is to delete my node_modules folder and rerun <code>npm install</code>.

Success! Everything installs as required.

What's going on? Well, it would seem that <code>npm install</code> doesn't just install packages and dependencies defined in your package.json. Instead it sees your package.json as simply the top level in the dependency graph. Once it's completed the install for all the packages in your package.json, it must then start enumerating all of the packages under node_modules and repeat the process for their package.json files.

This behaviour makes sense and more importantly for me would explain how I ended up with this problem. My git hook script does an npm install <em>without the --production</em> switch. After I'd fixed this up as part of my analysis of this issue I'd fixed the problem for future deployments but I'd left my node_modules folder in an invalid state because the failing module (browser-sync) was still in there.

Further reading on this problem shows there is an npm command called <code>prune</code> that will clear all dangling dependencies from your node_modules folder based on your current package.json. In fact we can do the following to clear out just our devDependencies, a common requirement if we've inadvertently installed them on the production box...as if!

<code>npm prune --production</code>

So, problem solved.  I hope this post has been useful or at least mildly entertaining for the more initiated out there.
