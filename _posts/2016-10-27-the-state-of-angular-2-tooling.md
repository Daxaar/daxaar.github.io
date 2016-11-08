---
layout: post
title: The state of Angular 2 Tooling
excerpt: 
author: daxaar
categories:
  - NET
  - Angular 2

tags:

draft: false
---
The Angular 2 framework has now been released so it's a great time to jump in and learn the ropes. However, whilst we can relax our attention on the changing API's in the framework for a short time, we're still faced with the endlessly changing world of front end tooling.

Webpack is currently top of the pile for all of our developer workflow needs. But what else is there and where do we start?

<h2>Angular cli</h2>

A fork of the ember cli that's recently been updated to support webpack replacing systemjs. This is almost certainly going to be the dominant player going forward as it has some prominent angular community contributors. Remember that much of the featureset comes from webpack rather than the cli itself.

<h5>For:</h5>

<ol>
<li>Your lowest friction option for getting a project up an running.</li>
<li>The generators are really useful for creating the often repeated boilerplate in an Angular app.</li>
<li>The generators help maintain consistency across an application in the absence of existing coding standards.</li>
<li>Built on test first principles. Unit and e2e tests are baked into the generators.</li>
</ol>

<h5>Against:</h5>

<ol>
<li>Performance overall is mediocre. Initialising a new project or running tests for the first time can be very slow.</li>
<li>Still in beta and past changes show they're not afraid to move the goal posts by quite some margin.</li>
<li>Currently no OOB support for cache busting in the webpack build.</li>
<li>The inline help system isn't good.</li>
<li>Due to the development cadence it's difficult to get answers to problems. Most answered questions on stackoverflow are long out of date.</li>
</ol>

<h2>ASP.NET Core Yeoman generators</h2>

If you're looking at developing an Angular application using ASP.NET Core for the backend <a href="https://www.npmjs.com/package/generator-aspnetcore-angular2">these generators</a> are worth a look.

This is a great video by Steve Sanderson at <a href="https://youtu.be/C6MPSLgsGGs">NDC Sydney 2016</a> discussing their capability in some detail.

<h2>Community Starter Templates</h2>

These are a couple of github projects that provide a basic application along with some preconfigured tooling. Generally they're going to provide the same bootstrapped project experience as you'll get from the angular cli but in a slightly lighter touch template.

<a href="https://github.com/preboot/angular2-webpack">preboot/angular2-webpack</a>

Low touch template with testing baked in and a solid README to get you going. As of this writing still being updated regularly.

<a href="https://github.com/mgechev/angular-seed#running-tests">mgechev/angular-seed</a>

Gulp based build - not a bad thing! It's an older project but it's still being updated. Again the README is solid and there are a number of forked reference sites linked that may prove handy.
