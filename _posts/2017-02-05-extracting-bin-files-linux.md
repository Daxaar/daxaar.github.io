---
layout: post
title: Extract a .bin disk image file under GNU/Linux
excerpt: How to convert and extract a .bin file from the GNU/Linux terminal  
author: Daxaar
categories:
  - Linux
  - Terminal
  - bash
  - HowTo
tags:

draft: false
comments: true
---

Binary image files (.bin) are a type of disk image format similar to the more
common .iso format.  They're a type of container file that when extracted or mounted
will provide access to their content.

If you search online for how to manage these files under Linux you'll see a lot of articles
stating that you can simply execute the file thus `./filename.bin`.  This is because .bin
files are commonly executable files on the *nix platform.  However, in the case of .bin disk image files this will not work.  

Here's how we crack open these files from the terminal.  It's a straightforward process
that involves converting the bin file to an ISO file and then mounting the ISO.

The high level steps are:

1. Create a .cue file if you don't have one.
2. Install bchunk
3. Convert the .bin to .iso using bchunk.
4. Mount the .iso file.
5. View the iso content.
6. Unmount the iso when complete.

The code below assumes all files are in your home directory. Make sure you have space in your home directory for both
the bin file and the converted iso file.

Step 1: You're going to need the associated .cue file but you may only have the .bin file.  No guarantee this will work but
you can try creating a cue file with the content below (make sure you change the FILENAME placeholder).  Save this
file alongside your .bin file with the same name i.e `my-file.cue` and `my-file.bin`.

~~~
FILE "FILENAME.bin" BINARY
  TRACK 01 MODE1/2352
    INDEX 01 00:00:00
~~~

Step 2: Install bchunk
~~~
sudo apt-get install bchunk
~~~

Step 3: Convert the .bin to .iso.  Make sure you get the arguments in the correct order.
~~~
bchunk ~/your-file.bin ~/your-file.cue ~/your-file.iso
~~~

Step 4: Create a mount point and mount the iso image.
~~~
sudo mkdir /mnt/iso
sudo mount -o loop ~/your-file.iso /mnt/iso
~~~

Step 5: Browse the content of your original bin.
~~~
ls /mnt/iso
~~~

Step 6: Once you've finished with the iso just unmount it
~~~
sudo umount /mnt/iso
~~~
