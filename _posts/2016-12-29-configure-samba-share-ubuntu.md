---
layout: post
title: Install and configure a Samba network share on Debian
excerpt: The steps to install and configure a network share on Debian and make this accessible from Windows
author: daxaar
categories:
  - Linux
  - Debian
  - bash
  - Samba
tags:

draft: false
comments: true
---
We can create and share a directory on the network with Windows clients using Samba.  This is an
[open source package](https://www.samba.org) providing a fast, stable and secure implementation of the CIFS/SMB protocol.

### Installing Samba

Open up your terminal of choice and install the required packages.

~~~
sudo apt-get install samba system-config-samba gvfs-bin gvfs-backends
~~~

Create a directory to share.  Don't worry too much about what this is called or where it's located.  The directory name won't be seen and we can symlink in any additional folders.  Let's just create a folder called samba-share under our home directory.

~~~
mkdir /home/darren/samba-share
~~~


We now need to edit the Samba configuration file but let's create a backup first.

~~~
sudo cp /etc/samba/smb.conf ~
~~~

Open up the `/etc/samba/smb.conf` file in your editor of choice (vim, nano, leafpad)
~~~
sudo vim /etc/samba/smb.conf
~~~

Before we start bear in mind that whitespace matters in this file so make sure you include the spaces before and after the =.

First we add the following line to the [global] section.  This section will already exist in the file, so just place the line at the top.  This line isn't entirely necessary but it will allow us to symlink other directories into the share and let windows clients navigate these.

~~~
[global]
allow insecure wide links = yes #This is the only line we're adding to [global]
~~~

Now we add the configuration for our new share at the bottom of the file.  For more info on what each line does see the [smb.conf docs](https://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html) on the samba.org website.

~~~
[sharename]                     #This is the name that will be seen on the network
follow symlinks = yes           #This will allow clients to navigate the content of symlinks
wide links = yes                #As above
comment = My first samba share  #Anything amusing you like
path = /home/darren/samba-share #The path to the folder we created in step 2.
browsable = yes                 #Share will be displayed at server level by client
guest ok = no                   #Prevent anonymous access
read only = no                  #Self explanatory
create mask = 0755              #File mask applied to files created within the share by a windows client
~~~

Save and close the file.

Create a Samba user and set a password.  The username doesn't have to be the same as your login name although I usually keep it the same for simplicity.
~~~
sudo smbpasswd -a darren
~~~

Stop and restart the required services

~~~
sudo service smdb restart
sudo service nmdb restart
~~~

We're done!

If you now open file explorer (Nautilus etc) and navigate to `smb://localhost` you should see the new share available.  As long as you see this you can now go ahead and map a network drive to this share from windows using the username and password you just created.
