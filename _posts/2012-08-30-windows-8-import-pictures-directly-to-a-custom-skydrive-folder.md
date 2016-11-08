---
layout: post
title: Windows 8 - Import pictures directly to a custom SkyDrive folder
excerpt: 
author: daxaar
categories:
  - Operating Systems

tags:

draft: false
---
If you want to import pictures from a camera or any other USB device straight to a custom SkyDrive folder you can't do this using the Windows 8 Photo Application.  By default it will import all photos to your picture library which won't be linked to your SkyDrive folder.  Whilst you can then upload the imported pictures to SkyDrive manually, this will duplicate the content, it's far too time consuming and it will also incur the extra download from the SkyDrive servers to sync back with your local SkyDrive folder!  There must be a better way.

I've fixed this by setting up my pictures library to point straight to the pictures folder within my local SkyDrive folder (which is stored on a second hard disk rather than my SSD where space is always at a premium).  That way you're importing from USB straight to SkyDrive all through the new Windows 8 Photo Application.
</p>

<ol><li>Open Windows Explorer (Win + E)
</li><li>Move all of your pictures from Libraries\Pictures to the folder of your choice within your SkyDrive folder.  For most people this will be the default Pictures folder you are provided with SkyDrive.
</li><li><div>Right click on Libraries\Pictures and select Properties
</div><img src="http://frozenorange.files.wordpress.com/2012/08/083012_0729_windows8imp11.png" alt="" />
            </p></li><li><div>Select the path to the current pictures folder most likely C:\Users\<em>username</em>_000.  <span style="font-size:10pt;"><em>I don't like the way Windows 8 creates these folder names when using Windows Live for your login.</em></span>
            </div><p><img src="http://frozenorange.files.wordpress.com/2012/08/083012_0729_windows8imp21.png" alt="" />
            </p></li><li>Click Remove
</li><li>Click Add
</li><li>Navigate to the pictures folder within your SkyDrive folder you just moved all your pictures to
</li><li><div>Click Include Folder
</div><p><img src="http://frozenorange.files.wordpress.com/2012/08/083012_0729_windows8imp31.png" alt="" />
            </p></li><li><div>Click OK.
</div><p><img src="http://frozenorange.files.wordpress.com/2012/08/083012_0729_windows8imp41.png" alt="" />
            </p></li><li>Click OK.
</li></ol>

<p>You now have the Windows 8 Photo Application importing directly to your SkyDrive.

You can also hide the Picture Library from the photo app as this is now just duplicating your SkyDrive folder.  Open the charms menu (Win + C) inside the Photo App.  Select Settings, Options and uncheck Picture Library.  Alternatively you could setup a new "Local" picture library as I have done for importing/storing images you don't want synced to the cloud.
