---
layout: post
title: TFS Check Out & Get Latest Version
excerpt: 
author: daxaar
categories:
  - Team Foundation Server

tags:

draft: false
---
<p>Over the last few days the guys in our team have started getting conflicts when checking back into source control despite exclusive check-out being set on all projects. It would seem that after doing some research, exclusive check-out in TFS no longer means exclusive or more accurately exclusive to the latest version.
</p><p>Consider the following scenario...
</p><p>Bob checks out file A<br>Bob makes changes to file A and checks back in.<br>Alice has the version of file A on her machine prior to Bob's changes.<br>Alice checks out file A
</p><p>Under VSS this would have brought the latest version of the file from the server to Alice's machine and checked it out to her.
</p><p>Under TFS Alice will receive check-out rights to the file preventing anyone else from changing it.  All is well so far, however the file that Alice is now editing is NOT the latest version from the server with Bob's changes, but the version she held prior to check-out.  When Alice attempts to check the file back in she is informed of a conflict with the version on the server.
</p><p>So what's happened?  Simple, TFS checks out the file BUT DOES NOT GET THE LATEST VERSION FROM THE SERVER leaving Alice to edit the "old" version.
</p><p>At first we assumed this was a bug but it turns out this is by design.  Microsoft has implemented this approach to prevent the local build for Alice from potentially being broken by changes applied by Bob.  Now the importance of not breaking the local build for Microsoft may be important given the scale of the projects they work on, but for us and I believe the majority of the development community this is not the case.  The time required to resolve changes is ridiculous and for some reason TFS disables the merge option on the dialog box leaving you to do it manually whilst trying to figure out what the implications are; usually dire on any large code changes.
</p><p>Now this approach is a reasonable option should it suit your development topology but the biggest mistake made by Microsoft is not giving you the option of turning this off!
</p><p>So how do you get around this issue?  There are two options...
</p><p>Option 1
</p><ol><li>In Team Explorer disable multiple check-out on ALL projects
</li><li>In VS2005 Source Control options, change from Silent Check Out to DO Nothing.  This means you have to manually check-out all files.  
</li><li>Before checking out do a Get Latest.  This makes the whole check-out process a more conscious exercise but still relies on the developer to be disciplined and we all know that ain't going to happen.
</li></ol><p>Option 2 (Our solution)
</p><p>As above except we have written a macro to perform the Get Latest and Check Out as one operation.  This doesn't resolve the issue entirely but does minimise as best as possible the chances of this happening.
</p><p>If like us you're not happy with this setup then I'm afraid you're going to have to wait for Orcas before it'll be changed (and it will as Microsoft has admitted they'll be changing it).
</p><p>I hope this information has proven useful and would welcome comments on any better solutions or whether you believe the approach taken within TFS currently is a good idea.</p>
