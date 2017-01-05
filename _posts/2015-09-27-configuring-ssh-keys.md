---
layout: post
title: Configuring ssh keys
excerpt:
author: daxaar
categories:
  - Bash Terminal
  - OSX
  - ssh
tags:

draft: false
---
In this post I'll explain how to setup ssh keys on a Mac so you no longer have to enter a password when connecting to a remote machine using ssh.

If you don't have homebrew installed consider <a href="http://brew.sh/">doing so now</a>. To quote the authors: "It's the missing package manager for OSX". Whilst not entirely necessary it will allow us to easily install the prerequisites.  

Install `ssh-copy-id` which allows us to upload the public key to the remote more easily.

~~~ bash
brew install ssh-copy-id
~~~

Create the public and private key pair file locally providing an optional password. This will get stored under ~/.ssh. Specifying a filename is optional.

~~~ bash
ssh-keygen
~~~

Now we need to put the public key on the remote server. The tool we installed in step 1 will allow us to easily do this.

~~~ bash
ssh-copy-id user@serverip-or-name
~~~

That's it! `ssh` onto the machine using the user you specified in step 3 and if all went well you'll connect without having to provide a password.
