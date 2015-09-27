---
layout: post

title: Configure ssh keys 
subtitle: "How to not have to type a password each time you ssh onto a machine."
cover_image: blog-cover.jpg

excerpt: ""

draft: false

author:
  name: Darren
  twitter: daxaar
  <!--gplus: 100687498195339762535 -->
  bio: Director, Software Hack
  image: ks.png
---

In this post I'll explain how to setup ssh keys on a Mac so you no longer have to enter a password when connecting to a remote machine (generally *nix based) using ssh.

If you don't have homebrew installed consider [doing so now](http://brew.sh/).  To quote the authors: "It's the missing package manager for OSX".  Whilst not entirely necessary it will allow us to easily install the prerequisites.

1. Install `ssh-copy-id` which allows us to upload the public key to the remote more easily.

`brew install ssh-copy-id`

2. Create the public and private key pair file locally providing an optional password.  This will get stored under ~/.ssh.  Specifying a filename is optional.

`ssh-keygen`

3. Now we need to put the public key on the remote server.  The tool we installed in step 1 will allow us to easily do this. 

`ssh-copy-id user@serverip-or-name`

4. That's it!  `ssh` onto the machine using the user you specified in step 3 and if all went well you'll connect without having to provide a password.
