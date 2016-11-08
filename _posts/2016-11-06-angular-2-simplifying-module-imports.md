---
layout: post
title: Angular 2 - Simplifying Module Imports
excerpt: 
author: daxaar
categories:
  - Angular 2

tags:

draft: false
---
<a href="https://angular.io/docs/ts/latest/guide/ngmodule.html">NgModule</a> was a late addition to Angular 2 first appearing in RC5.  One of it's main purposes is to support lazy loading but it also helps reduce the code required for exporting and importing of components, directives and pipes.  This post isn't an intro to modules, there are plenty of those out there including the great docs on the angular site linked above.

What I want to look at in this post is how we can use a small quality of life feature to simplify the importing of modules into other modules using an index.ts to export all items from a module.

Below is the typical folder structure for a simple angular 2 app with the top level app module that will serve as our entry point and a single feature module called contact.  Somewhat contrived but it provides what we need.

[code lang=text]
/app
    app.component.ts
    app.component.html
    app.module.ts
    /contact
        contact.component.ts
        contact.directive.ts
        contact.pipe.ts
        contact.module.ts
[/code]

ContactModule (contact.module.ts) includes our ContactComponent (contact.component.ts), ContactDirective (contact.directive.ts) and ContactPipe (contact.pipe.ts) in its exports making them available to any module that imports ContactModule.

Our AppComponent (app.component.ts) wants to use the ContactComponent and ContactDirective so we must import them into our AppModule (app.module.ts).  It doesn't need the Pipe.

Our <code>AppModule</code> will look something like this:

[code lang=javascript]
//Import the module and individually the Component and Directive
import { ContactModule }    from &#039;./contact/contact.module&#039;;
import { ContactComponent } from &#039;./contact/contact.component&#039;;
import { ContactDirective } from &#039;./contact/contact.directive&#039;;

@NgModule({
    imports: [ContactModule],
    exports: [],
    declarations: [AppComponent]
})
export class AppModule() {}
[/code]

Even though we import the module ContactModule we must also include the imports for the ContactComponent and ContactDirective or neither of them will be available inside AppModule.

If the ContactModule is imported into lots of other modules this can lead to repetitive code.  If we add something new to ContactModule we'd need to add the imports to each module that already imports ContactModule.  Bit of a pain!

The solution to this is to create a "feature exports" file for all the exports from our contact feature.  We only have to then import this file defining the items we want to use.  Also, if we name this file index.ts we can also omit the filename when defining the import statement in the imorting module.

The new folder structure will now look as follows including our new <code>index.ts</code> file in the feature folder:

[code lang=text]
/app
    app.component.ts
    app.component.html
    app.module.ts
    /contact
        contact.component.ts
        contact.directive.ts
        contact.pipe.ts
        contact.module.ts
        index.ts
[/code]

<code>index.ts</code> will contain the following:

[code lang=javascript]
export { ContactComponent } from &#039;./contact.component&#039;;
export { ContactDirective } from &#039;./contact.directive&#039;;
export { ContactPipe }      from &#039;./contact.pipe&#039;;
export { ContactModule }    from &#039;./contact.module&#039;;
[/code]

Now when we want to import the contact feature module into our app module we just need to import the "feature file" for which we don't even have to specify the filename due to convention just the feature folder name...nice!:

[code lang=javascript]
//Import what we need from the &#039;contact feature&#039;
import { ContactComponent, ContactDirective } from &#039;./contact&#039;;

@NgModule({
    imports: [ContactModule],
    exports: [],
    declarations: []
})

[/code]
